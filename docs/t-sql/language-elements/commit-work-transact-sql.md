---
title: "提交工作 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COMMIT_WORK_TSQL
- WORK_TSQL
- WORK
- COMMIT WORK
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- COMMIT WORK statement
ms.assetid: 4de76f33-399e-4912-a617-6eb6c560a058
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5f3bdf224b83f93f655ae1d324bbb654debf498e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="commit-work-transact-sql"></a>COMMIT WORK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  标志事务的结束。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
COMMIT [ WORK ]  
[ ; ]  
```  
  
## <a name="remarks"></a>注释  
 此语句的功能与 COMMIT TRANSACTION 相同，但 COMMIT TRANSACTION 接受用户定义的事务名称。 这个指定或没有指定可选关键字 WORK 的 COMMIT 语法与 SQL-92 兼容。  
  
## <a name="see-also"></a>另请参阅  
 [BEGIN DISTRIBUTED TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION (Transact-SQL)](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION (Transact-SQL)](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [回滚工作 &#40;Transact SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION (Transact-SQL)](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT (Transact-SQL)](../../t-sql/functions/trancount-transact-sql.md)  
  
  
