---
title: SQL Server XTP IO 调控器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 4f849d6c282fda16709b556131e44dd1ce9cd5ce
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380188"
---
# <a name="sql-server-xtp-io-governor"></a>SQL Server XTP IO 调控器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server XTP IO 调控器性能对象包含与内存中 OLTP IO 速率调控器相关的计数器。

下表介绍了 **SQL Server XTP IO 调控器** 计数器。

|计数器|描述|  
|-------------|-----------------|  
|**信用不足等待数/秒**|由于速率对象中没有足够的信用而引起的等待次数（每秒）。|
|**发出的 IO 数/秒**|每秒由刷新线程发出的 IO 数。|
|**日志块数/秒**|每秒由控制器处理的日志块数。|
|**丢失的信用槽数**|由于等待速率对象中的信用而丢失的信用槽的数量。|
|**陈旧速率对象等待数/秒**|由于陈旧速率对象引起的等待的次数（每秒）。|
|**已发布对象的总速率**|已发布对象的速率总数。|
 

## <a name="see-also"></a>另请参阅  
[SQL Server XTP（内存中 OLTP）性能计数器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
