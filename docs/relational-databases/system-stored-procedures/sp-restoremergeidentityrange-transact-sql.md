---
title: sp_restoremergeidentityrange (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_restoremergeidentityrange_TSQL
- sp_restoremergeidentityrange
helpviewer_keywords:
- sp_restoremergeidentityrange
ms.assetid: 7923e422-2748-40c0-b5a8-6410c48d5b70
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0576f180809a4432af022d278867d847c8087dd4
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526209"
---
# <a name="sprestoremergeidentityrange-transact-sql"></a>sp_restoremergeidentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此存储过程用于更新标识范围分配。 该存储过程可确保从备份还原发布服务器后，自动标识范围管理运行正常。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_restoremergeidentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是发布的名称。 *发布*是**sysname**，默认值为**所有**。 如果指定了此参数，则只还原该发布的标识范围。  
  
`[ @article = ] 'article'` 是的名称。 *文章*是**sysname**，默认值为**所有**。 如果指定了此参数，则只还原该项目的标识范围。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_restoremergeidentityrange**与合并复制一起使用。  
  
 **sp_restoremergeidentityrange**获取最大标识范围分配信息从分发服务器并更新中的值**max_used**的列[MSmerge_identity_range_allocations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-identity-range-allocations-transact-sql.md)使用自动标识范围管理的项目。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_restoremergeidentityrange**。  
  
## <a name="see-also"></a>请参阅  
 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
