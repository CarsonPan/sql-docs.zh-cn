---
title: 填充全文索引 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- index populations [full-text search]
- incremental populations [full-text search]
- populations [full-text search]
- full-text search [SQL Server], populations
- crawls [full-text search]
- automatic full-text index updates
- change tracking-based populations [full-text search]
- manual updates [full-text search]
- manual populations [full-text search]
- auto populations [full-text search]
- full-text indexes [SQL Server], key column
- full populations [full-text search]
- full-text indexes [SQL Server], populations
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
caps.latest.revision: 74
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cbe50e41fb353e092edddf2eacc2f189d635aa5d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37162258"
---
# <a name="populate-full-text-indexes"></a>填充全文索引
  创建和维护全文索引涉及使用称为“填充”（也称为“爬网”）的过程填充索引。  
  
##  <a name="types"></a> 填充类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持以下填充类型： 完全填充、 基于更改跟踪的自动或手动填充和基于时间戳的增量式填充。  
  
### <a name="full-population"></a>完全填充  
 在完全填充期间，为表或索引视图的所有行生成索引条目。 全文索引的完全填充为基表或索引视图的所有行生成索引条目。  
  
 默认情况下，一旦创建新的全文索引，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 便会对其进行完全填充。 但是，完全填充会占用相当多的资源。 因此，当在高峰期创建全文索引时，最佳做法通常是将完全填充推迟到非高峰时段，当全文索引的基表非常大时更应如此。 不过，索引所属的全文目录在填充其所有全文索引之后才可使用。 若要创建全文索引而不立即填充它，请在 CREATE FULLTEXT INDEX 语句中指定 CHANGE_TRACKING OFF, NO POPULATION 子句。 如果您指定 CHANGE_TRACKING MANUAL，全文引擎将使用语句。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 直到执行使用 START FULL POPULATION 或 START INCREMENTAL POPULATION 子句的 ALTER FULLTEXT INDEX 语句，将不填充新的全文索引。 有关详细信息，请参阅本主题后面的示例“A. 创建全文索引而不运行完全填充”和“B. 对表运行完全填充”。  
  

  
### <a name="change-tracking-based-population"></a>基于更改跟踪的填充  
 或者，您可以在对全文索引进行初始完全填充之后使用更改跟踪对其进行维护。 将出现与更改跟踪关联的较小开销，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 维护它用来跟踪自上次填充后对基表所做更改的表。 当使用更改跟踪时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 维护基表或索引视图中已通过更新、删除或插入进行过修改的行的记录。 通过 WRITETEXT 和 UPDATETEXT 所做的数据更改不会反映到全文索引中，也不能使用更改跟踪方法拾取。  
  
> [!NOTE]  
>  表包含`timestamp`列中，可以使用增量填充。  
  
 如果在创建索引期间启用更改跟踪，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在新全文索引创建之后立即对其进行完全填充。 其后，将跟踪更改并将更改传播到全文索引。 有两类更改跟踪：自动（CHANGE_TRACKING AUTO 选项）和手动（CHANGE_TRACKING MANUAL 选项）。 自动更改跟踪为默认行为。  
  
 更改跟踪的类型确定全文索引的填充方式，如下所示：  
  
-   自动填充  
  
     默认情况下，或者如果您指定 CHANGE_TRACKING AUTO，全文引擎将对全文索引使用自动填充。 完成首次完全填充之后，当修改基表中的数据时将跟踪更改并自动传播跟踪的更改。 不过，由于全文索引是在后台更新的，因此传播的更改可能不会立即反映到索引中。  
  
     **若要设置使用自动填充的跟踪更改**  
  
    -   [CREATE FULLTEXT INDEX](/sql/t-sql/statements/create-fulltext-index-transact-sql) … WITH CHANGE_TRACKING AUTO  
  
    -   [ALTER FULLTEXT INDEX](/sql/t-sql/statements/alter-fulltext-index-transact-sql) … SET CHANGE_TRACKING AUTO  
  
     有关详细信息，请参阅本主题后面的示例“E. 更改全文索引以使用自动更改跟踪”。  
  
