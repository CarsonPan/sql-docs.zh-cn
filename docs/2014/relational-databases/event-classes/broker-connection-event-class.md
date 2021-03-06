---
title: Broker:Connection 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Connection event class
ms.assetid: d3e505f2-0a43-486f-aa92-9c8e49b2dfea
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22cb73877dcea8fb880d4c565b809990e5ce7123
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52789949"
---
# <a name="brokerconnection-event-class"></a>Broker:Connection 事件类
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成 **Broker:Connection** 事件来报告 Service Broker 管理的传输连接的状态。  
  
## <a name="brokerconnection-event-class-data-columns"></a>Broker:Connection 事件类的数据列  
  
|数据列|类型|Description|列号|可筛选|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|`nvarchar`|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|用户帐户控制|  
|**ClientProcessID**|`int`|由主机分配给正在运行客户端应用程序的进程的 ID。 如果客户端提供了客户端进程 ID，则填充此数据列。|9|用户帐户控制|  
|**DatabaseID**|`int`|由 USE *database* 语句指定的数据库的 ID；如果未对给定实例发出 USE *database*语句，则为默认数据库的 ID。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 数据列而且服务器可用，则 **ServerName** 将显示数据库名。 可使用 **DB_ID** 函数来确定数据库的值。|3|用户帐户控制|  
|**错误**|`int`|事件中文本的 **sys.messages** 的消息 ID 号。 如果此事件报告错误，即是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误号。|31|否|  
|**EventClass**|`int`|捕获的事件类的类型。 对于 **Broker:Connection** 始终为 **138**。|27|否|  
|**EventSequence**|`int`|此事件的序列号。|51|否|  
|**EventSubClass**|`nvarchar`|此连接的连接状态。 对于此事件，子类是以下值之一：<br /><br /> **Connecting**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在启动传输连接。<br /><br /> **Connected**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已建立传输连接。<br /><br /> **Connect Failed**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立传输连接失败。<br /><br /> **Closing**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在关闭传输连接。<br /><br /> **Closed**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已关闭传输连接。<br /><br /> **Accept**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已接受来自另一个实例的传输连接。<br /><br /> **Send IO Error**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在发送消息时遇到了传输错误。<br /><br /> **Receive IO Error**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在接收消息时遇到了传输错误。|21|用户帐户控制|  
|**GUID**|`uniqueidentifier`|此连接的端点 ID。|54|否|  
|**HostName**|`nvarchar`|正在运行客户端程序的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 **HOST_NAME** 函数。|8|用户帐户控制|  
|**IntegerData**|`int`|已关闭此连接的次数。|25|用户帐户控制|  
|**IsSystem**|`int`|指示事件是发生在系统进程中还是发生在用户进程中。<br /><br /> 0 = 用户<br /><br /> 1 = 系统|60|否|  
|**LoginSid**|`image`|已登录用户的安全标识号 (SID)。 服务器中的每个登录名都具有唯一的 SID。|41|用户帐户控制|  
|**NTDomainName**|`nvarchar`|用户所属的 Windows 域。|7|用户帐户控制|  
|**NTUserName**|`nvarchar`|拥有生成此事件的连接的用户的名称。|6|用户帐户控制|  
|**ObjectName**|`nvarchar`|对话的会话句柄。|34|否|  
|**ServerName**|`nvarchar`|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|**SPID**|`int`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为客户端所关联的进程分配的服务器进程 ID。|12|用户帐户控制|  
|**StartTime**|`datetime`|事件（如果有）的开始时间。|14|用户帐户控制|  
|**TextData**|`ntext`|与事件相关的错误消息的文本。 对于不报告错误的事件，此字段为空。 错误消息可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息，也可以是 Windows 错误消息。|1|用户帐户控制|  
|**TransactionID**|`bigint`|系统为事务分配的 ID。|4|否|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
