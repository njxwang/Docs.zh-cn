# <a name="aspnet-core-model-providers-sample"></a><span data-ttu-id="0202b-101">ASP.NET Core 模型提供程序示例</span><span class="sxs-lookup"><span data-stu-id="0202b-101">ASP.NET Core Model Providers Sample</span></span>

<span data-ttu-id="0202b-102">本示例演示如何使用 Razor 页面自定义路由和页面模型提供程序。</span><span class="sxs-lookup"><span data-stu-id="0202b-102">This sample illustrates use of Razor Pages custom route and page model providers.</span></span> <span data-ttu-id="0202b-103">本示例演示 [Razor 页面路由和应用约定](https://docs.microsoft.com/aspnet/core/mvc/razor-pages/razor-pages-convention-features)主题中介绍的功能。</span><span class="sxs-lookup"><span data-stu-id="0202b-103">This sample demonstrates the features described in the [Razor Pages route and app conventions](https://docs.microsoft.com/aspnet/core/mvc/razor-pages/razor-pages-convention-features) topic.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="0202b-104">此示例中的示例</span><span class="sxs-lookup"><span data-stu-id="0202b-104">Examples in this sample</span></span>

| <span data-ttu-id="0202b-105">方案</span><span class="sxs-lookup"><span data-stu-id="0202b-105">Scenario</span></span> | <span data-ttu-id="0202b-106">示例演示</span><span class="sxs-lookup"><span data-stu-id="0202b-106">Sample demo</span></span> |
| -------- | ----------- |
| [<span data-ttu-id="0202b-107">模型约定</span><span class="sxs-lookup"><span data-stu-id="0202b-107">Model conventions</span></span>](https://docs.microsoft.com/aspnet/core/mvc/razor-pages/razor-pages-convention-features#model-conventions) | <span data-ttu-id="0202b-108">将路由特性和标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="0202b-108">Add a route attribute and header to the app's pages.</span></span> |
| [<span data-ttu-id="0202b-109">使用 AddPageRoute 添加页面路由</span><span class="sxs-lookup"><span data-stu-id="0202b-109">Use AddPageRoute to add a page route</span></span>](https://docs.microsoft.com/aspnet/core/mvc/razor-pages/razor-pages-convention-features#configure-a-page-route) | <span data-ttu-id="0202b-110">将指定的路由添加到指定的页面。</span><span class="sxs-lookup"><span data-stu-id="0202b-110">Adds the specified route to the page at the specified page.</span></span> |
| [<span data-ttu-id="0202b-111">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="0202b-111">Page model action conventions</span></span>](https://docs.microsoft.com/aspnet/core/mvc/razor-pages/razor-pages-convention-features#page-model-action-conventions) | <span data-ttu-id="0202b-112">将标头添加到某个文件夹中的多个页面，将标头添加到单个页面，以及配置筛选器工厂以将标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="0202b-112">Add a header to pages in a folder, add a header to a single page, and configure a filter factory to add a header to the app's pages.</span></span> |
| [<span data-ttu-id="0202b-113">替换默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="0202b-113">Replace the default page app model provider</span></span>](https://docs.microsoft.com/aspnet/core/mvc/razor-pages/razor-pages-convention-features#replace-the-default-page-app-model-provider) | <span data-ttu-id="0202b-114">更改处理程序命名约定。</span><span class="sxs-lookup"><span data-stu-id="0202b-114">Change the conventions for handler naming.</span></span> |