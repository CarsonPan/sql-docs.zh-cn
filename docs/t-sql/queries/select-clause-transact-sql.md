---
title: "SELECT 子句 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT Clause
- SELECT_Clause_TSQL
- DISTINCT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- identity columns [SQL Server], SELECT clause
- SELECT clause
- $IDENTITY keyword
- user-defined types [SQL Server], invoking methods and properties
- SELECT statement [SQL Server], processing orders
- clauses [SQL Server], SELECT
- $ROWGUID keyword
- queries [SQL Server], results
ms.assetid: 2616d800-4853-4cf1-af77-d32d68d8c2ef
caps.latest.revision: 54
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8b6972868c221ec0368b689164eff740ae6f1a7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="select-clause-transact-sql"></a>SELECT 子句 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定要由查询返回的列。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [ ALL | DISTINCT ]  
[ TOP ( expression ) [ PERCENT ] [ WITH TIES ] ]   
<select_list>   
<select_list> ::=   
    {   
      *   
      | { table_name | view_name | table_alias }.*   
      | {  
          [ { table_name | view_name | table_alias }. ]  
               { column_name | $IDENTITY | $ROWGUID }   
          | udt_column_name [ { . | :: } { { property_name | field_name }   
            | method_name ( argument [ ,...n] ) } ]  
          | expression  
          [ [ AS ] column_alias ]   
         }  
      | column_alias = expression   
    } [ ,...n ]   
```  
  
## <a name="arguments"></a>参数  
 **ALL**  
 指定在结果集中可以包含重复行。 ALL 为默认值。  
  
 DISTINCT  
 指定在结果集中只能包含唯一行。 对于 DISTINCT 关键字来说，Null 值是相等的。  
  
 顶部 (*表达式*) [百分比] [WITH TIES]  
 指示只能从查询结果集返回指定的第一组行或指定的百分比数目的行。 *expression* 可以是行数或行的百分比。  
  
 为了向后兼容，使用 TOP*表达式*不带括号中选择支持语句，但我们不建议这样做。 有关详细信息，请参阅[顶部 &#40;Transact SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
  
\<select_list > 要为结果集选择的列。 选择列表是以逗号分隔的一系列表达式。 可在选择列表中指定的表达式的最大数目是 4096。  
  
 \*  
 指定返回 FROM 子句中的所有表和视图中的所有列。 这些列按 FROM 子句中指定的表或视图顺序返回，并对应于它们在表或视图中的顺序。  
  
 *table_name* | *view_name* | *表*_*别名*。 *  
 限制的作用域\*到指定的表或视图。  
  
 *column_name*  
 要返回的列名。 限定*column_name*若要避免不明确的引用，例如当两个表在 FROM 子句中时发生使具有相同名称的列。 例如，SalesOrderHeader 和 SalesOrderDetail 中的表[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库这两个具有一个名为 ModifiedDate 列。 如果将这两个表加入查询，则可以在选择列表中指定 SalesOrderDetail 项的修改日期，即 SalesOrderDetail.ModifiedDat。  
  
 *expression*  
 常量、函数以及由一个或多个运算符连接的列名、常量和函数的任意组合，或者是子查询。  
  
 $IDENTITY  
 返回标识列。 有关详细信息，请参阅[标识 &#40;属性 &#41;&#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)， [ALTER TABLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md)，和[创建 TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 如果 FROM 子句中的多个表内都包含具有 IDENTITY 属性的列，则必须使用特定的表名限定 $IDENTITY（如 T1.$IDENTITY）。  
  
 $ROWGUID  
 返回行 GUID 列。  
  
 如果在 FROM 子句中有多个表具有 ROWGUIDCOL 属性，则必须用特定的表名限定 $ROWGUID，如 T1.$ROWGUID。  
  
 *udt_column_name*  
 要返回的公共语言运行时 (CLR) 用户定义类型列的名称。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 返回以二进制表示形式表示的用户定义类型值。 若要在字符串或 XML 格式返回用户定义类型值，使用[强制转换](../../t-sql/functions/cast-and-convert-transact-sql.md)或[转换](../../t-sql/functions/cast-and-convert-transact-sql.md)。  
  
 { . | :: }  
 指定 CLR 用户定义类型的方法、属性或字段。 使用。 用于实例（非静态）方法、属性或字段。 将 :: 用于静态方法、属性或字段。 若要调用 CLR 用户定义类型的方法、属性或字段，必须对类型具有 EXECUTE 权限。  
  
 *property_name*  
 是的一个公共属性*udt_column_name*。  
  
 *字段名*  
 公共数据成员的*udt_column_name*。  
  
 *method_name*  
 是一个公共方法的*udt_column_name*采用一个或多个参数。 *method_name*不能为赋值函数方法。  
  
 以下示例通过调用名为 `Location` 类型的方法，从 `point` 表中选择 `Cities` 列的值（定义为 `Distance` 类型）：  
  
```  
CREATE TABLE dbo.Cities (  
     Name varchar(20),  
     State varchar(20),  
     Location point );  
GO  
DECLARE @p point (32, 23), @distance float;  
GO  
SELECT Location.Distance (@p)  
FROM Cities;  
```  
  
 *column_ 别名*  
 查询结果集内替换列名的可选名。 例如，可以为名为 quantity 的列指定别名，如 Quantity、Quantity to Date 或 Qty。  
  
 别名还可用于为表达式结果指定名称，例如：  
  
 `USE AdventureWorks2012`;  
  
 `GO`  
  
 `SELECT AVG(UnitPrice) AS [Average Price]`  
  
 `FROM Sales.SalesOrderDetail;`  
  
 *column_alias*可在 ORDER BY 子句。 但不能用于 WHERE、GROUP BY 或 HAVING 子句中。 如果查询表达式是 DECLARE CURSOR 语句的一部分*column_alias*不能在 FOR UPDATE 子句中。  
  
## <a name="remarks"></a>注释  
 为返回的数据的长度**文本**或**ntext**选择列表中包含的列设置为以下的最小值： 的实际大小**文本**列、 默认 TEXTSIZE 会话设置或硬编码的应用程序限制。 若要更改会话的返回文本长度，请使用 SET 语句。 默认情况下，用 SELECT 语句返回的文本数据的长度限制是 4,000 字节。  
  
 如果发生下列两种情况中的一种，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 将引发编号为 511 的异常错误并回滚当前运行的语句：  
  
-   SELECT 语句生成超过 8,060 字节的结果行或中间级工作表。  
  
-   尝试对超过 8,060 字节的行执行 DELETE、INSERT 或 UPDATE 语句。  
  
 如果没有为 SELECT INTO 或 CREATE VIEW 语句创建的列指定列名，将会发生错误。  
  
## <a name="see-also"></a>另请参阅  
 [选择示例 &#40;Transact SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)  
  
  
