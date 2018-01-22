---
title: "基于声明的授权"
author: rick-anderson
description: "本文档说明如何在 ASP.NET Core 应用中添加声明授权检查。"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/claims
ms.openlocfilehash: dd8f42684f9e58b9329602aa9b70d2c0ab950892
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="claims-based-authorization"></a><span data-ttu-id="3e79b-103">基于声明的授权</span><span class="sxs-lookup"><span data-stu-id="3e79b-103">Claims-Based Authorization</span></span>

<a name="security-authorization-claims-based"></a>

<span data-ttu-id="3e79b-104">创建一个标识时它可能会分配一个或多个由受信任方发出的声明。</span><span class="sxs-lookup"><span data-stu-id="3e79b-104">When an identity is created it may be assigned one or more claims issued by a trusted party.</span></span> <span data-ttu-id="3e79b-105">声明为名称值对，表示哪些主题为，可以不哪些的主题。</span><span class="sxs-lookup"><span data-stu-id="3e79b-105">A claim is name value pair that represents what the subject is, not what the subject can do.</span></span> <span data-ttu-id="3e79b-106">例如，你可能具有驱动程序的许可证，本地驱动的许可证颁发机构签发。</span><span class="sxs-lookup"><span data-stu-id="3e79b-106">For example, you may have a driver's license, issued by a local driving license authority.</span></span> <span data-ttu-id="3e79b-107">驱动程序的许可证对其具有你的出生日期。</span><span class="sxs-lookup"><span data-stu-id="3e79b-107">Your driver's license has your date of birth on it.</span></span> <span data-ttu-id="3e79b-108">在这种情况下将声明名称`DateOfBirth`，声明值将是你为出生日期，例如`8th June 1970`和颁发者是驱动的许可证颁发机构。</span><span class="sxs-lookup"><span data-stu-id="3e79b-108">In this case the claim name would be `DateOfBirth`, the claim value would be your date of birth, for example `8th June 1970` and the issuer would be the driving license authority.</span></span> <span data-ttu-id="3e79b-109">基于声明的授权，简单地说，将检查声明的值，并允许对基于该值资源的访问。</span><span class="sxs-lookup"><span data-stu-id="3e79b-109">Claims based authorization, at its simplest, checks the value of a claim and allows access to a resource based upon that value.</span></span> <span data-ttu-id="3e79b-110">例如，如果你想夜间俱乐部访问授权过程可能是：</span><span class="sxs-lookup"><span data-stu-id="3e79b-110">For example if you want access to a night club the authorization process might be:</span></span>

<span data-ttu-id="3e79b-111">门安全负责人将评估你的出生声明，并且它们是否在授予你访问之前信任颁发者 （驱动许可证机构） 的日期的值。</span><span class="sxs-lookup"><span data-stu-id="3e79b-111">The door security officer would evaluate the value of your date of birth claim and whether they trust the issuer (the driving license authority) before granting you access.</span></span>

<span data-ttu-id="3e79b-112">标识可以包含具有多个值的多个声明，并且可以包含多个相同类型的声明。</span><span class="sxs-lookup"><span data-stu-id="3e79b-112">An identity can contain multiple claims with multiple values and can contain multiple claims of the same type.</span></span>

## <a name="adding-claims-checks"></a><span data-ttu-id="3e79b-113">添加声明检查</span><span class="sxs-lookup"><span data-stu-id="3e79b-113">Adding claims checks</span></span>

<span data-ttu-id="3e79b-114">声明基于的授权检查声明性-开发人员将它们嵌入在其代码中，针对控制器或者控制器中的某个操作指定当前用户必须拥有，并选择性地声明的值必须保留访问的声明请求的资源。</span><span class="sxs-lookup"><span data-stu-id="3e79b-114">Claim based authorization checks are declarative - the developer embeds them within their code, against a controller or an action within a controller, specifying claims which the current user must possess, and optionally the value the claim must hold to access the requested resource.</span></span> <span data-ttu-id="3e79b-115">要求是基于策略的声明，开发人员必须生成并注册表达声明要求的策略。</span><span class="sxs-lookup"><span data-stu-id="3e79b-115">Claims requirements are policy based, the developer must build and register a policy expressing the claims requirements.</span></span>

<span data-ttu-id="3e79b-116">最简单的类型声明的声明存在策略如下所示，并且不检查值。</span><span class="sxs-lookup"><span data-stu-id="3e79b-116">The simplest type of claim policy looks for the presence of a claim and does not check the value.</span></span>

