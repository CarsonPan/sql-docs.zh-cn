---
title: sys.server_event_session_events (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_events
- server_event_session_events_TSQL
- sys.server_event_session_events
- sys.server_event_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_events catalog view
- xe
ms.assetid: 75986e91-1fc7-4f14-98ac-4e90154a74db
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 766d614db7d07c8db5305c32a5e84d71dac53dca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681275"
---
# <a name="sysservereventsessionevents-transact-sql"></a>sys.server_event_session_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对事件会话中的每个事件都返回一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件会话的 ID。 不可为 null。|  
|event_id|**int**|事件的 ID。 此 ID 是在事件会话对象中是唯一的。 不可为 null。|  
|NAME|**sysname**|事件的名称。 不可为 null。|  
|包|**sysname**|包含事件的事件包的名称。 不可为 null。|  
|module|**sysname**|包含事件的模块的名称。 不可为 null。|  
|predicate|**nvarchar(3000)**|应用于事件的谓词表达式。 可以为 Null。|  
|predicate_xml|**nvarchar(3000)**|应用于事件的 XML 谓词表达式。 可以为 Null。|  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="remarks"></a>备注  
 此视图具有下列关系基数。  
  
||||  
|-|-|-|  
|From|若要|关系|  
|sys.server_event_session_events.event_session_id|sys.server_event_sessions.event_session_id|多对一|  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [扩展事件目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
