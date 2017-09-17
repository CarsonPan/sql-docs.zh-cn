---
title: "计数 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COUNT_TSQL
- COUNT
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT function
- totals [SQL Server]
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT function [Transact-SQL]
ms.assetid: 28d39da6-bc2e-46c7-858c-b1721c938830
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6750b73e1b6833c9cb80c69d758351d961990f7a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="count-transact-sql"></a>COUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回组中的项数。 计数工作方式类似于[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)函数。 两个函数唯一的差别是它们的返回值。 COUNT 始终返回**int**数据类型值。 始终返回 COUNT_BIG **bigint**数据类型值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )   
    [ OVER (   
        [ partition_by_clause ]   
        [ order_by_clause ]   
        [ ROW_or_RANGE_clause ]  
    ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregation Function Syntax  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )  

-- Analytic Function Syntax  
COUNT ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>参数  
**ALL**  
向所有值应用此聚合函数。 ALL 为默认值。
  
DISTINCT  
指定 COUNT 返回唯一非 Null 值的数量。
  
*expression*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)以外的任意类型的**文本**，**映像**，或**ntext**。 不允许使用聚合函数和子查询。
  
\*  
指定应该计算所有行以返回表中行的总数。 计数 (\*) 不采用任何参数并不能与 DISTINCT 一起使用。 计数 (\*) 不需要*表达式*参数因为根据定义，它不使用任何特定的列的相关信息。 COUNT(*) 返回指定表中行数而不删除副本。 它对各行分别计数。 包括包含空值的行。
  
通过**(** [ *partition_by_clause* ] [ *order_by_clause* ] [ *ROW_or_RANGE_clause* ] **)**  
*partition_by_clause*将划分为分区函数应用到的 FROM 子句生成的结果集。 如果未指定，则此函数将查询结果集的所有行视为单个组。 *order_by_clause*确定在其中执行该操作的逻辑顺序。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>返回类型
 **int**  
  
## <a name="remarks"></a>注释  
COUNT(*) 返回组中的项数。 包括 NULL 值和重复项。
  
计数 (所有*表达式*) 的计算结果*表达式*组中每一行，并返回非 null 值的数目。
  
计数 (DISTINCT*表达式*) 的计算结果*表达式*组中每一行，并返回唯一、 非 null 值的数目。
  
对于大于 2^31-1 的返回值，COUNT 生成一个错误。 这时应使用 COUNT_BIG。
  
COUNT 不与 OVER 和 ORDER BY 子句配合使用时为确定性函数。 与 OVER 和 ORDER BY 子句一同指定时，它具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
## <a name="examples"></a>示例  
  
### <a name="a-using-count-and-distinct"></a>A. 使用 COUNT 和 DISTINCT  
以下示例列出了在 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 工作的雇员可以拥有的不同职位的数量。
  
```sql
SELECT COUNT(DISTINCT Title)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `67`  
  
`(1 row(s) affected)`
  
### <a name="b-using-count"></a>B. 使用 COUNT(*)  
以下示例计算 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 的雇员总数。
  
```sql
SELECT COUNT(*)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `290`  
  
`(1 row(s) affected)`
  
### <a name="c-using-count-with-other-aggregates"></a>C. 组合使用 COUNT(*) 和其他聚合函数  
以下示例显示可以组合使用 `COUNT(*)` 和选择列表中的其他聚合函数。 该示例使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库。
  
```sql
SELECT COUNT(*), AVG(Bonus)  
FROM Sales.SalesPerson  
WHERE SalesQuota > 25000;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`----------- ---------------------`
  
`14            3472.1428`
  
`(1 row(s) affected)`
  
### <a name="c-using-the-over-clause"></a>C. 使用 OVER 子句  
以下示例将 MIN、MAX、AVG 和 COUNT 函数与 OVER 子句结合使用，以便为 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `HumanResources.Department` 表中的每个部门提供聚合值。
  
```sql
SELECT DISTINCT Name  
       , MIN(Rate) OVER (PARTITION BY edh.DepartmentID) AS MinSalary  
       , MAX(Rate) OVER (PARTITION BY edh.DepartmentID) AS MaxSalary  
       , AVG(Rate) OVER (PARTITION BY edh.DepartmentID) AS AvgSalary  
       ,COUNT(edh.BusinessEntityID) OVER (PARTITION BY edh.DepartmentID) AS EmployeesPerDept  