-   手动填充  
  
     如果您指定 CHANGE_TRACKING MANUAL，全文引擎将对全文索引使用手动填充。 完成首次完全填充之后，当修改基表中的数据时将跟踪更改。 但是，这些更改不会传播到全文索引，直至你执行 ALTER FULLTEXT INDEX … START UPDATE POPULATION 语句手动应用更改。 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理来定期调用此 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
     **启动使用手动填充的跟踪更改**  
  
    -   [CREATE FULLTEXT INDEX](/sql/t-sql/statements/create-fulltext-index-transact-sql) … WITH CHANGE_TRACKING MANUAL  
  
    -   [ALTER FULLTEXT INDEX](/sql/t-sql/statements/alter-fulltext-index-transact-sql) … SET CHANGE_TRACKING MANUAL  
  
     有关详细信息，请参阅本主题后面的示例“C. 使用手动更改跟踪创建全文索引”和“D. 运行手动填充”。  
  
 **若要关闭更改跟踪**  
  
-   [CREATE FULLTEXT INDEX](/sql/t-sql/statements/create-fulltext-index-transact-sql) … WITH CHANGE_TRACKING OFF  
  
-   [ALTER FULLTEXT INDEX](/sql/t-sql/statements/alter-fulltext-index-transact-sql) … SET CHANGE_TRACKING OFF  
  

  
### <a name="incremental-timestamp-based-population"></a>基于时间戳的增量填充  
 增量填充是手动填充全文索引的一种替代机制。 您可以对 CHANGE_TRACKING 设置为 MANUAL 或 OFF 的全文索引运行增量填充。 如果全文索引的第一个填充是增量填充，它将对所有行编制索引并使其等效于完全填充。  
  
 增量填充要求是索引的表必须具有的一个列`timestamp`数据类型。 如果 `timestamp` 列不存在，则无法执行增量填充。 没有的表增量填充请求`timestamp`列会导致完全填充操作。 另外，如果影响表全文索引的任意元数据自上次填充以来发生了变化，则增量填充请求将作为完全填充来执行。 这包括更改任何列、索引或全文索引定义所引起的元数据更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 `timestamp` 列标识自上次填充后发生更改的行。 然后，增量填充在全文索引中更新上次填充的当时或之后添加、删除或修改的行。 如果对表进行大量插入操作，则使用增量填充会较使用手动填充有效。  
  
 在填充结束时，全文引擎将记录新的 `timestamp` 值。 此值是最大`timestamp`SQL 收集器遇到的值。 以后再启动增量填充时，将会使用此值。  
  
 若要运行增量填充，请执行使用 START INCREMENTAL POPULATION 子句的 ALTER FULLTEXT INDEX 语句。  
  

  
##  <a name="examples"></a> 填充全文索引的示例  
  
> [!NOTE]  
>  本节中的示例使用 `Production.Document` 示例数据库的 `HumanResources.JobCandidate` 或 `AdventureWorks` 表。  
  
### <a name="a-creating-a-full-text-index-without-running-a-full-population"></a>A. 创建全文索引而不运行完全填充  
 以下示例对 `Production.Document` 示例数据库的 `AdventureWorks` 表创建全文索引。 该示例使用 WITH CHANGE_TRACKING OFF, NO POPULATION 来延迟初次完全填充。  
  
```  
CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
CREATE FULLTEXT CATALOG AW_Production_FTCat;  
CREATE FULLTEXT INDEX ON Production.Document  
(  
    Document                         --Full-text index column name   
        TYPE COLUMN FileExtension    --Name of column that contains file type information  
        Language 1033                 --1033 is LCID for the English language  
)  
    KEY INDEX ui_ukDoc  
    ON AW_Production_FTCat  
    WITH CHANGE_TRACKING OFF, NO POPULATION;  
GO  
  
```  
  
### <a name="b-running-a-full-population-on-table"></a>B. 对表运行完全填充  
 以下示例对 `Production.Document` 示例数据库的 `AdventureWorks` 表运行完全填充。  
  
