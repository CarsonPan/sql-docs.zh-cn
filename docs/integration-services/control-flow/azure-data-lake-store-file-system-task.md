---
title: "Azure 数据湖存储文件系统任务 |Microsoft 文档"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 303d3b74da3fe370d19b7602c0e11e67b63191e7
ms.openlocfilehash: ce2355de312faed9ab66991d6d0dd344ff315a55
ms.contentlocale: zh-cn
ms.lasthandoff: 08/29/2017

---
# <a name="azure-data-lake-store-file-system-task"></a>Azure 数据湖存储文件系统任务

**Azure 数据湖存储文件系统任务**使用户能够执行各种文件系统操作[Azure 数据湖存储 (ADLS)](https://azure.microsoft.com/services/data-lake-store/)。

**Azure 数据湖存储文件系统任务**的组成部分[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

若要添加到包的 Azure 数据湖存储文件系统任务，将它从 SSIS 工具箱拖到设计器画布中。 然后双击该任务，或右键单击该任务并选择**编辑**，若要打开任务编辑器对话框。

**操作**属性指定要执行的文件系统操作。 支持以下操作。

* **CopyToADLS:**将文件上载到 ADLS。
* **CopyFromADLS:**从 ADLS 下载文件。

对于任何操作，你必须指定一个 Azure 数据湖连接管理器。

以下是特定于每个操作的属性的说明。

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:**指定包含要上载的文件的源目录。
* **FileNamePattern:**指定源文件的文件名称筛选器。 只有其名称与指定的模式匹配的文件将会上载。 通配符`*`和`?`支持。
* **SearchRecursively:**指定是否要上载的文件的源目录中进行递归搜索。
* **AzureDataLakeDirectory:**指定要将文件上载到的 ADLS 目标目录。
* **FileExpiry:**指定过期日期和时间的文件上载到 ADLS，或将此属性留空以指示文件永不过期。

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory:**指定包含要下载的文件的 ADLS 源目录。
* **SearchRecursively:**指定是否搜索以递归方式中下载的文件的源目录。
* **LocalDirectory:**指定要存储已下载的文件的目标目录。