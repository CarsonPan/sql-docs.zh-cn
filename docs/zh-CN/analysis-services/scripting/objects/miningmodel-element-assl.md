---
title: MiningModel 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MiningModel Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningModel
helpviewer_keywords:
- MiningModel element
ms.assetid: a61d935f-c8f6-457d-ad0c-44f58bb286f5
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: aaebf57375836dfea73863201eada3d7809f147e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="miningmodel-element-assl"></a>MiningModel 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个数据挖掘模型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModels>  
      <MiningModel>  
      <Name>...</Name>  
            <ID>...</ID>  
      <Description>...</<Descrip  
            <Algorithm>...</Algorithm>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <AlgorithmParameters>...</AlgorithmParameters>  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <Translations>...</Translations>  
      <Columns>...</Columns>  
      <State>...</State>  
      <MiningModelPermissions>...</MiningModelPermissions>  
      <Language>...</Language>  
            <Collation>...</Collation>  
            <Annotations>...</Annotations>  
            <ddl100_100:FoldingParameters>   </FoldingParameters>  
   </MiningModel>  
</MiningModels>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModels](../../../analysis-services/scripting/collections/miningmodels-element-assl.md)|  
|子元素|[算法](../../../analysis-services/scripting/properties/algorithm-element-assl.md)， [AlgorithmParameters](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)， [AllowDrillThrough](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[排序规则](../../../analysis-services/scripting/properties/collation-element-assl.md)， [列](../../../analysis-services/scripting/collections/columns-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)，[语言](../../../analysis-services/scripting/properties/language-element-assl.md)， [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [MiningModelPermissions](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[状态](../../../analysis-services/scripting/properties/state-element-assl.md)， [翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)，<br /><br /> [FoldingParameters](../../../analysis-services/scripting/properties/foldingparameters-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 **FoldingParameters**挖掘模型的元素是服务器上，由内部使用，不支持在 DDL 语句中使用。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningModel>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  