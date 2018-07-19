---
title: 升级 SQL Server 管理工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- management tools, upgrading
ms.assetid: 1dab50b9-d16c-49a1-9ecc-af72adb6c378
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2895efa338745f8935674ff42620c1f8d6272652
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289406"
---
# <a name="upgrade-sql-server-management-tools"></a>升级 SQL Server 管理工具
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本进行升级。 本主题介绍对升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具和管理组件（如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理、数据库邮件、维护计划、XPStar 和 XPWeb）的支持及其行为。  
  
> [!IMPORTANT]  
>  对于本地安装，必须以管理员身份运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。 如果从远程共享位置运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序，必须使用对该远程共享位置具有读取和执行权限的域帐户。  
  
## <a name="known-upgrade-issues"></a>已知升级问题  
 在升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之前，请考虑以下问题：  
  
### <a name="for-all-upgrade-scenarios"></a>对于所有升级方案：  
  
-   在升级 MSX 服务器之前，应先对所有 TSX 服务器进行升级。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的 MSX/TSX 的详细信息，请参阅 [企业范围的自动化管理](../../ssms/agent/automated-administration-across-an-enterprise.md)。  
  
-   必须同时升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的所有组件。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件的版本号在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例中必须相同。  
  
-   在升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时可以向 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的现有安装添加组件。 有关详细信息，请参阅[升级到使用 SQL Server 2014 安装向导&#40;安装程序&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端工具（如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问、sqlcmd 和 osql）不升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 相反，客户端工具与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本中的工具并行运行。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持从早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端工具导入设置。  
  
-   在升级期间，从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的身份验证将从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证更新为 Windows 身份验证。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支持 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
-   在升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的过程中将保留有关作业和警报的数据。  
  
-   如果在要升级的实例中正在使用 SQLMail，则在升级之后将支持并启用关联的 XP。 否则，将关闭它们。  
  
-   数据库邮件（也称为 SQLiMail）将与 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]组件一起升级。 默认情况下，数据库邮件在升级之后将会关闭。 升级之后，任何架构更新都应该与更新脚本进行协调。  
  
## <a name="see-also"></a>请参阅  
 [支持的版本升级](supported-version-and-edition-upgrades.md)   
 [后向兼容性](../../getting-started/backward-compatibility.md)   
 [升级到 SQL Server 2014 使用安装向导&#40;安装程序&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  