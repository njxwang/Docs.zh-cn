---
title: "使用 Visual Studio for Mac 向 Razor 页面应用添加模型"
author: rick-anderson
description: "使用 Visual Studio for Mac 在 ASP.NET Core 中向 Razor 页面应用添加模型"
ms.author: riande
manager: wpickett
ms.date: 08/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages-mac/model
ms.openlocfilehash: 7b1b2d54e9c68b0a6f2b1355726d0d1cb484f69e
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="adding-a-model-to-a-razor-pages-app-in-aspnet-core-with-visual-studio-for-mac"></a><span data-ttu-id="d4b48-103">使用 Visual Studio for Mac 在 ASP.NET Core 中向 Razor 页面应用添加模型</span><span class="sxs-lookup"><span data-stu-id="d4b48-103">Adding a model to a Razor Pages app in ASP.NET Core with Visual Studio for Mac</span></span>

[!INCLUDE[model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="d4b48-104">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="d4b48-104">Add a data model</span></span>

* <span data-ttu-id="d4b48-105">在解决方案资源管理器中，右键单击“RazorPagesMovie”项目，然后选择“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-105">In Solution Explorer, right-click the **RazorPagesMovie** project, and then select **Add** > **New Folder**.</span></span> <span data-ttu-id="d4b48-106">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-106">Name the folder *Models*.</span></span>
* <span data-ttu-id="d4b48-107">右键单击“Models”文件夹，然后选择“添加” > “新建文件”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-107">Right-click the *Models* folder, and then select **Add** > **New File**.</span></span>
* <span data-ttu-id="d4b48-108">在“新建文件”对话框中：</span><span class="sxs-lookup"><span data-stu-id="d4b48-108">In the **New File** dialog:</span></span>

  * <span data-ttu-id="d4b48-109">在左侧窗格中，选择“常规”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-109">Select **General** in the left pane.</span></span>
  * <span data-ttu-id="d4b48-110">在中间窗格中，选择“空类”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-110">Select **Empty Class** in the center pain.</span></span>
  * <span data-ttu-id="d4b48-111">将此类命名为“Movie”，然后选择“新建”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-111">Name the class **Movie** and select **New**.</span></span>

[!INCLUDE[model 2](../../includes/RP/model2.md)]
[!INCLUDE[model 2a](../../includes/RP/model2a.md)]

[!code-csharp[Main](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

<span data-ttu-id="d4b48-112">右键单击红色波浪线，例如，行 `services.AddDbContext<MovieContext>(options =>` 中的 `MovieContext`。</span><span class="sxs-lookup"><span data-stu-id="d4b48-112">Right click on a red squiggly line, for example `MovieContext` in the line `services.AddDbContext<MovieContext>(options =>`.</span></span> <span data-ttu-id="d4b48-113">选择“快速修复”>“使用RazorPagesMovie.Models;”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-113">Select **Quick Fix > using RazorPagesMovie.Models;**.</span></span> <span data-ttu-id="d4b48-114">Visual Studio 添加 using 语句。</span><span class="sxs-lookup"><span data-stu-id="d4b48-114">Visual studio adds the using statement.</span></span>

<span data-ttu-id="d4b48-115">生成项目以验证有没有任何错误存在。</span><span class="sxs-lookup"><span data-stu-id="d4b48-115">Build the project to verify you don't have any errors.</span></span>

![创建页面](model/red.png)

### <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="d4b48-117">用于进行迁移的 Entity Framework Core NuGet 包</span><span class="sxs-lookup"><span data-stu-id="d4b48-117">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="d4b48-118">[Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) 中提供了适用于命令行接口 (CLI) 的 EF 工具。</span><span class="sxs-lookup"><span data-stu-id="d4b48-118">The EF tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="d4b48-119">若要安装此包，请将它添加到 .csproj 文件中的 `DotNetCliToolReference` 集合。</span><span class="sxs-lookup"><span data-stu-id="d4b48-119">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file.</span></span> <span data-ttu-id="d4b48-120">注意：必须通过编辑 .csproj 文件来安装此包；不能使用 `install-package` 命令或程序包管理器 GUI。</span><span class="sxs-lookup"><span data-stu-id="d4b48-120">**Note:** You have to install this package by editing the *.csproj* file; you can't use the `install-package` command or the package manager GUI.</span></span>

<span data-ttu-id="d4b48-121">若要编辑“.csproj”文件：</span><span class="sxs-lookup"><span data-stu-id="d4b48-121">To edit a *.csproj* file:</span></span>

* <span data-ttu-id="d4b48-122">选择“文件” > “打开”，然后选择“.csproj”文件。</span><span class="sxs-lookup"><span data-stu-id="d4b48-122">Select **File** > **Open**, and then select the *.csproj* file.</span></span>
* <span data-ttu-id="d4b48-123">选择“选项”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-123">Select **Options**.</span></span>
* <span data-ttu-id="d4b48-124">将“打开方式”更改为“源代码编辑器”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-124">Change **Open with** to **Source Code Editor**.</span></span>

![编辑 csproj 文件](model/csproj.png)

<span data-ttu-id="d4b48-126">将 `Microsoft.EntityFrameworkCore.Tools.DotNet` 工具引用添加至第二个 \<ItemGroup>：</span><span class="sxs-lookup"><span data-stu-id="d4b48-126">Add the `Microsoft.EntityFrameworkCore.Tools.DotNet` tool reference to the second **\<ItemGroup>**:</span></span>

[!code-xml[Main](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj?range=12-16&highlight=4)]

[!INCLUDE[model3](../../includes/RP/model3.md)]
[!INCLUDE[model 4x](../../includes/RP/model4x.md)]

[!INCLUDE[model 4 exit](../../includes/RP/model4exit.md)]

[!INCLUDE[model 4](../../includes/RP/model4.md)]

### <a name="add-the-pagesmovies-files-to-the-project"></a><span data-ttu-id="d4b48-127">将页面/电影文件添加到项目</span><span class="sxs-lookup"><span data-stu-id="d4b48-127">Add the Pages/Movies files to the project</span></span>

* <span data-ttu-id="d4b48-128">在 Visual Studio 中，右键单击“页面”文件夹，然后选择“添加”>“添加现有文件夹”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-128">In Visual Studio, Right-click the *Pages* folder and select **Add > Add existing Folder**.</span></span>
* <span data-ttu-id="d4b48-129">选择“电影”文件夹。</span><span class="sxs-lookup"><span data-stu-id="d4b48-129">Select the *Movies* folder.</span></span>
* <span data-ttu-id="d4b48-130">在“选择包括到项目中的文件”对话框中，选择“包括所有”。</span><span class="sxs-lookup"><span data-stu-id="d4b48-130">In the *Chosse files to include in the project* dialog, select **Include All**.</span></span>

<span data-ttu-id="d4b48-131">下一个教程介绍由基架创建的文件。</span><span class="sxs-lookup"><span data-stu-id="d4b48-131">The next tutorial explains the files created by scaffolding.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="d4b48-132">[上一篇：入门](xref:tutorials/razor-pages-mac/razor-pages-start)
[下一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="d4b48-132">[Previous: Getting Started](xref:tutorials/razor-pages-mac/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>