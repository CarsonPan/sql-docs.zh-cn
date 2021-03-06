---
title: sys.external_library_files (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_library_files catalog view
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9666b58132feb79876c4e8074dc530440c05b2c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828055"
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys.external_library_files (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

列出了每个文件组成的外部库的行。

|列名 |数据类型 |Description|
|------|------|-----|
|external_library_id | ssNoversion |外部库对象的 ID。 |
|content |varbinary(max) |外部库文件项目的内容。 |
|平台 |TINYINT |在其安装 SQL Server 的主机平台的 ID。 |
|platform_desc | nvarchar(60) |主机平台的名称。 有效值为 WINDOWS、 LINUX。 |

### <a name="see-also"></a>另请参阅  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)  
[为 SQL Server 机器学习服务的包管理](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
