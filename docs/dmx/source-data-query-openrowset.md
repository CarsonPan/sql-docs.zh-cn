---
title: "OPENROWSET (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENROWSET
dev_langs:
- DMX
helpviewer_keywords:
- OPENROWSET statement
ms.assetid: 8c8b61b4-2bf6-46c7-8976-51484004dc22
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 914e1be70255414373fd758301ef0682f3aba6e7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;源数据查询&gt;-OPENROWSET
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用对外部访问接口的查询替换源数据查询。 插入、 选择从 PREDICTION JOIN，和选择从 NATURAL PREDICTION JOIN 语句支持**OPENROWSET**。  
  
## <a name="syntax"></a>語法  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>参数  
 *provider_name*  
 OLE DB 访问接口名称。  
  
 *provider_string*  
 用于指定的访问接口的 OLE DB 连接字符串。   
  
 *query_syntax*  
 一个返回行集的查询语法。  
  
## <a name="remarks"></a>注释  
 数据挖掘提供程序将通过使用建立到数据源对象的连接*provider_name*和*provider_string* ，会执行中指定的查询*query_syntax*源数据中检索行集。  
  
## <a name="examples"></a>示例  
 以下示例可用于 PREDICTION JOIN 语句中，通过使用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] SELECT 语句检索 [!INCLUDE[tsql](../includes/tsql-md.md)] 数据库中的数据。  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#60; 源数据查询 &#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
