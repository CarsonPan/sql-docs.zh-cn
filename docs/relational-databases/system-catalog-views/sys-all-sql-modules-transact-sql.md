---
title: sys.all_sql_modules (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- all_sql_modules_TSQL
- sys.all_sql_modules
- all_sql_modules
- sys.all_sql_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_sql_modules catalog view
ms.assetid: 7477a3fe-afb3-44c8-bb2c-c6e1d9bdee6f
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b5b9f84f432a0861483066f3367556b5afc1f9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684141"
---
# <a name="sysallsqlmodules-transact-sql"></a>sys.all_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回的联合**sys.sql_modules**并**sys.system_sql_modules**。  
  
 该视图返回每个本机编译的标量用户定义的函数的行。 有关详细信息，请参阅[内存中 OLTP 的标量用户定义函数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|包含对象的对象 ID。 是在数据库中唯一。|  
|**定义**|**nvarchar(max)**|定义此模块的 SQL 文本。<br /><br /> NULL = 已加密|  
|**uses_ansi_nulls**|**bit**|模块是使用 SET ANSI_NULLS ON 创建的。|  
|**uses_quoted_identifier**|**bit**|模块是使用 SET QUOTED_IDENTIFIER ON 创建的。|  
|**is_schema_bound**|**bit**|模块是使用 SCHEMABINDING 选项创建的。|  
|**uses_database_collation**|**bit**|1 = 架构绑定模块定义取决于正确处理所需的数据库的默认排序规则；否则为 0。 此种依赖关系可防止更改数据库的默认排序规则。|  
|**is_recompiled**|**bit**|过程是使用 WITH RECOMPILE 选项创建的。|  
|**null_on_null_input**|**bit**|模块被声明为针对任何 NULL 输入生成 NULL 输出。|  
|**execute_as_principal_id**|**int**|EXECUTE AS 数据库主体的 ID。<br /><br /> 默认情况下，或者 EXECUTE AS CALLER 时，为 NULL。<br /><br /> 指定主体 if ID EXECUTE AS SELF 或 EXECUTE AS\<主体 >。<br /><br /> -2 = EXECUTE AS OWNER。|  
|**uses_native_compilation**|bit|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 0 = 非本机编译<br /><br /> 1 = 本机编译<br /><br /> 默认值为 0。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.system_sql_modules &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-sql-modules-transact-sql.md)   
 [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