FROM HumanResources.EmployeePayHistory AS eph  
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
     ON eph.BusinessEntityID = edh.BusinessEntityID  
JOIN HumanResources.Department AS d  
ON d.DepartmentID = edh.DepartmentID
WHERE edh.EndDate IS NULL  
ORDER BY Name;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Name                          MinSalary             MaxSalary             AvgSalary             EmployeesPerDept  
----------------------------- --------------------- --------------------- --------------------- ----------------  
Document Control              10.25                 17.7885               14.3884               5  
Engineering                   32.6923               63.4615               40.1442               6  
Executive                     39.06                 125.50                68.3034               4  
Facilities and Maintenance    9.25                  24.0385               13.0316               7  
Finance                       13.4615               43.2692               23.935                10  
Human Resources               13.9423               27.1394               18.0248               6  
Information Services          27.4038               50.4808               34.1586               10  
Marketing                     13.4615               37.50                 18.4318               11  
Production                    6.50                  84.1346               13.5537               195  
Production Control            8.62                  24.5192               16.7746               8  
Purchasing                    9.86                  30.00                 18.0202               14  
Quality Assurance             10.5769               28.8462               15.4647               6  
Research and Development      40.8654               50.4808               43.6731               4  
Sales                         23.0769               72.1154               29.9719               18  
Shipping and Receiving        9.00                  19.2308               10.8718               6  
Tool Design                   8.62                  29.8462               23.5054               6  
  
(16 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-count-and-distinct"></a>D. 使用 COUNT 和 DISTINCT  
下面的示例列出在特定公司工作的员工可以容纳的不同标题的数目。
  
```sql
USE ssawPDW;  
  
SELECT COUNT(DISTINCT Title)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `67`  
  
### <a name="e-using-count"></a>E. 使用 COUNT(*)  
下面的示例返回中的行总数`dbo.DimEmployee`表。
  
```sql
USE ssawPDW;  
  
SELECT COUNT(*)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-------------`
  
 `296`  
  
### <a name="f-using-count-with-other-aggregates"></a>F. 组合使用 COUNT(*) 和其他聚合函数  
下面的示例结合`COUNT(*)`与选择列表中的其他聚合函数。 查询返回销售代表每年的销售定额数大于 $500,000 和平均的销售配额。
  
```sql
USE ssawPDW;  
  
SELECT COUNT(EmployeeKey) AS TotalCount, AVG(SalesAmountQuota) AS [Average Sales Quota]  
FROM dbo.FactSalesQuota  
WHERE SalesAmountQuota > 500000 AND CalendarYear = 2001;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`TotalCount  Average Sales Quota`
  
`----------  -------------------`
  
`10          683800.0000`
  
### <a name="g-using-count-with-having"></a>G. 使用 HAVING 的计数  
下面的示例使用计数的 HAVING 子句以返回处于已超过 15 个员工的公司部门。
  
```sql
USE ssawPDW;  
  
SELECT DepartmentName,   
       COUNT(EmployeeKey)AS EmployeesInDept  
FROM dbo.DimEmployee  
GROUP BY DepartmentName  
HAVING COUNT(EmployeeKey) > 15;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`DepartmentName  EmployeesInDept`
  
`--------------  ---------------`
  
`Sales           18`
  
`Production      179`
  
### <a name="h-using-count-with-over"></a>H. 使用转移计数  
下面的示例使用计数与 OVER 子句中指定的销售订单的每个返回的包含的产品数目。
  
```sql
USE ssawPDW;  
  
SELECT DISTINCT COUNT(ProductKey) OVER(PARTITION BY SalesOrderNumber) AS ProductCount  
    ,SalesOrderNumber  
FROM dbo.FactInternetSales  
WHERE SalesOrderNumber IN (N'SO53115',N'SO55981');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`ProductCount   SalesOrderID`
  
`------------   -----------------`
  
`3              SO53115`
  
`1              SO55981`
  
## <a name="see-also"></a>另请参阅
[聚合函数 &#40;Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT_BIG &#40;Transact SQL &#41;](../../t-sql/functions/count-big-transact-sql.md)  
[通过子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  


