---
title: STConvexHull（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STConvexHull (geometry Data Type)
- STConvexHull_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull (geometry Data Type)
ms.assetid: 60a520a6-1a7c-486b-8d91-34401edf6233
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a97b0f6fc8ad1264c146efd3dd0de9751788093e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690245"
---
# <a name="stconvexhull-geometry-data-type"></a>STConvexHull（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回表示 geometry 实例的凸包的对象。
  
## <a name="syntax"></a>语法  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry  
  
 CLR 返回类型：SqlGeometry  
  
## <a name="remarks"></a>Remarks  
 `STConvexHull()` 返回包含给定 geometry 实例的最小凸多边形。 Points 或共线 LineString 实例将生成与该输入具有相同类型的实例。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STConvexHull()` 查找非凸 `Polygon``geometry` 实例的凸包。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 1 1, 2 2, 2 0, 0 0))', 0);  
SELECT @g.STConvexHull().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

