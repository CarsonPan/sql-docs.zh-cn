---
title: "模式元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Mode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57c3450e8928b24dc03e2d5915983f39330d0b0c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mode-element-xmla"></a>Mode 元素 (XMLA)
  标识要使用由容器的父模式[锁](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)元素在指定的对象上创建锁时。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[锁定](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)，[解锁](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 父**锁**元素使用**模式**元素来确定的锁的对象创建的类型。 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*CommitShared*|对指定对象建立一个共享锁。 还可以为同一对象创建其他共享锁。<br /><br /> 共享的锁可防止事务包含写入操作，如[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用运行[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)命令，对指定的对象，从提交之前删除的共享的锁。 共享的锁不会阻止事务包含读取的操作，如[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法调用或**执行**方法调用运行[语句](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)命令，从正在提交。|  
|*CommitExclusive*|对指定对象建立一个排他锁。 不可为同一对象创建其他共享锁或排他锁。<br /><br /> 排他锁可阻止指定对象的包含写或读操作的事务的提交，阻止会一直持续到该排他锁被删除为止。|  
  
## <a name="see-also"></a>另请参阅  
 [ID 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Object 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  