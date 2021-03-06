---
title: 第 2 课：定义用于父报表的数据连接和数据表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0a19f5fd51cf4e1b24e898ef3016c46edc152920
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022870"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>第 2 课：定义用于父报表的数据连接和数据表
  使用 Visual C# 的 ASP.NET 网站模板创建新网站项目后，接下来要创建用于父报表的数据连接和数据表。 在本教程中，数据连接指向 AdventureWorks2008 数据库。 也可选择连接到 AdventureWorks2012 数据库。  
  
### <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>通过添加 DataSet 定义数据连接和 DataTable（用于父报表）  
  
1.  在“网站”菜单上，选择“添加新项”。  
  
2.  在中**添加新项**对话框中，选择**数据集**然后单击**添加**。 出现提示时，应将该项添加到**App_Code**通过单击文件夹**是**。  
  
     此操作会将一个新的 XSD 文件 **DataSet1.xsd** 添加到项目，然后打开数据集设计器。  
  
3.  从“工具箱”窗口中，将一个 **[TableAdapter](https://msdn.microsoft.com/library/bz9tthwx\(v=vs.100\).aspx)** 控件拖到设计图面上。 随后将启动 **TableAdapter** 配置向导。  
  
4.  上**选择数据连接**页上，单击**新的连接**。  
  
5.  如果是首次在 Visual Studio 中创建数据源，可看到“选择数据源”页。 在“数据源”框中，选择“Microsoft SQL Server”。  
  
6.  在“添加连接”对话框中，执行以下步骤：  
  
    1.  在中**服务器名称**框中，输入服务器的位置**AdventureWorks2008**位于数据库所在。  
  
         默认的 SQL Server Express 实例为 **(local)\sqlexpress**。  
  
    2.  在“登录到服务器”部分中，选择使你可访问数据的选项。 “使用 Windows 身份验证”为默认选项。  
  
    3.  从**选择或输入数据库名称**下拉列表中，单击**AdventureWorks2008**。  
  
    4.  单击“确定”，然后单击“下一步”。  
  
7.  如果在第 6 (b) 步中选择了“使用 SQL Server 身份验证”，则选择一个选项，决定是在字符串中加入敏感数据还是在应用程序代码中设置该信息。  
  
8.  上**将连接字符串保存到应用程序配置文件**页上，键入连接字符串的名称或接受默认**AdventureWorks2008ConnectionString**。 单击“下一步” 。  
  
9. 上**选择命令类型**页上，选择**使用 SQL 语句**，然后单击**下一步**。  
  
10. 上**输入 SQL 语句**页上，输入以下 TRANSACT-SQL 查询以检索数据**AdventureWorks2008**数据库，然后依次**下一步**。  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
     此外可以通过单击创建查询**查询生成器**，然后通过单击验证查询**执行查询**。 如果查询返回的数据不符合预期，则可能使用的 AdventureWorks 版本较低。 有关安装的详细信息**AdventureWorks2008**版本的 AdventureWorks，请参阅[演练：安装 AdventureWorks 数据库](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx)。  
  
11. 上**生成的选择方法**页上，确保取消选中**创建方法以将更新发送到数据库 (GenerateDBDirectMethods) 直接**，然后单击**完成**.  
  
    > [!WARNING]  
    >  务必取消选中“创建”  
  
     配置 ADO.NET DataTable 对象作为报表的数据源现已完毕。 在 Visual Studio 中的“数据集设计器”页上，应看到所添加的 DataTable 对象，并列出在查询中指定的列。 DataSet1 由根据查询从 Product 表获得的数据组成。  
  
12. 保存该文件。  
  
13. 若要预览的数据，请单击**预览数据**上**数据**菜单，并单击**预览**。  
  
## <a name="next-task"></a>下一个任务  
 您已成功创建了用于父报表的数据连接和数据表。 接下来，将使用报表向导设计父报表。  
  
  
