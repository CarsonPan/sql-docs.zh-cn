---
title: sys.database_filestream_options (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_filestream_options
- sys.database_filestream_options_TSQL
- database_filestream_options_TSQL
- sys.database_filestream_options
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_filestream_options catalog view
ms.assetid: 3383c607-0bbc-456a-ab37-7230f4cbf0e9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3038b27084dce6a84436e658c66b77dc61ead49e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543010"
---
# <a name="sysdatabasefilestreamoptions-transact-sql"></a>sys.database_filestream_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示已启用的针对 FileTable 中的 FILESTREAM 数据的非事务性访问级别的相关信息。 为 SQL Server 实例中的每个数据库包含一行。  
  
 有关 FileTable 的详细信息，请参阅 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)。  
  
  
|“列”|类型|Description|  
|------------|----------|-----------------|  
|**database_id**|**int**|数据库的 ID。 此值在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中是唯一的。|  
|**directory_name**|**nvarchar(255)**|所有 FileTable 命名空间的数据库级别目录。|  
|**non_transacted_access**|**tinyint**|已启用的针对 FILESTREAM 数据的非事务性访问的级别。 通过设置 NON_TRANSACTED_ACCESS 选项的设置的访问级别**CREATE DATABASE**或**ALTER DATABASE**语句。<br /><br /> 此设置具有以下值之一：<br /><br /> 0-未启用。 这是默认值。 通过提供值来设置此级别**OFF**有关**NON_TRANSACTED_ACCESS**选项。<br /><br /> 1-只读访问权限。 通过提供值来设置此级别**READ_ONLY**有关**NON_TRANSACTED_ACCESS**选项。<br /><br /> 3-完全访问权限。 通过提供值来设置此级别**完整**有关**NON_TRANSACTED_ACCESS**选项。<br /><br /> 5 - 正在转换到 READONLY<br /><br /> 6-正在转换到 OFF|  
|**non_transacted_access_desc**|**nvarchar(60)**|Non_transacted_access 中标识的非事务性访问的级别的说明。<br /><br /> 此设置具有以下值之一：<br /><br /> 无-这是默认值。<br /><br /> READ_ONLY<br /><br /> FULL<br /><br /> IN_TRANSITION_TO_READ_ONLY<br /><br /> IN_TRANSITION_TO_OFF|  
  
## <a name="see-also"></a>请参阅  
 [启用 FileTable 的先决条件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
  
