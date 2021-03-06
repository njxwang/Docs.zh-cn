---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 开始使用 Entity Framework 6 Code First 通过 MVC 5 |Microsoft Docs
author: tdykstra
description: 本教程系列的较新版本是可用： 开始使用 ASP.NET Core 和 Entity Framework Core 使用 Visual Studio 2015。 Contoso Universi 中...
ms.author: aspnetcontent
ms.date: 10/22/2015
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: f03ddcf7dcc8b5d20c5459a7fb0015ab20f340c5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837164"
---
<a name="getting-started-with-entity-framework-6-code-first-using-mvc-5"></a>首先通过 MVC 5 使用 Entity Framework 6 Code First
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> > [!NOTE] 
> > 
> > 本系列教程的较新版本：[开始使用 ASP.NET Core 和 Entity Framework Core 使用 Visual Studio 2015](https://docs.asp.net/en/latest/data/ef-mvc/intro.html)。
> 
> 
> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。 本教程使用 Code First 工作流。 有关如何选择第一个代码、 数据库第一个和第一个模型之间的信息，请参阅[实体框架开发工作流](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。
> 
> 示例应用程序供一个虚构的 Contoso 大学网站使用。 它包括诸如学生入学、 课程创建和导师分配等功能。 此教程系列介绍了如何构建 Contoso University 示例应用程序。 你可以[下载完整的应用程序](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)。
> 
> 提供了由 Mike Brind 转换的 Visual Basic 版本：[使用 EF 6 在 Visual Basic 中的 MVC 5](http://www.mikesdotnetting.com/Article/241/MVC-5-with-EF-6-in-Visual-Basic-Creating-an-Entity-Framework-Data-Model) Mikesdotnetting 站点上。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - 实体框架 6 （EntityFramework 6.1.0 NuGet 包）
> - [Windows Azure SDK 2.2](https://go.microsoft.com/fwlink/p/?linkid=323510) （可选）
>   
> 
> 本教程还应适用于[Visual Studio 2013 Express for Web](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express)或 Visual Studio 2012。 [VS 2012 的 Windows Azure SDK 版本](https://go.microsoft.com/fwlink/p/?linkid=323511)是使用 Visual Studio 2012 的 Windows Azure 部署所必需的。
> 
> 
> ## <a name="tutorial-versions"></a>教程版本
> 
> 对于本教程的早期版本，请参阅[EF 4.1 / MVC 3 电子书](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)并[开始使用 EF 5 使用 MVC 4](../../older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> ## <a name="questions-and-comments"></a>问题和提出的意见
> 
> 请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)，则[实体框架和 LINQ to 实体论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。
> 
> 如果遇到无法解决的问题，您通常可以通过比较已完成的项目，您可以下载到你的代码中找到问题的解决方案。 一些常见错误以及如何解决这些问题，请参阅[常见的错误，以及解决方案或为它们的解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


## <a name="the-contoso-university-web-application"></a>Contoso University Web 应用程序

你将在这些教程中学习构建一个简单的大学网站的应用程序。

用户可以查看和更新学生、 课程和教师信息。 以下是一些你即将创建的页面。

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![编辑学生](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

本教程主要关注于如何使用 Entity Framework , 所以此站点的UI样式都是直接套用内置的模板。

## <a name="prerequisites"></a>系统必备

请参阅**软件版本**页的顶部。 Entity Framework 6 不是系统必备组件，因为本教程的一部分安装 EF NuGet 包。

## <a name="create-an-mvc-web-application"></a>创建 MVC Web 应用程序

打开 Visual Studio 并创建一个名为"ContosoUniversity"的新 C# Web 项目。

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

在中**新建 ASP.NET 项目**对话框中，选择**MVC**模板。

如果**在云中托管**中的复选框**Microsoft Azure**部分处于选中状态，将其清除。

单击**更改身份验证**。

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

在中**更改身份验证**对话框中，选择**无身份验证**，然后单击**确定**。 本教程中您不是要求用户在登录或基于登录的用户限制访问。

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

在新建 ASP.NET 项目对话框中，单击**确定**创建项目。

## <a name="set-up-the-site-style"></a>设置网站样式

通过几个简单的更改设置站点菜单、 布局和主页。

打开*views/shared\\_Layout.cshtml*，并进行以下更改：

- 将每个匹配项的"My ASP.NET Application"和"Application name"更改为"Contoso University"。
- 面向学生、 课程、 讲师和部门，添加菜单项和删除联系人条目。

突出显示所作更改。

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

在中*Views\Home\Index.cshtml*，该文件的内容替换为以下代码以将有关 ASP.NET 和 MVC 文本有关此应用程序的文本替换为：

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

按 CTRL + F5 以运行该站点。 请参阅主页，其中主菜单。

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

## <a name="install-entity-framework-6"></a>安装 Entity Framework 6

从**工具**菜单上，单击**NuGet 包管理器**，然后单击**程序包管理器控制台**。

在中**程序包管理器控制台**窗口中输入以下命令：

`Install-Package EntityFramework`

![安装 EF](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

该图像显示 6.0.0 安装，但 NuGet 将安装 （不包括预发行版本），实体框架的最新版本，截至到本教程的最新的更新是 6.1.1。

此步骤是几个步骤，本教程要求您手动执行此，但其无法进行了自动通过 ASP.NET MVC 基架功能之一。 要执行这些手动，以便您可以看到使用实体框架所需的步骤。 您将更高版本使用基架创建 MVC 控制器和视图。 一种替代方法是让基架会自动安装 EF NuGet 包、 创建数据库上下文类，并创建连接字符串。 如果你已准备好执行此操作通过这种方式，只需是跳过这些步骤，在创建实体类后，在 MVC 控制器搭建基架。

## <a name="create-the-data-model"></a>创建数据模型

接下来你将创建 Contoso 大学应用程序的实体类。 首先将以下三个实体：

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

`Student` 和 `Enrollment`实体之间是一对多的关系，`Course` 和`Enrollment` 实体之间也是一个对多的关系。 换而言之，一名学生可以修读任意数量的课程, 并且某一课程可以被任意数量的学生修读。

接下来，你将创建与这些实体对应的类。

> [!NOTE]
> 如果您尝试编译项目，然后完成创建所有这些实体类，将收到编译器错误。


### <a name="the-student-entity"></a>Student 实体

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

在中*模型*文件夹中，创建名为的类文件*Student.cs*和模板代码替换为以下代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` 属性将成为对应于此类的数据库表中的主键。 名为的属性解释默认情况下，实体框架`ID`或*classname* `ID`为主键。

`Enrollments`属性是*导航属性*。 导航属性中包含与此实体相关的其他实体。 在这种情况下，`Enrollments`的属性`Student`实体将保留所有`Enrollment`实体相关的`Student`实体。 换而言之，如果给定`Student`数据库中的行具有两个相关`Enrollment`行 (包含该学生的主键的行中的值及其`StudentID`外键列)，则该`Student`实体的`Enrollments`导航属性将包含这两个`Enrollment`实体。

导航属性通常定义为`virtual`，以便它们可以充分利用 Entity Framework 的特定功能，如*延迟加载*。 (将解释延迟加载在后面[读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)本系列后面的教程。)

如果导航属性可以具有多个实体 （如多对多或一对多关系），那么导航属性的类型必须是可以添加、 删除和更新条目的容器，如 `ICollection`。

### <a name="the-enrollment-entity"></a>Enrollment 实体

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)

在 *Models* 文件夹中，创建 *Enrollment.cs* 并且用以下代码替换现有代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID`属性将被设为主键; 此实体使用*classname* `ID`模式而不是`ID`如示`Student`实体。 通常情况下，你选择一个主键模式，并在你的数据模型自始至终使用这种模式。 在这里，使用了两种不同的模式只是为了说明你可以使用任一模式来指定主键。 在后面的教程，您将看到如何使用`ID`而无需`classname`轻松地在数据模型中实现继承。

`Grade`属性是[枚举](https://msdn.microsoft.com/data/hh859576.aspx)。 问号后`Grade`类型声明指示`Grade`属性是[可以为 null](https://msdn.microsoft.com/library/2cf62fcy.aspx)。 评级为 null 是不同于评级为零，null 表示一个等级未知或者尚未分配。

`StudentID` 属性是一个外键， `Student` 是与其对应的导航属性。 `Enrollment` 实体与一个 `Student` 实体相关联，因此该属性只包含单个 `Student` 实体 (与前面所看到的 `Student.Enrollments` 导航属性不同后，`Student`中可以容纳多个 `Enrollment` 实体)。

`CourseID` 属性是一个外键， `Course` 是与其对应的导航属性。 `Enrollment` 实体与一个 `Course` 实体相关联。

实体框架的属性解释为外键属性如果它名为*&lt;导航属性名称&gt;&lt;主键属性名称&gt;* (例如， `StudentID`对于`Student`导航属性所以`Student`实体的主键是`ID`)。 外键属性还可以进行命名相同只需*&lt;主键属性名称&gt;* (例如，`CourseID`由于`Course`实体的主键是`CourseID`)。

### <a name="the-course-entity"></a>Course 实体

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

在中*模型*文件夹中，创建*Course.cs*，模板代码替换为以下代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` 属性是导航属性。 一个 `Course` 体可以与任意数量的 `Enrollment` 实体相关。

我们会说的详细信息[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)本系列后面的教程中的属性。 简单来说，此特性让你能自行指定主键，而不是让数据库自动指定主键。

## <a name="create-the-database-context"></a>创建数据库上下文

协调为给定的数据模型的实体框架功能的主类是*数据库上下文*类。 通过从派生来创建此类[System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)类。 在该类中你可以指定数据模型中包含哪些实体。 你还可以定义某些 Entity Framework 行为。 在此项目中将数据库上下文类命名为 `SchoolContext`。

若要为 ContosoUniversity 项目中创建一个文件夹，右键单击项目中的**解决方案资源管理器**并单击**添加**，然后单击**新文件夹**。 将新文件夹命名*DAL* （适用于数据访问层）。 在该文件夹中创建名为的新类文件*SchoolContext.cs*，并使用以下代码替换模板代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specifying-entity-sets"></a>指定实体集

此代码将创建[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx)每个实体集的属性。 在实体框架术语中，*实体集*通常对应于数据库表和一个*实体*对应于表中的行。

> [!NOTE] 
> 
> 在这里可以省略 `DbSet<Enrollment>` 和 `DbSet<Course>` 语句，效果和省略之前相同。 Entity Framework 会隐式包含这两个实体因为 `Student` 实体引用了 `Enrollment` 实体、`Enrollment` 实体引用了 `Course` 实体。


### <a name="specifying-the-connection-string"></a>指定连接字符串

连接字符串 （它稍后将添加到 Web.config 文件） 的名称被传递给构造函数。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

此外可以传递连接字符串本身而不是一个存储在 Web.config 文件的名称中。 有关使用用于指定数据库选项的详细信息，请参阅[Entity Framework-连接和模型](https://msdn.microsoft.com/data/jj592674)。

如果未显式指定连接字符串或其中一个的名称，实体框架将假定该连接字符串名称是与类名称相同。 在此示例中的默认连接字符串名称都将`SchoolContext`，与您要指定的显式。

### <a name="specifying-singular-table-names"></a>指定单数形式的表名称

`modelBuilder.Conventions.Remove`中的语句[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法会阻止表名正在变为复数形式。 如果不这样做，将命名为数据库中生成的表`Students`， `Courses`，和`Enrollments`。 相反，将表名`Student`， `Course`，和`Enrollment`。 开发者对表名称是否应为复数意见不一。 本教程使用单数形式，但重要的一点是，你可以选择任意窗体，您的首选，通过包括或省略这行代码。

## <a name="set-up-ef-to-initialize-the-database-with-test-data"></a>EF 设置以使用测试数据初始化数据库

实体框架可以自动创建 （或删除并重新创建） 为您的应用程序运行时的数据库。 您可以指定应此操作每次你的应用程序运行时或仅在与现有的数据库不同步模型时。 此外可以编写`Seed`实体框架会自动填充测试数据以创建数据库后调用的方法。

默认行为是创建数据库，仅当它不存在 （和引发异常，如果模型已更改，并且数据库已存在）。 在本部分中会指定应删除并重新创建该模型发生更改时数据库。 删除数据库导致所有数据的丢失。 这通常是确定在开发期间，因为`Seed`方法将运行时重新创建数据库，并将重新创建您的测试数据。 但在生产环境中通常不想丢失所有数据，每次需要更改数据库架构。 稍后你将了解如何通过使用 Code First 迁移来更改数据库架构而不是删除并重新创建数据库来处理模型更改。

在 DAL 文件夹中，创建名为的新类文件*SchoolInitializer.cs*和的模板代码替换为  
下面的代码，这会导致要创建的数据库所需，并将测试数据加载到新数据库。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

`Seed`方法采用数据库上下文对象作为输入参数，并在方法中的代码使用该对象来将新实体添加到数据库。 对于每个实体类型，代码创建新实体的集合，将它们添加到相应`DbSet`属性，然后单击保存到数据库的更改。 但并不需要调用`SaveChanges`后的实体的每个组的方法，正如在这里，但这样做可帮助您找到问题的根源，如果向数据库写入代码时出现异常。

若要指示 Entity Framework 使用初始值设定项类，将元素添加到`entityFramework`应用程序中的元素*Web.config*文件 （一个根项目文件夹中），如下面的示例中所示：

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

`context type`指定完全限定的上下文类名称和它所在的程序集和`databaseinitializer type`指定初始值设定项类和它所在的程序集的完全限定的名称。 (如果不希望 EF 使用初始值设定项，您可以设置属性`context`元素： `disableDatabaseInitialization="true"`。)有关详细信息，请参阅[Entity Framework-配置文件设置](https://msdn.microsoft.com/data/jj556606)。

作为设置初始值设定项的替代方法*Web.config*文件是在代码中执行该操作通过添加`Database.SetInitializer`语句`Application_Start`中的方法*Global.asax.cs*文件。 有关详细信息，请参阅[了解数据库初始值设定项中 Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)。

现在设置应用程序注册，以便在给定运行的第一次访问数据库时  
应用程序中，实体框架比较模型数据库 (您`SchoolContext`和实体类)。 如果差异，应用程序删除并重新创建数据库。

> [!NOTE]
> 在部署到生产 web 服务器的应用程序时，必须删除或禁用删除并重新创建数据库的代码。 在本系列中下一个教程，将执行该操作。


## <a name="set-up-ef-to-use-a-sql-server-express-localdb-database"></a>设置为使用 SQL Server Express LocalDB 数据库的 EF

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)是 SQL Server Express 数据库引擎的轻型版本。 它易于安装和配置、 按需、 启动并在用户模式下运行。 中的 SQL Server Express，使您可以使用数据库作为特殊执行模式运行 LocalDB *.mdf*文件。 可以将 LocalDB 数据库文件放入*应用程序\_数据*web 项目，如果你想要能够复制数据库与项目的文件夹。 在 SQL Server Express 用户实例功能还使您可以使用 *.mdf*文件，但用户实例功能已弃用; 因此，用于处理建议 LocalDB *.mdf*文件。 在 Visual Studio 2012 和更高版本中，默认情况下使用 Visual Studio 安装 LocalDB。

通常 SQL Server Express 不用于生产 web 应用程序。 LocalDB 具体而言不是建议用于生产 web 应用程序因为它不旨在与 IIS 配合使用。

在本教程将使用 LocalDB。 打开应用程序*Web.config*文件，并添加`connectionStrings`元素前面`appSettings`元素，如下面的示例中所示。 (请确保更新*Web.config*根项目文件夹中的文件。 此外，还有*Web.config*文件位于*视图*无需更新的子文件夹。)

如果使用 Visual Studio 2015，"v11.0"替换连接字符串中"MSSQLLocalDB"，因为默认 SQL Server 实例名称已更改。

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

已添加的连接字符串指定实体框架将使用名为的 LocalDB 数据库*ContosoUniversity1.mdf*。 （该数据库尚不存在;EF 将创建它。）如果你想要在中创建的数据库你*应用程序\_数据*文件夹中，您可以添加`AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf`到连接字符串。 有关连接字符串的详细信息，请参阅[ASP.NET Web 应用程序的 SQL Server 连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。

您实际上不必中有一个连接字符串*Web.config*文件。 如果不提供连接字符串，实体框架将使用一个基于您的上下文类的默认值。 有关详细信息，请参阅[到新数据库 Code First](https://msdn.microsoft.com/data/jj193542)。

## <a name="creating-a-student-controller-and-views"></a>创建一个学生控制器和视图

现在，您将创建 web 页以显示数据，并请求数据的过程会自动触发  
创建数据库。 您将首先创建一个新的控制器。 但这样做之前，请生成项目以使模型和上下文类可用于 MVC 控制器基架。

1. 右键单击**控制器**中的文件夹**解决方案资源管理器**，选择**添加**，然后单击**新基架项**。
2. 在中**添加基架**对话框中，选择**包含的 MVC 5 控制器视图，使用实体框架**。

     ![添加基架](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)
3. 在添加控制器对话框中，进行以下选择，然后单击**添加**:

   - 模型类：**学生 (ContosoUniversity.Models)**。 （如果看不到下拉列表中的此选项，生成项目，然后重试。）
   - 数据上下文类： **SchoolContext (ContosoUniversity.DAL)**。
   - 控制器名称： **StudentController** (不 StudentsController)。
   - 保留其他字段的默认值。

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

     当您单击**添加**，基架创建 StudentController.cs 文件和一组使用控制器的视图 （.cshtml 文件）。 将来当你创建使用实体框架的项目，您还可以充分利用一些附加功能的基架： 只需创建第一个模型类，不要创建连接字符串，然后在**添加控制器**框中指定新的上下文类。 基架将创建在`DbContext`类和你的连接字符串以及控制器和视图。
4. Visual Studio 将打开*Controllers\StudentController.cs*文件。 您看到类变量已经创建了实例化数据库上下文对象：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     `Index`操作方法获取的学生列表*学生*实体集通过阅读`Students`数据库上下文实例的属性：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     *Student\Index.cshtml*视图的表中显示此列表：

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. 按 Ctrl+F5 运行项目。 （如果收到"无法创建卷影副本"错误，关闭浏览器和重试。）

     单击**学生**选项卡以查看测试数据的`Seed`插入的方法。 具体取决于如何窄浏览器窗口，您将看到顶部的地址栏中的学生选项卡链接或您必须单击右上角才能看到该链接。

     ![菜单按钮](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

     ![学生索引页](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="view-the-database"></a>查看数据库

当运行学生页面和应用程序尝试访问数据库时，EF 将看到没有任何数据库，所以创建了一个，然后它运行 seed 方法来使用数据填充数据库。

你可以使用**服务器资源管理器**或**SQL Server 对象资源管理器**(SSOX) 在 Visual Studio 中查看数据库。 对于本教程中，将使用**服务器资源管理器**。 (在 Visual Studio Express 版本早于 2013 年**服务器资源管理器**称为**数据库资源管理器**。)

1. 关闭浏览器。
2. 在中**服务器资源管理器**，展开**数据连接**，展开**学校上下文 (ContosoUniversity)**，然后展开**表**以查看在新数据库中的表。

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
3. 右键单击**学生**表，然后单击**显示表数据**若要查看已创建的列和插入到表的行。

    ![Student 表](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
4. 关闭**服务器资源管理器**连接。

*ContosoUniversity1.mdf*并 *.ldf*数据库文件位于`C:\Users\<yourusername>`文件夹。

正在使用，因此`DropCreateDatabaseIfModelChanges`初始值设定项，可以现在更改到`Student`类、 运行一次，应用程序和数据库会自动将重新创建，以匹配所做的更改。 例如，如果您将添加`EmailAddress`属性设置为`Student`类中，学生页上再次运行，然后查看表再次，您将看到管理新`EmailAddress`列。

## <a name="conventions"></a>约定

您必须在实体框架能够为您创建完整的数据库中编写的代码量很小的因为使用了*约定*，或使实体框架的假设。 其中一些已记下或使用而无需你不知道的：

- 复数的形式的实体类名称用作表名。
- 使用实体属性名作为列名。
- 命名的实体属性`ID`或*classname* `ID`被视为主键属性。
- 如果它名为一个属性将被解释为外键属性*&lt;导航属性名称&gt;&lt;主键属性名称&gt;* (例如， `StudentID` 为`Student`导航属性所以`Student`实体的主键是`ID`)。 外键属性还可以进行命名相同只需&lt;主键属性名称&gt;(例如，`EnrollmentID`由于`Enrollment`实体的主键是`EnrollmentID`)。

您已了解约定可以重写。 例如，指定表名不应变为复数形式，并稍后您将看到如何显式标记为外键属性的属性。 您将学习有关约定以及如何重写中对其的详细信息[创建更多的复杂数据模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)本系列后面的教程。 有关约定的详细信息，请参阅[Code First 约定](https://msdn.microsoft.com/data/jj679962)。

## <a name="summary"></a>总结

你现在已创建使用 Entity Framework 和 SQL Server Express LocalDB 来存储和显示数据的简单应用程序。 在以下教程中，您将学习如何执行基本的 CRUD （创建、 读取、 更新、 删除） 操作。

请在你喜欢本教程的内容，我们可以提高上留下反馈。 此外可以请求新主题[教我代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。

其他实体框架资源的链接可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)。

> [!div class="step-by-step"]
> [下一篇](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
