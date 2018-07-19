---
title: 发布服务器信息，代理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.commonjobs.f1
ms.assetid: 2346c00d-c269-45a1-af14-68e7fd7ebd7e
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84403d87fac40506b244931fd967504d2a18e78c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266793"
---
# <a name="publisher-information-agents"></a>发布服务器信息，代理
  **“代理”** 选项卡显示与发布服务器关联的代理和维护作业的相关信息：  
  
-   快照代理，为所有发布显示。  
  
-   日志读取器代理，为所有事务发布显示。  
  
-   队列读取器代理，为那些针对排队更新订阅启用的事务发布显示。  
  
-   维护作业，为所有发布显示：  
  
    -   重新初始化出现数据验证失败的订阅  
  
    -   代理历史记录清除：分发  
  
    -   分发的复制监视刷新器  
  
    -   复制代理检查  
  
    -   分发清除：分发  
  
    -   过期的订阅清除  
  
 有关这些作业的详细信息，请参阅[复制代理管理](agents/replication-agent-administration.md)。  
  
## <a name="options"></a>“常规”  
 若要显示有关代理或作业的信息，请从 **“代理和作业类型”** 下拉菜单中选择。 若要查看与代理或作业相关的详细信息和任务，请右键单击该代理或作业所在的行，然后单击快捷菜单上的选项。 若要更改网格显示数据的方式，请右键单击网格，然后单击以下选项之一：  
  
-   **排序**：按 **“列排序”** 对话框中的一列或多列排序。  
  
-   **选择要显示的列**：选择要显示哪些列以及要在 **“选择列”** 对话框中以何种顺序显示它们。  
  
-   **筛选器**：根据 **“筛选设置”** 对话框中的列值筛选网格中的行。  
  
-   **清除筛选器**：清除网格的任何筛选设置。  
  
 筛选设置是特定于每个网格的。 列的选择和排序应用于同一类型的所有网格，如每个发布服务器的发布网格。  
  
 以下各节说明了此选项卡上为每个代理或作业显示的数据。  
  
### <a name="snapshot-agent"></a>快照代理  
 **“状态”**  
 此代理的状态。 下面列出了可能的状态值：  
  
-   错误  
  
-   重试  
  
-   正在运行  
  
-   已完成  
  
 **发布**  
 与此代理关联的发布的名称。  
  
 **上次启动时间**  
 上次启动此代理的时间。  
  
 **Duration**  
 此代理已经运行的时间长度。 如果此代理当前正在运行，该时间表示已运行的时间；如果此代理之前已运行完毕，则该时间表示总时间。  
  
 **上一操作**  
 在此代理最近一次运行的过程中最后执行的操作。  
  
 **传送速率**  
 在此代理最近一次运行期间分发数据库中提交初始化命令的速率，以每秒的命令数表示。  
  
 **事务数**  
 在此代理最近一次运行期间分发数据库中提交的事务数。  
  
 **命令数**  
 在此代理最近一次运行期间分发数据库中提交的命令数。 一个命令相当于一次数据更改，如一次更新。  
  
### <a name="log-reader-agent"></a>日志读取器代理  
 **“状态”**  
 此代理的状态。 下面列出了可能的状态值：  
  
-   错误  
  
-   重试  
  
-   正在运行  
  
-   未运行  
  
 **发布数据库**  
 与此代理关联的发布的名称。  
  
 **上次启动时间**  
 上次启动此代理的时间。  
  
 **Duration**  
 此代理已经运行的时间长度。 如果此代理当前正在运行，该时间表示已运行的时间；如果此代理之前已运行完毕，则该时间表示总时间。  
  
 **上一操作**  
 在此代理最近一次运行的过程中最后执行的操作。  
  
 **传送速率**  
 在分发数据库中提交更改的速率，以每秒的命令数为单位。  
  
 **滞后时间**  
 从在发布数据库中提交最近的更改到在分发数据库中提交对应的命令经过的时间，以秒为单位。  
  
 **事务数**  
 在此代理最近一次运行期间分发数据库中提交的事务数。  
  
 **命令数**  
 在此代理最近一次运行期间分发数据库中提交的命令数。 一个命令相当于一次数据更改，如一次更新。  
  
 **平均命令数**  
 在此代理最近一次运行期间平均每个事务的命令数。  
  
### <a name="queue-reader-agent"></a>队列读取器代理  
 **“状态”**  
 此代理的状态。 下面列出了可能的状态值：  
  
-   错误  
  
-   重试  
  
-   正在运行  
  
-   未运行  
  
 **分发数据库**  
 与此代理关联的分发数据库的名称。  
  
 **上次启动时间**  
 上次启动此代理的时间。  
  
 **Duration**  
 此代理已经运行的时间长度。 如果代理当前正在运行，该时间表示已用时间；如果代理已在之前运行完毕，则该时间表示总时间。  
  
 **上一操作**  
 在此代理最近一次运行的过程中最后执行的操作。  
  
 **传送速率**  
 在分发数据库中提交更改的速率，以每秒的命令数为单位。  
  
 **滞后时间**  
 从在订阅数据库中提交最近的更改到在发布数据库中提交对应的命令经过的时间，以秒为单位。  
  
 **事务数**  
 在此代理最近一次运行期间发布数据库中提交的事务数。  
  
 **命令数**  
 在此代理最近一次运行期间发布数据库中提交的命令数。 一个命令相当于一次数据更改，如一次更新。  
  
 **平均命令数**  
 在此代理最近一次运行期间平均每个事务的命令数。  
  
### <a name="maintenance-jobs"></a>维护作业  
 **“状态”**  
 每个作业的状态。 下面列出了可能的状态值：  
  
-   错误  
  
-   重试  
  
-   正在运行  
  
-   未运行  
  
 **作业**  
 作业的名称。  
  
 **上次启动时间**  
 上次启动作业的时间。  
  
 **Duration**  
 作业已运行的时间。 如果此作业当前正在运行，该时间表示已运行的时间；如果此作业之前已运行完毕，该时间表示总时间。  
  
 **上一操作**  
 在此作业最近一次运行的过程中最后执行的操作。  
  
## <a name="see-also"></a>请参阅  
 [启动复制监视器](monitor/start-the-replication-monitor.md)   
 [查看发布服务器的信息和执行其任务（复制监视器）](monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [查看与发布关联的代理的信息和执行其任务（复制监视器）](monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [监视复制](monitoring-replication.md)  
  
  