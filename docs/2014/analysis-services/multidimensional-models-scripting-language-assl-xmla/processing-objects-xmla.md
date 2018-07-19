---
title: 处理对象 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
- writeback [Analysis Services], XML for Analysis
- out-of-line bindings
- processing objects [XML for Analysis]
- XMLA, objects
ms.assetid: a65b3249-303d-49c6-98af-6ac6eed11a03
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce70d5d9168d1158b98453553b2323afc8da8e11
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306507"
---
# <a name="processing-objects-xmla"></a>处理对象 (XMLA)
  在中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 处理指的是或系列的指导的数据转换为业务分析的信息。 处理因对象类型而异，但处理始终是将数据转换为信息的一个环节。  
  
 到进程[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象，可以使用[进程](../xmla/xml-elements-commands/process-element-xmla.md)命令。 `Process` 命令可以对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例处理以下对象：  
  
-   多维数据集  
  
-   “数据库”  
  
-   维度  
  
-   度量值组  
  
-   挖掘模型  
  
-   挖掘结构  
  
-   “度量值组”  
  
 为了控制对象的处理，`Process` 命令有多个可设置的属性。 `Process` 命令的属性可以控制以下方面：处理的程度、处理的对象、是否使用外部绑定、如何处理错误以及如何管理写回表。  
  
## <a name="specifying-processing-options"></a>指定处理选项  
 [类型](../xmla/xml-elements-properties/type-element-xmla.md)属性的`Process`命令指定处理对象时要使用的处理选项。 有关处理选项的详细信息，请参阅[处理选项和设置 (Analysis Services)](../multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
 下表列出了 `Type` 属性的各个常量以及使用每一常量时可处理的不同对象。  
  
|`Type` 值|适用对象|  
|--------------------|------------------------|  
|*ProcessFull*|多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区|  
|*ProcessAdd*|维度和分区|  
|*ProcessUpdate*|维度|  
|*ProcessIndexes*|维度、多维数据集、度量值组和分区|  
|*ProcessData*|维度、多维数据集、度量值组和分区|  
|*ProcessDefault*|多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区|  
|*ProcessClear*|多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区|  
|*ProcessStructure*|多维数据集和挖掘结构|  
|*ProcessClearStructureOnly*|挖掘结构|  
|*ProcessScriptCache*|多维数据集|  
  
 有关处理的详细信息[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象，请参阅[多维模型对象处理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
## <a name="specifying-objects-to-be-processed"></a>指定要处理的对象  
 [对象](../xmla/xml-elements-properties/object-element-xmla.md)属性的`Process`命令包含要处理的对象的对象标识符。 在 `Process` 命令中仅可指定一个对象，但是在处理一个对象的同时会处理其所有子对象。 例如，在处理多维数据集中的一个度量值组时会处理该度量值组的所有分区；在处理一个数据库时会处理该数据库所包含的所有对象，包括多维数据集、维度和挖掘结构。  
  
 如果将 `ProcessAffectedObjects` 命令的 `Process` 属性设置为 true，则处理指定对象时所影响的所有相关对象都会得到处理。 例如，如果通过使用增量更新维度*ProcessUpdate*处理中的选项`Process`命令时，其聚合失效由于成员的添加或删除任何分区也是通过处理[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]如果`ProcessAffectedObjects`设置为 true。 在这种情况下，单个 `Process` 命令可以处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的多个对象，但是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会确定除 `Process` 命令中指定的单个对象外，哪些对象也必须加以处理。  
  
 不过，在 `Process` 命令中使用多个 `Batch` 命令可以同时处理多个对象，如多个维度。 与使用 `ProcessAffectedObjects` 属性相比，批处理操作可为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上对象的串行或并行处理提供更为精确的控制，从而为较大的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库提供更好的处理方法。 有关执行批处理操作的详细信息，请参阅[执行批处理操作&#40;XMLA&#41;](performing-batch-operations-xmla.md)。  
  
## <a name="specifying-out-of-line-bindings"></a>指定外部绑定  
 如果`Process`不包含命令`Batch`命令，可以选择指定中的外部绑定[绑定](../xmla/xml-elements-properties/bindings-element-xmla.md)，[数据源](../xmla/xml-elements-properties/source-element-xmla.md)，和[DataSourceView](../xmla/xml-elements-properties/datasourceview-element-xmla.md)的属性`Process`命令要处理的对象。 外部绑定是对数据源、数据源视图和其他对象的引用（在这些数据源、数据源视图和对象中，该绑定仅在执行 `Process` 命令时存在），并会覆盖与所处理对象关联的所有现有绑定。 如果未指定外部绑定，则使用当前与要处理的对象关联的绑定。  
  
 外部绑定用在以下情况下：  
  
-   增量处理一个分区，其中必须指定另一个事实数据表或现有事实数据表上的一个筛选器以确保不会对行进行两次计数。  
  
-   使用在数据流任务[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]处理维度、 挖掘模型或分区时提供数据。  
  
 外部绑定属于 Analysis Services 脚本语言 (ASSL) 的一部分。 有关 ASSL 中的外部绑定的详细信息，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
### <a name="incrementally-updating-partitions"></a>增量更新分区  
 增量更新已处理的分区时通常需要外部绑定，原因在于为该分区指定的绑定会引用已在该分区中聚合的事实数据表数据。 使用 `Process` 命令增量更新已处理的分区时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会执行以下操作：  
  
-   创建一个与要增量更新的分区具有相同结构的临时分区。  
  
-   使用 `Process` 命令中指定的外部绑定处理该临时分区。  
  
-   将该临时分区与所选现有分区合并。  
  
 有关合并分区使用 XML for Analysis (XMLA) 的详细信息，请参阅[合并分区&#40;XMLA&#41;](merging-partitions-xmla.md)。  
  
## <a name="handling-processing-errors"></a>对处理错误进行处理  
 [ErrorConfiguration](../xmla/xml-elements-properties/errorconfiguration-element-xmla.md)属性的`Process`命令可用于指定如何处理处理对象过程中遇到的错误。 例如，在处理维度时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在键属性的键列中遇到重复的值。 因为属性键必须是唯一的，因此 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 丢弃重复的记录。 基于[KeyDuplicate](../scripting/properties/keyduplicate-element-assl.md)的属性`ErrorConfiguration`，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可以：  
  
-   忽略错误并继续处理该维度。  
  
-   返回说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 遇到了重复键的消息并继续处理。  
  
 `ErrorConfiguration` 可为执行 `Process` 命令过程中遇到的许多类似情况提供各种选项。  
  
## <a name="managing-writeback-tables"></a>管理写回表  
 如果 `Process` 命令遇到一个可写入的分区或者此类分区的多维数据集或度量值组，而且是未完整处理的，则该分区的写回表可能不存在。 [WritebackTableCreation](../xmla/xml-elements-properties/writebacktablecreation-element-xmla.md)的属性`Process`命令将确定是否[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]应创建写回表。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>Description  
 下面的示例对 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 示例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库进行完整处理。  
  
### <a name="code"></a>代码  
  
```  
<Process xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Description  
 下面的示例以增量方式处理**Internet_Sales_2004**分区中**Internet Sales**度量值组**Adventure Works DW** 中的多维数据集[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]示例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 `Process`命令订单日期晚于 2006 年 12 月 31 日使用添加到该分区中的一个扩展的行的查询绑定`Bindings`属性的`Process`命令以检索从中生成的事实表行若要添加到该分区的聚合。  
  
### <a name="code"></a>代码  
  
```  
<Process ProcessAffectedObjects="true" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2006</PartitionID>  
  </Object>  
  <Bindings>  
    <Binding>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2006</PartitionID>  
      <Source xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="QueryBinding">  
        <DataSourceID>Adventure Works DW</DataSourceID>  
        <QueryDefinition>  
          SELECT  
            [dbo].[FactInternetSales].[ProductKey],  
            [dbo].[FactInternetSales].[OrderDateKey],  
            [dbo].[FactInternetSales].[DueDateKey],  
            [dbo].[FactInternetSales].[ShipDateKey],   
            [dbo].[FactInternetSales].[CustomerKey],   
            [dbo].[FactInternetSales].[PromotionKey],  
            [dbo].[FactInternetSales].[CurrencyKey],  
            [dbo].[FactInternetSales].[SalesTerritoryKey],  
            [dbo].[FactInternetSales].[SalesOrderNumber],  
            [dbo].[FactInternetSales].[SalesOrderLineNumber],  
            [dbo].[FactInternetSales].[RevisionNumber],  
            [dbo].[FactInternetSales].[OrderQuantity],  
            [dbo].[FactInternetSales].[UnitPrice],  
            [dbo].[FactInternetSales].[ExtendedAmount],  
            [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
            [dbo].[FactInternetSales].[DiscountAmount],  
            [dbo].[FactInternetSales].[ProductStandardCost],  
            [dbo].[FactInternetSales].[TotalProductCost],  
            [dbo].[FactInternetSales].[SalesAmount],  
            [dbo].[FactInternetSales].[TaxAmt],  
            [dbo].[FactInternetSales].[Freight],  
            [dbo].[FactInternetSales].[CarrierTrackingNumber],  
            [dbo].[FactInternetSales].[CustomerPONumber]  
          FROM [dbo].[FactInternetSales]  
          WHERE OrderDateKey > '1280'  
        </QueryDefinition>  
      </Source>  
    </Binding>  
  </Bindings>  
  <Type>ProcessAdd</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
  