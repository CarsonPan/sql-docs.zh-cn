---
title: sp_help_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_operator
- sp_help_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_operator
ms.assetid: caedc43d-44b8-415a-897e-92923f6de3b8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 48d70126d071879754011fed7342d03dd72185a5
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534379"
---
# <a name="sphelpoperator-transact-sql"></a>sp_help_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告有关为服务器定义的操作员的信息。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## <a name="arguments"></a>参数  
`[ @operator_name = ] 'operator_name'` 运算符名称。 *operator_name*是**sysname**。 如果*operator_name*是未指定，则返回有关所有运算符的信息。  
  
`[ @operator_id = ] operator_id` 为其请求信息的操作员的标识号。 *operator_id*是**int**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*operator_id*或*operator_name*必须指定，但不能同时指定两者。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|操作员标识号。|  
|**名称**|**sysname**|运算符名称。|  
|**enabled**|**tinyint**|操作员可以接收到任何通知：<br /><br /> 1 = 是<br /><br /> 0 = 否|  
|**email_address**|**nvarchar(100)**|操作员电子邮件地址。|  
|**last_email_date**|**int**|上次用电子邮件通知操作员的日期。|  
|**last_email_time**|**int**|上一次用电子邮件通知操作员的时间。|  
|**pager_address**|**nvarchar(100)**|操作员寻呼地址。|  
|**last_pager_date**|**int**|上一次通过寻呼通知操作员的日期。|  
|**last_pager_time**|**int**|上一次通过寻呼通知操作员的时间。|  
|**weekday_pager_start_time**|**int**|某一时间段的起始时间，在工作日的该时间段内操作员可以接收到寻呼通知。|  
|**weekday_pager_end_time**|**int**|某一时间段的结束时间，在工作日的该时间段内操作员可以接收到寻呼通知。|  
|**saturday_pager_start_time**|**int**|某一时间段的起始时间，在星期六的该时间段内操作员可以接收到寻呼通知。|  
|**saturday_pager_end_time**|**int**|某一时间段的结束时间，在星期六的该时间段内操作员可以接收到寻呼通知。|  
|**sunday_pager_start_time**|**int**|某一时间段的起始时间，在星期日的该时间段内操作员可以接收到寻呼通知。|  
|**sunday_pager_end_time**|**int**|某一时间段的结束时间，在星期日的该时间段内操作员可以接收到寻呼通知。|  
|**pager_days**|**tinyint**|一个位掩码 (**1** = 星期日， **64** = 星期六) 的指示操作员可以接收寻呼通知的天的周。|  
|**netsend_address**|**nvarchar(100)**|接收网络弹出通知的操作员地址。|  
|**last_netsend_date**|**int**|上一次用网络弹出消息通知操作员的日期。|  
|**last_netsend_time**|**int**|上一次用网络弹出消息通知操作员的时间。|  
|**category_name**|**sysname**|该操作员所属的操作员分类的名称。|  
  
## <a name="remarks"></a>备注  
 **sp_help_operator**必须从运行**msdb**数据库。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="examples"></a>示例  
 以下示例报告有关操作员 `François Ajenstat` 的信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_operator  
    @operator_name = N'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
