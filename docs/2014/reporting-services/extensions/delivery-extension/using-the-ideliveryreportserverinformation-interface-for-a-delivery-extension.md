---
title: 将 IDeliveryReportServerInformation 接口用于传递扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d211842a43af771e953fd74a15403ba9321f2860
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027998"
---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>将 IDeliveryReportServerInformation 接口用于传递扩展插件
  <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 接口公开多个属性，您可以使用这些属性来检索有关报表服务器的信息。 您可以使用此信息来传递通知和报表。 当实现传递扩展插件类时，您按照 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 接口的要求实现 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 属性。 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 属性返回一个实现 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 接口的对象。 从该对象，您可以获得报表服务器当前支持的呈现扩展插件的列表。  
  
 以下`for`循环可用于存储中的报表服务器上当前可用的呈现扩展插件的列表**ArrayList**对象。  
  
```vb  
Dim renderFormats As New ArrayList()  
Dim e As Microsoft.ReportingServices.Interfaces.Extension  
For Each e In  ReportServerInformation.RenderingExtension  
   If e.Visible Then  
      renderFormats.Add(e.Name)  
   End If  
Next e  
```  
  
```csharp  
ArrayList renderFormats = new ArrayList();  
foreach (Microsoft.ReportingServices.Interfaces.Extension e in ReportServerInformation.RenderingExtension)  
{   
   if (e.Visible)  
   {  
      renderFormats.Add(e.Name);  
   }  
}  
```  
  
 有关 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 接口的详细信息，请参阅[将 IDeliveryReportServerInformation 接口用于传递扩展插件](using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [实现传递扩展插件](implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
