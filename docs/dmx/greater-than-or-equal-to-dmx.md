---
title: "&gt;= (大于或等于) (DMX) |Microsoft 文档"
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
dev_langs:
- DMX
helpviewer_keywords:
- '>= (greater than or equal to operator)'
- greater than or equal to (>=)
ms.assetid: a96b7e9c-72dc-4df1-aa41-85aad933df96
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 736cf2361101a9722aa3723c64a04f98fde04b0c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="gt-greater-than-or-equal-to-dmx"></a>&gt;= (大于或等于) (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  执行比较运算，以确定一个数据挖掘扩展插件 (DMX) 表达式的值是否大于等于另一个 DMX 表达式的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
DMX_Expression >= DMX_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *DMX_Expression*  
 一个有效的 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 如果两个参数都为非空值，并且第一个参数的值大于或等于第二个参数的值，则返回包含 TRUE 的布尔值。 如果两个参数都为非空值，并且第一个参数的值小于第二个参数的值，则返回包含 FALSE 的布尔值。 如果其中一个参数的计算结果为空值或这两个参数的计算结果均为空值，则该布尔值包含空值。  
  
## <a name="see-also"></a>另請參閱  
 [比较运算符 &#40; DMX &#41;](../dmx/operators-comparison.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
