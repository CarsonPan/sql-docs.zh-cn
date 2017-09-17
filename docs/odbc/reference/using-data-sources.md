---
title: "使用数据源 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb3e6adb6f563e49429c2e04239ce3170d96b9a4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-data-sources"></a>使用数据源
数据源通常由最终用户或与程序的技术调用*ODBC 管理器*。 ODBC 管理器会提示驱动程序要使用的用户，然后调用该驱动程序。 该驱动程序显示一个对话框，请求它需要连接到数据源的信息。 用户输入的信息后，该驱动程序会将其存储在系统上。  
  
 更高版本，应用程序调用驱动程序管理器，并将其传递机数据源的名称或包含文件数据源的文件的路径。 当传递机数据源名称，驱动程序管理器搜索系统以查找数据源使用的驱动程序。 然后，将加载驱动程序，并将数据源名称传递给它。 该驱动程序使用的数据源名称查找它需要连接到数据源的信息。 最后，它会连接到数据源，通常提示输入用户 ID 和密码，这通常不会存储的用户。  
  
 当传递文件数据源时，驱动程序管理器中打开的文件，并加载指定的驱动程序。 如果文件还包含连接字符串，它可以将此传递到该驱动程序。 该驱动程序连接字符串中使用的信息，连接到数据源。 如果不传递任何连接字符串，该驱动程序通常会提示用户输入所需的信息。