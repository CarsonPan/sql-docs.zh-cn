---
title: 优化属性的动态 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3512f1a63ae92ce75990f63caabf80a83099c149
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="optimize-property-dynamic-ado"></a>优化属性的动态 (ADO)
指定是否应在创建索引[字段](../../../ado/reference/ado-api/field-object.md)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**布尔**值，该值指示是否应创建索引。  
  
## <a name="remarks"></a>注释  
 索引可以提高查找或排序中的值的操作的性能[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 索引是内部 ADO;显式无法访问，或在你的应用程序中使用它。  
  
 若要创建索引的字段上时，将设置**优化**属性**True**。 若要删除索引，请将此属性设置为**False**。  
  
 **优化**动态属性追加到[字段](../../../ado/reference/ado-api/field-object.md)对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
## <a name="usage"></a>用法  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [优化属性示例 (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [优化属性示例 （VC + +）](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [筛选器属性](../../../ado/reference/ado-api/filter-property.md)   
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Sort 属性](../../../ado/reference/ado-api/sort-property.md)