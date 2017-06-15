---
title: "如何： 部署自定义报表项 |Microsoft 文档"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
caps.latest.revision: 26
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ab5f90df0ff1d3c91a641811e54bf4394506c2a4
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="how-to-deploy-a-custom-report-item"></a>如何部署自定义报表项
  若要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中部署自定义报表项，必须修改报表服务器配置文件，并将设计时和运行时组件程序集复制到报表设计器和报表服务器的相应应用程序文件夹中。  
  
### <a name="to-deploy-a-custom-report-item"></a>部署自定义报表项  
  
1.  编辑 Rsreportdesigner.config 文件，以配置供在相应设计器中使用的自定义报表项运行时组件和设计时组件。 请注意， **ReportItemName**条目必须匹配**CustomReportItemAttribute**属性中使用你**CustomReportItemDesigner**类。 例如：  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    <ReportItemDesigner>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsDesigner, PolygonsDesigner" />  
    </ReportItemDesigner>  
    <ReportItemConverter>  
       <Converter Source="Chart" Target="Polygons" Type="PolygonsCRI.PolygonsConverter, PolygonsDesigner" />  
    </ReportItemConverter>  
    ```  
  
2.  编辑 Rsreportserver.config 文件以注册自定义报表项运行时组件。 例如：  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  编辑 Rsssrvpolicy.config 文件以添加**CodeGroup**授予了自定义报表项的适当权限。 例如：  
  
    ```  
    <CodeGroup   
       class="UnionCodeGroup"   
       version="1"   
       PermissionSetName="FullTrust"  
       Description="This code group grants MyCustomReportItem.dll FullTrust permission. ">  
       <IMembershipCondition   
          class="UrlMembershipCondition"  
          version="1"  
       Url="C:\Program Files\Microsoft SQL Server\ MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin\MyCustomReportItem.dll" />  
    </CodeGroup>  
    ```  
  
4.  将相应自定义报表项运行时组件 DLL 复制到 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies 和 \Program Files\Microsoft SQL Server\MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin 目录下。  
  
5.  将相应自定义报表项设计时组件 DLL 复制到 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies 目录下。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置文件](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [自定义报表项类库](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  