```  
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
  
### <a name="c-creating-a-full-text-index-with-manual-change-tracking"></a>C. 使用手动更改跟踪创建全文索引  
 以下示例对 `HumanResources.JobCandidate` 示例数据库的 `AdventureWorks` 表创建全文索引，该全文索引将使用具有手动填充的更改跟踪。  
  
```  
USE AdventureWorks;  
GO  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH CHANGE_TRACKING=MANUAL;  
GO  
```  
  
### <a name="d-running-a-manual-population"></a>D. 运行手动填充  
 以下示例对 `HumanResources.JobCandidate` 示例数据库的 `AdventureWorks` 表的更改跟踪全文索引运行手动填充。  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
GO  
```  
  
### <a name="e-altering-a-full-text-index-to-use-automatic-change-tracking"></a>E. 更改全文索引以使用自动更改跟踪  
 以下示例更改 `HumanResources.JobCandidate` 示例数据库的 `AdventureWorks` 表的全文索引以使用自动填充的更改跟踪。  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
GO   
```  
  

  
##  <a name="create"></a> 创建或更改增量填充计划  
  
#### <a name="to-create-or-change-a-schedule-for-incremental-population-in-management-studio"></a>在 Management Studio 中创建或更改增量填充计划  
  
1.  在对象资源管理器中，展开服务器。  
  
2.  展开“数据库”，然后展开包含全文索引的数据库。  
  
3.  展开 **“表”**。  
  
 右键单击对其定义了全文索引的表，选择“全文索引”，然后在“全文索引”上下文菜单中单击“属性”。 此时将打开“全文索引属性”对话框。  
  
1.  在 **“选择页”** 窗格中，选择“计划”。  
  
     使用此页可以创建或管理 SQL Server 代理作业的计划，该作业用于启动对全文索引基表或索引视图的表增量填充。  
  
    > [!IMPORTANT]  
    >  如果基表或视图不包含的列`timestamp`数据类型，则执行完全填充。  
  
     选项如下所示：  
  
    -   若要创建新计划，请单击 **“新建”**。  
  
         此时将打开“新建全文索引表计划”对话框，你可以在此对话框中创建计划。 若要保存计划，请单击 **“确定”**。  
  
        > [!IMPORTANT]  
        >  在退出“全文索引属性”对话框之后，SQL Server 代理作业（对 *database_name*.*table_name* 启动表增量填充）将与新计划相关联。 如果您针对该全文索引创建多个计划，则这些计划都将使用同一作业。  
  
    -   若要更改某个计划，请选择该计划并单击 **“编辑”**。  
  
         此时将打开“新建全文索引表计划” 对话框，你可以在此对话框中修改计划。  
  
        > [!NOTE]  
        >  有关修改作业的信息，请参阅[修改作业](../../ssms/agent/modify-a-job.md)。  
  
    -   若要删除某个计划，请选择该计划并单击 **“删除”**。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  

  
##  <a name="crawl"></a> 排除全文填充 （爬网） 中的错误  
 如果在爬网期间发生了错误，全文搜索的爬网日志功能会创建并维护一个爬网日志，该日志是一个纯文本文件。 每个爬网日志都对应于某一个全文目录。 对给定实例的默认爬网日志，在这种情况下，第一个实例，位于 %ProgramFiles%\Microsoft SQL Server\MSSQL12。MSSQLSERVER\MSSQL\LOG 文件夹。 爬网日志文件遵循以下命名方案：  
  
 SQLFT\<DatabaseID >\<FullTextCatalogID >。日志 [\<n >]  
  
 <`DatabaseID`>  
 数据库的 ID。 <`dbid`> 是一个五位数带有前导零。  
  
 <`FullTextCatalogID`>  
 全文目录 ID。 <`catid`> 是一个五位数带有前导零。  
  
 <`n`>  
 是一个整数，指示同一全文目录现有的一个或多个爬网日志。  
  
 例如，SQLFT0000500008.2 是一个数据库 ID 为 5、全文目录 ID 为 8 的数据库爬网日志文件。 文件名结尾的 2 指示此数据库/目录对具有两个爬网日志文件。  
  

  
## <a name="see-also"></a>请参阅  
 [sys.dm_fts_index_population (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)   
 [全文搜索入门](get-started-with-full-text-search.md)   
 [创建和管理全文索引](create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  