---
title: “筛选器”对话框 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b987b141-5abf-4161-a073-4cfc3e7f5aae
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e18dbbd921fc4acfd75e61bbf402b754a22d22d3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52784589"
---
# <a name="filter-dialog-box-mds-add-in-for-excel"></a>“筛选器”对话框（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，使用“筛选器”  对话框可以先筛选 MDS 管理的数据列表，然后再将其加载到 Excel 中。  
  
 此对话框包含三个部分：**列**，**行**，和**摘要**。  
  
## <a name="columns"></a>“列”  
 使用“列”  部分可以确定要在 Excel 中显示的属性（列）。  
  
|控件名称|Description|  
|------------------|-----------------|  
|属性类型|属性类型描述您想要使用的成员的类型。 在大多数情况下，类型为 **“叶”**。 有关成员类型的详细信息，请参阅[成员 (Master Data Services)](../members-master-data-services.md)。|  
|显式层次结构|如果您选择 **“已合并”** 属性类型，请选择已合并成员所属的层次结构。 有关详细信息，请参阅[显式层次结构 (Master Data Services)](../explicit-hierarchies-master-data-services.md)。|  
|属性组|属性组是对属性子集进行分组的方式。 如果您想要显示可用属性的子集，请选择属性组。 有关属性组的详细信息，请参阅[属性组 (Master Data Services)](../attribute-groups-master-data-services.md)。|  
|全选|单击此选项可选择列表中显示的所有属性。|  
|全部清除|单击此选项可清除列表中显示的选定属性。<br /><br /> 注意：您不能清除 **Name** 和 **Code**。|  
|向上键|单击此选项可在列表中向上移动所选属性。 从上到下的顺序对应于列在工作表中从左到右的显示顺序。|  
|向下键|单击此选项可在列表中向下移动所选的属性。 从上到下的顺序对应于列在工作表中从左到右的显示顺序。|  
  
## <a name="rows"></a>“行”  
 使用“行”  部分可以确定要在 Excel 中显示的成员（行）。 通过定义要显示的行的筛选条件可以确定要显示的行。  
  
|控件名称|Description|  
|------------------|-----------------|  
|Attribute|显示筛选所依据的属性。 如果未列出任何属性，这是因为尚未添加任何属性。<br /><br /> 注意：您可以通过不打算在工作表中显示的属性进行筛选。|  
|运算符|显示对应于所选属性的类型的运算符。 有关详细信息，请参阅 [Filter 运算符 (Master Data Services)](../filter-operators-master-data-services.md)。|  
|条件|筛选要依据的条件。|  
|更新摘要|处理大型数据集时，单击该选项可使用要加载的数据的详细信息来更新 **“摘要”** 部分。|  
|添加|在您单击 **“列”** 部分中的属性，然后单击 **“添加”** 后，将向筛选器列表添加属性。|  
|全部删除|从列表中删除所有筛选器。|  
|删除|从列表中删除所选的筛选器。|  
  
## <a name="summary"></a>“摘要”  
 使用 **“摘要”** 部分可以在加载数据之前先查看有关要加载的数据的详细信息。  
  
|控件名称|Description|  
|------------------|-----------------|  
|“模型”|模型的名称。|  
|版本|版本的名称。|  
|实体|实体的名称。|  
|“行”|基于在 **“行”** 部分中应用的筛选器要加载到 Excel 中的行数。|  
|“列”|基于在 **“列”** 部分中所选的属性要加载到 Excel 中的列数。|  
  
## <a name="see-also"></a>请参阅  
 [加载前筛选数据&#40;MDS add-in for Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)   
 [加载数据&#40;MDS add-in for Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
