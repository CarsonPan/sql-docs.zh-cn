---
title: "设置警报的寻呼地址的格式 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pager addresses [SQL Server]
- SQL Server Agent, alerts
- formats [SQL Server], pager addresses
- pager notifications [SQL Server]
- addresses [SQL Server]
- alerts [SQL Server], pager addresses
ms.assetid: a9797d01-1050-442c-9038-ed4bfee1e76a
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f202f1e48ca7c9ef030b5434514c4c5d6a93300b
ms.lasthandoff: 04/11/2017

---
# <a name="format-pager-addresses-for-alerts"></a>Format Pager Addresses for Alerts
本主题说明了如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中设置 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理警报的寻呼地址的格式。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要设置寻呼地址的格式，可使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
默认情况下，只有 **sysadmin** 固定服务器角色的成员才能查看有关警报的信息。 其他用户必须被授予 **msdb** 数据库中的 **SQLAgentOperatorRole** 固定数据库角色的权限。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-format-pager-addresses"></a>设置寻呼地址格式  
  
1.  在 **“对象资源管理器”**中，单击加号以展开包含要发送到寻呼程序的警报的服务器。  
  
2.  右键单击“SQL Server 代理”****，然后选择“属性”****  
  
3.  在 **“选择页”**下，选择 **“警报系统”**。  
  
4.  在“寻呼电子邮件的地址格式”****字段的“收件人行”****和“抄送行”****框中，输入寻呼地址的前缀或后缀。 发送通知时，将插入操作员的实际寻呼地址。  
  
5.  在 **“主题”** 框中，输入主题行的前缀或后缀。  
  
6.  选择“在通知页中包含电子邮件的正文部分”****复选框，以便在寻呼消息中包含完整电子邮件（与仅包含主题行相对）。  
  
7.  完成后，单击 **“确定”**。  
  
