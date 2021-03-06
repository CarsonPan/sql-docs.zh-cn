---
title: sp_updateextendedproperty (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updateextendedproperty_TSQL
- sp_updateextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updateextendedproperty
ms.assetid: 7f02360f-cb9e-48b4-b75f-29b4bc9ea304
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 347e8d170006cb289b421171851140b18e64f14b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47843845"
---
# <a name="spupdateextendedproperty-transact-sql"></a>sp_updateextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  更新现有扩展属性的值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_updateextendedproperty  
    [ @name = ]{ 'property_name' }   
    [ , [ @value = ]{ 'value' }  
        [, [ @level0type = ]{ 'level0_object_type' }  
         , [ @level0name = ]{ 'level0_object_name' }  
              [, [ @level1type = ]{ 'level1_object_type' }  
               , [ @level1name = ]{ 'level1_object_name' }  
                     [, [ @level2type = ]{ 'level2_object_type' }  
                      , [ @level2name = ]{ 'level2_object_name' }  
                     ]  
              ]  
        ]  
    ]  
```  
  
## <a name="arguments"></a>参数  
 [ @name=] {'*property_name*}  
 要更新的属性的名称。 *property_name*是**sysname**，且不能为 NULL。  
  
 [ @value=] {'*值*}  
 与属性关联的值。 *值*是**sql_variant**，默认值为 NULL。 大小*值*可能超过 7500 个字节。  
  
 [ @level0type=] {'*level0_object_type*}  
 用户或用户定义类型。 *level0_object_type*是**varchar （128)**，默认值为 NULL。 有效输入包括程序集、 协定、 事件通知、 文件组、 消息类型、 分区函数、 分区方案，计划指南、 REMOTE SERVICE BINDING、 路由、 架构、 服务、 用户、 触发器、 类型和为 NULL。  
  
> [!IMPORTANT]  
>  作为级别 0 类型的 USER 和 TYPE 将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中删除。 请避免在新的开发工作中使用这些功能，并考虑修改当前使用这些功能的应用程序。 改用 SCHEMA 替代 USER 作为级别 0 类型。 对于 TYPE，请使用 SCHEMA 作为级别 0 类型，使用 TYPE 作为级别 1 类型。  
  
 [ @level0name=] {'*level0_object_name*}  
 所指定的级别 1 对象类型的名称。 *level0_object_name*是**sysname**默认值为 NULL。  
  
 [ @level1type=] {'*level1_object_type*}  
 级别 1 对象的类型。 *level1_object_type*是**varchar （128)** 默认值为 NULL。 有效的输入包括：AGGREGATE、DEFAULT、FUNCTION、LOGICAL FILE NAME、PROCEDURE、QUEUE、RULE、SYNONYM、TABLE、TABLE_TYPE、TYPE、VIEW、XML SCHEMA COLLECTION 和 NULL。  
  
 [ @level1name=] {'*level1_object_name*}  
 所指定的级别 1 对象类型的名称。 *level1_object_name*是**sysname**默认值为 NULL。  
  
 [ @level2type=] {'*level2_object_type*}  
 级别 2 对象的类型。 *level2_object_type*是**varchar （128)** 默认值为 NULL。 有效的输入包括：COLUMN、CONSTRAINT、EVENT NOTIFICATION、INDEX、PARAMETER、TRIGGER 和 NULL。  
  
 [ @level2name=] {'*level2_object_name*}  
 所指定的级别 2 对象类型的名称。 *level2_object_name*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 为了指定扩展属性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的对象分为三个级别（0、1、2）。 级别 0 是最高级别，定义为包含在数据库范围内的对象。 级别 1 的对象包含在架构作用域或用户作用域中，而级别 2 的对象包含在级别 1 对象中。 可以为这些级别中任一级别的对象定义扩展属性。 引用某个级别中的对象必须用拥有或包含它们的更高级别对象的名称进行限制。  
  
 给定一个有效*property_name*并*值*，如果所有对象类型和名称都均为 null，更新的属性属于当前数据库。  
  
## <a name="permissions"></a>Permissions  
 db_owner 和 db_ddladmin 固定数据库角色的成员可以更新任何对象的扩展属性，但以下情况例外：db_ddladmin 不能向数据库本身添加属性，也不能向用户或角色中添加属性。  
  
 用户可以更新其拥有的对象的扩展属性，也可更新其拥有 ALTER 或 CONTROL 权限的扩展属性。  
  
## <a name="examples"></a>示例  
  
### <a name="a-updating-an-extended-property-on-a-column"></a>A. 对列更新扩展属性  
 以下示例对 `Caption` 表的 `ID` 列更新 `T1` 属性的值。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
    @name = N'Caption'  
    ,@value = N'Employee ID'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
--Update the extended property.  
EXEC sp_updateextendedproperty   
    @name = N'Caption'  
    ,@value = 'Employee ID must be unique.'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
```  
  
### <a name="b-updating-an-extended-property-on-a-database"></a>B. 对数据库更新扩展属性  
 以下示例将先对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库创建扩展属性，然后更新该属性的值。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample OLTP Database';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_updateextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample Database';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.fn_listextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
