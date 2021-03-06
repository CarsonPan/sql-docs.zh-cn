---
title: WMI 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5d57a0783c8af0121169f09622b8e5bd8547d1ad
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386015"
---
# <a name="wmi-connection-manager"></a>WMI 连接管理器
  WMI 连接管理器使得包可以使用 Windows Management Instrumentation (WMI) 来管理企业环境中的信息。  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 Web 服务任务使用 WMI 连接管理器。  
  
 当将 WMI 连接管理器添加到包中，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建的连接管理器将解析为在运行时的 WMI 连接，设置该连接管理器属性，并将对该连接管理器`Connections`集合. 该连接管理器的 `ConnectionManagerType` 属性设置为 `WMI`。  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>配置 WMI 连接管理器  
 可按下列方式配置 WMI 连接管理器：  
  
-   指定服务器名称。  
  
-   指定服务器上的命名空间。  
  
-   为连接到服务器选择身份验证模式。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请参阅 [WMI 连接管理器编辑器](../wmi-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="see-also"></a>请参阅  
 [Web 服务任务](../control-flow/web-service-task.md)   
 [Integration Services (SSIS) 连接](integration-services-ssis-connections.md)  
  
  
