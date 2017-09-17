---
title: "STCurveToLine (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STCurveToLine_TSQL
- STCurveToLine
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geography)
ms.assetid: 2f863a85-6168-465a-b32f-bb5e3de58dee
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9d2ad93d8bc292ebb86233917dc3f934fbe57dca
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回多边形的近似**geography**包含条圆弧线段实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STCurveToLine()  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 返回**LineString**实例**CircularString**或**CompoundCurve**实例。  
  
 返回**多边形**实例**CurvePolygon**实例。  
  
 返回一份**geography**不包含的实例**CircularString**， **CompoundCurve**，或**CurvePolygon**实例。  
  
 与不同的是 SQL MM 规范中，此方法不使用在计算的多边形近似的 z 坐标值。 调用中存在任何 z 坐标值**geography**实例将被忽略。  
  
## <a name="examples"></a>示例  
 以下示例返回作为 `LineString` 实例的多边形近似值的 `CircularString` 实例。  
  
 `DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';`  
  
 `DECLARE @g2 geography;`  
  
 `SET @g2 = @g1.STCurveToLine();`  
  
 `SELECT @g1.STNumPoints() AS G1, @g2.STNumPoints() AS G2;`  
  
## <a name="see-also"></a>另请参阅  
 [STLength &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)   
 [STNumPoints &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)   
 [空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  