<span data-ttu-id="3e79b-117">首先，你需要生成和注册策略。</span><span class="sxs-lookup"><span data-stu-id="3e79b-117">First you need to build and register the policy.</span></span> <span data-ttu-id="3e79b-118">这是作为授权服务配置的一部分，这通常需要一部分花在`ConfigureServices()`中你*Startup.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="3e79b-118">This takes place as part of the Authorization service configuration, which normally takes part in `ConfigureServices()` in your *Startup.cs* file.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("EmployeeOnly", policy => policy.RequireClaim("EmployeeNumber"));
    });
}
```

<span data-ttu-id="3e79b-119">在这种情况下`EmployeeOnly`策略将检查是否存在`EmployeeNumber`于当前的标识声明。</span><span class="sxs-lookup"><span data-stu-id="3e79b-119">In this case the `EmployeeOnly` policy checks for the presence of an `EmployeeNumber` claim on the current identity.</span></span>

<span data-ttu-id="3e79b-120">你随后可应用策略使用`Policy`属性`AuthorizeAttribute`特性以指定策略名称;</span><span class="sxs-lookup"><span data-stu-id="3e79b-120">You then apply the policy using the `Policy` property on the `AuthorizeAttribute` attribute to specify the policy name;</span></span>

```csharp
[Authorize(Policy = "EmployeeOnly")]
public IActionResult VacationBalance()
{
    return View();
}
```

<span data-ttu-id="3e79b-121">`AuthorizeAttribute`特性可以应用于整个控制器，在这种情况，仅匹配策略的标识将在控制器上允许向任何操作的访问。</span><span class="sxs-lookup"><span data-stu-id="3e79b-121">The `AuthorizeAttribute` attribute can be applied to an entire controller, in this instance only identities matching the policy will be allowed access to any Action on the controller.</span></span>

```csharp
[Authorize(Policy = "EmployeeOnly")]
public class VacationController : Controller
{
    public ActionResult VacationBalance()
    {
    }
}
```

<span data-ttu-id="3e79b-122">如果您有一个控制器受`AuthorizeAttribute`属性，但想要允许匿名访问你应用的特定操作`AllowAnonymousAttribute`属性。</span><span class="sxs-lookup"><span data-stu-id="3e79b-122">If you have a controller that is protected by the `AuthorizeAttribute` attribute, but want to allow anonymous access to particular actions you apply the `AllowAnonymousAttribute` attribute.</span></span>

```csharp
[Authorize(Policy = "EmployeeOnly")]
public class VacationController : Controller
{
    public ActionResult VacationBalance()
    {
    }

    [AllowAnonymous]
    public ActionResult VacationPolicy()
    {
    }
}
```

<span data-ttu-id="3e79b-123">大多数声明附带了一个值。</span><span class="sxs-lookup"><span data-stu-id="3e79b-123">Most claims come with a value.</span></span> <span data-ttu-id="3e79b-124">创建策略时，你可以指定允许的值的列表。</span><span class="sxs-lookup"><span data-stu-id="3e79b-124">You can specify a list of allowed values when creating the policy.</span></span> <span data-ttu-id="3e79b-125">下面的示例将仅成功执行员工的员工数是 1、 2、 3、 4 或 5。</span><span class="sxs-lookup"><span data-stu-id="3e79b-125">The following example would only succeed for employees whose employee number was 1, 2, 3, 4 or 5.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("Founders", policy =>
                          policy.RequireClaim("EmployeeNumber", "1", "2", "3", "4", "5"));
    });
}
```

## <a name="multiple-policy-evaluation"></a><span data-ttu-id="3e79b-126">多个策略评估</span><span class="sxs-lookup"><span data-stu-id="3e79b-126">Multiple Policy Evaluation</span></span>

<span data-ttu-id="3e79b-127">如果将多个策略应用到的控制器或操作，然后授予访问权限之前也必须传递所有策略。</span><span class="sxs-lookup"><span data-stu-id="3e79b-127">If you apply multiple policies to a controller or action, then all policies must pass before access is granted.</span></span> <span data-ttu-id="3e79b-128">例如:</span><span class="sxs-lookup"><span data-stu-id="3e79b-128">For example:</span></span>

```csharp
[Authorize(Policy = "EmployeeOnly")]
public class SalaryController : Controller
{
    public ActionResult Payslip()
    {
    }

    [Authorize(Policy = "HumanResources")]
    public ActionResult UpdateSalary()
    {
    }
}
```

<span data-ttu-id="3e79b-129">在上例中任何标识了满足`EmployeeOnly`策略可以访问`Payslip`在控制器上强制执行该策略的操作。</span><span class="sxs-lookup"><span data-stu-id="3e79b-129">In the above example any identity which fulfills the `EmployeeOnly` policy can access the `Payslip` action as that policy is enforced on the controller.</span></span> <span data-ttu-id="3e79b-130">但是为了调用`UpdateSalary`标识必须满足的操作*同时*`EmployeeOnly`策略和`HumanResources`策略。</span><span class="sxs-lookup"><span data-stu-id="3e79b-130">However in order to call the `UpdateSalary` action the identity must fulfill *both* the `EmployeeOnly` policy and the `HumanResources` policy.</span></span>

<span data-ttu-id="3e79b-131">如果你希望更复杂的策略，如将出生声明的日期，计算年龄字段从它，然后检查年龄为 21 或更低版本，则需要编写[自定义策略处理程序](policies.md)。</span><span class="sxs-lookup"><span data-stu-id="3e79b-131">If you want more complicated policies, such as taking a date of birth claim, calculating an age from it then checking the age is 21 or older then you need to write [custom policy handlers](policies.md).</span></span>