---
title: MSSQLSERVER_33129 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 991757d1bfeae8ecc0dec3a69d82c3dcab6415b1
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531649"
---
# <a name="mssqlserver33129"></a>MSSQLSERVER_33129
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|33129|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_CANNOT_DISABLE_WIN_GROUP|  
|消息正文|不能使用带 DISABLE 参数的 ALTER_LOGIN 来拒绝对 Windows 组的访问。|  
  
## <a name="explanation"></a>解释  
 尝试禁用某一 Windows 组的登录名时，会出现此消息。  
  
## <a name="user-action"></a>用户操作  
 Windows 组的登录名不能禁用。 若要暂时删除对某一 Windows 组授予的访问权限，则使用 REVOKE 命令吊销对 Windows 组的该登录名的 CONNECT 权限。 Windows 用户仍可能通过其单独的登录名或通过另一个 Windows 组具有访问权限。 下面的示例吊销 WESTCOAST 域的 Accounting 组的连接权限。  
  
```sql  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
  
