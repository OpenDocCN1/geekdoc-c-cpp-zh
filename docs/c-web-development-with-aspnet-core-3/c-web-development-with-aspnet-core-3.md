
# ASP.NET Core 3 C# Web 开发

这是一份详细的教程，涵盖了 Visual Studio、Entity Framework 和 Blazor 的最新功能，并以逐步的方式呈现。

## 作者

Katie Millie

## 目录

### 第一章

### 第二章

### 第三章

### 第四章

### Razor Pages：简化 Web 开发

### 第五章

### 第六章

### 第七章

### 第八章

### 将 ASP.NET Core 3 部署到不同的环境

### 第九章

### 第

### 附录

## 引言

释放你体内的 Web 开发动力：精通 C# & ASP.NET Core 3，构建令人兴奋的动态网站！

网络是一个活生生的实体，不断进化并对创新解决方案提出需求。你准备好站在这一演化的前沿，打造捕捉用户并突破可能边界的交互式网络体验了吗？

《使用 ASP.NET Core 3 进行 C# Web 开发》是你通往 Web 开发大师的发射平台。这本书不仅仅是一本技术手册——它是你互动式的编程之旅，旨在将你从一个好奇的学习者转变为一个自信的 Web 开发者。无论你是初学者，还是想要提升技能的资深程序员，这本书都为你提供了业界所需的工具和技术，帮助你构建当今企业追求的强大、高性能 Web 应用程序。

为什么选择 C# & ASP.NET Core 3？这是你的优势：

- **轻松学习**：忘记复杂的术语和枯燥的讲座。我们将 C# 基础知识和 ASP.NET Core 概念拆解为易于接受、易于理解的课程，配有清晰的解释和引人注目的视觉效果。
- **实战掌握**：这不是一本被动阅读的书——而是一本让你积极编写代码的书。你从第一天就开始编写代码，构建吸引人的项目，以巩固你的理解并点燃你对 Web 开发的热情。
- **在做中学习**：我们相信实践的力量。你不仅是在学习理论——还将通过解决现实世界的编程挑战，掌握数据处理、用户交互和 Web API 集成等核心概念。
- **现代应用程序的现代开发**：ASP.NET Core 3 是驱动当今一些创新 Web 应用程序的尖端框架。这本书确保你掌握了构建性能、可扩展且安全的网络体验的最新工具和最佳实践。

但益处远不止代码：

- **解决问题能力**：编程可以了你的批判性思维和解决问题的能力，这在任何职业中都是宝贵的资产。
- **逻辑推理**：将问题分解为更小的、可解决的步骤——这种技能适用于生活的各个方面。
- **沟通大师**：清晰简洁的沟通对于编写代码和记录文档至关重要。
- **兴奋的职业机会**：C# 和 ASP.NET Core 3 是不断增长的 Web 开发行业中需求量极大的技能，开启了职业前景。

书中等待着你的是：

- 掌握 C# 基础知识，包括变量、数据类型、控制流和函数。
- 发挥 ASP.NET Core 3 的力量，利用其丰富的工具和功能进行现代 Web 开发。
- 构建具有用户友好界面、交互元素和数据集成的动态 Web 应用程序。
- 探索高级主题（可选章节），如 Web API、安全最佳实践和部署策略。
- 通过构建吸引人的项目释放你的创造力，展示你新学到的技能。

不要只是浏览网络——构建它！通过《使用 ASP.NET Core 3 进行 C# Web 开发》，你将拥有技能和信心，将你的 Web 开发梦想变为惊人的现实。向上滚动，点击“加入购物车”，从今天开始你的编程之旅！网络的未来等待着你。

```csharp
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
    }

    public void Configure(IApplicationBuilder app)
    {
        app.UseMvc();
    }
}
```

## ASP.NET Core 的主要优势

### 2. 性能与可扩展性

ASP.NET Core 为性能而构建，具有诸如内置异步编程支持和轻级 HTTP 请求处理等特性。这使得开发者能够构建可以处理大量并发用户并随需求增长轻松扩展的 Web 应用。

```csharp
public async Task<IActionResult> Index()
{
    var products = await _productService.GetProductsAsync();
    return View(products);
}
```

### 3. 安全性

安全在 Web 开发中至关重要，ASP.NET Core 提供了内置的安全功能，帮助开发者保护应用程序免受常见的安全风险，如跨站脚本（XSS）、跨站请求伪造（CSRF）和 SQL 注入。

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> Create(ProductViewModel model)
{
    if (ModelState.IsValid)
    {
        await _productService.CreateProductAsync(model);
        return RedirectToAction(nameof(Index));
    }
    return View(model);
}
```

### 4. 现代开发工作流

ASP.NET Core 带有现代化的开发工作流，包括内置依赖注入、中间件管道以及对 Visual Studio 和 Visual Studio Code 等流行开发工具的支持。这使开发者能够编写整洁、可维护的代码，并简化他们的开发流程。

```csharp
public class ProductService : IProductService
{
    private readonly ApplicationDbContext _context;

    public ProductService(ApplicationDbContext context)
    {
        _context = context;
    }

    public async Task<IEnumerable<Product>> GetProductsAsync()
    {
        return await _context.Products.ToListAsync();
    }
}
```

### 5. 社区与支持

ASP.NET Core 拥有一个活跃的开发者社区，他们贡献开源项目、分享知识和最佳实践，并为其他开发者提供支持。这种社区驱动的方法确保了开发者能够获得丰富的资源和专业知识，帮助他们在 Web 开发之旅中取得成功。

使用 ASP.NET Core 进行 Web 开发为开发者提供了一个构建现代 Web 应用的强大且多功能的平台。无论你是寻求扩展技能树的资深开发者，还是对学习 Web 开发感兴趣的新手，ASP.NET Core 都能提供一个坚实的基础，让你的想法在 Web 上变为现实。

## 探索 Web 开发版图：技术概览

Web 开发是一个不断演变的领域，为开发者提供了大量的技术。在本次探索中，我们将深入探讨 Web 开发领域，特别关注使用 ASP.NET Core 3 进行 C# Web 开发。ASP.NET Core 是一个使用 C# 构建现代、可扩展和高性能 Web 应用的流行框架。让我们仔细观察该生态系统中的一些关键方面和技术。

### ASP.NET Core 3 概述

ASP.NET Core 是一个用于使用 .NET 构建 Web 和服务的开源、跨平台框架。它为构建 Web API、Web 应用和微服务提供了统一的编程模型。ASP.NET Core 3 带来了多项改进和新功能，包括增强性能、对 gRPC 的支持、Blazor 更新以及改进的身份验证和授权机制。

```csharp
// 简单的 ASP.NET Core 3 控制器示例

using Microsoft.AspNetCore.Mvc;

[Route("api/{controller}")]
[ApiController]
public class HomeController : ControllerBase
{
    [HttpGet]
    public ActionResult<string> Get()
    {
        return "Hello, World!";
    }
}
```

### C# 与 ASP.NET Core MVC

ASP.NET Core MVC 是一个遵循模型-视图-控制器（MVC）架构模式构建 Web 应用的强大框架。它允许开发者分离关注点，使得代码的管理和维护变得更加容易。

```csharp
// ASP.NET Core MVC 控制器示例

using Microsoft.AspNetCore.Mvc;

public class HomeController : Controller
{
    public IActionResult Index()
    {
      return View();
    }
}
```

### Entity Framework Core

Entity Framework Core (EF Core) 是著名的 Entity Framework 数据访问技术的精简版、可定制且多功能的迭代版本，兼容多个平台。它允许开发者使用面向对象的技术来处理数据，简化了数据访问和持久化。

```csharp
// 使用 Entity Framework Core 定义模型的示例

using System.ComponentModel.DataAnnotations;

public class Product
{
    public int Id { get; set; }

    [Required]
    public string Name { get; set; }

    public decimal Price { get; set; }
}
```

### Razor Pages

Razor Pages 是 ASP.NET Core 引入的一个新功能，使构建 Web UI 变得简单高效。它允许开发者使用更少的代码，利用 Razor 模板语法创建动态 Web 页面。

```html
<!-- Razor Page 示例 -->

@page
@model IndexModel
@{
  ViewData["Title"] = "Home";
}

<h1>@ViewData["Title"]</h1>

<p>欢迎来到 ASP.NET Core!</p>
```

### SignalR

SignalR 是一个用于 ASP.NET Core 的实时通信库，能够实现客户端与服务器之间的双向通信。它简化了聊天应用程序、实时更新和通知的实现。

```csharp
// 在 ASP.NET Core 中使用 SignalR 示例

using Microsoft.AspNetCore.SignalR;

public class ChatHub : Hub
{
  public async Task SendMessage(string user, string message)
  {
    await Clients.All.SendAsync("ReceiveMessage", user, message);
  }
}
```

```html
@ViewData["Title"]

<p>欢迎访问我们的网站！</p>
```

## 中间件管道（Middleware Pipeline）

ASP.NET Core 中的管道管道允许开发者配置一系列中间件组件，用于处理 HTTP 请求和响应。这允许开发者以模块化和可重用的方式将身份验证、日志记录和错误管理等全局考虑整合到应用程序中。

```csharp
// 在 ASP.NET Core 中向管道添加中间件的示例

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    app.UseHttpsRedirection();
    app.UseStaticFiles();
    app.UseRouting();
    app.UseAuthentication();
    app.UseAuthorization();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapRazorPages();
    });
}
```

## Entity Framework Core

Entity Framework Core 提供了广泛使用的 Entity Framework 数据访问技术的轻量级且适应性版本。它提供了一个强大的对象关系映射 (ORM) 框架，简化了 ASP.NET Core 应用程序中的数据访问和持久化。

```csharp
// 使用 Entity Framework Core 定义模型的示例

public class Product
{
    Identifier as an integer { get; set; }
    Name as a string { get; set; }
    Price in decimal format { get; set; }
}
```

C# 和 ASP.NET Core 3 为开发者构建出色的网站提供了一套全面的工具集。从 C# 语言的简单性和表现力，到 ASP.NET Core 3 的强大功能（如 Razor Pages、中间件管道和 Entity Framework Core），开发者拥有创建现代、可扩展和高性能 Web 应用程序所需的一切。有了这些工具，打造卓越网络体验的可能性几乎是无尽的。因此，无论你是在构建个人博客、电子商务平台，还是复杂的企业级应用程序，C# 和 ASP.NET Core 3 都是你通往卓越 Web 开发之旅的可靠伴侣。

## 设置你的开发环境：准备好编码！

设置一个健壮的开发环境对于任何 Web 开发人员来说至关重要，特别是在使用 C# 和 ASP.NET Core 3 等技术时。在本指南中，我们将介绍如何有效地设置你的开发环境，确保你拥有所有所需的工具和配置，以信心地开始编码。

### 步骤 1：安装 Visual Studio IDE

Visual Studio 是一个强大的集成开发环境 (IDE)，用于使用 C# 和 ASP.NET Core 构建 Web 应用程序。它提供了一套全面的工具，包括代码编辑、调试和项目管理功能。

1. **下载 Visual Studio**：前往官方 [Visual Studio 网站](https://visualstudio.microsoft.com/downloads/) 并下载最新版本的 Visual Studio IDE。
2. **安装 Visual Studio**：运行下载的安装程序，并按照屏幕指令在你的机器上安装 Visual Studio。安装时，确保选择了“.NET 桌面开发”和“ASP.NET 和 Web 开发”工作负载。
3. **更新 Visual Studio**：安装后，启动 Visual Studio，通过导航到 **工具 > 选项 > 环境 > 扩展 > 更新** 来检查任何更新。

### 步骤 2：安装 .NET Core SDK

.NET Core SDK 是构建和运行 .NET Core 应用程序（包括 ASP.NET Core Web 项目）必不可少的。

1. **下载 .NET Core SDK**：访问官方 [.NET 网站](https://dotnet.microsoft.com/download/) 并下载与你的操作系统兼容的最新版 .NET Core SDK。
2. **安装 .NET Core SDK**：运行下载的安装程序并按照提供的说明进行操作。
3. **验证安装**：打开命令提示符或终端并输入 `dotnet --version` 以验证 .NET Core SDK 是否成功安装。

### 步骤 3：初始化 ASP.NET Core 项目

现在你已经安装了 Visual Studio 和 .NET Core SDK，让我们创建一个新的 ASP.NET Core 项目来开始 Web 开发。

1. **打开 Visual Studio**：启动 Visual Studio IDE。
2. **创建新项目**：从菜单中选择文件 > 新建 > 项目。
3. **选择项目**：选择 ASP.NET Core Web App (Model-View-Controller)。
4. **配置项目**：输入项目名称和位置。
5. **附加信息**：选择 .NET 框架版本。
6. **创建**：点击“创建”并等待项目加载。

### 步骤 4：运行你的 ASP.NET Core

现在你已经创建了项目，让我们运行它来验证一切。

1. **编译**：按 Ctrl+B 生成解决方案。
2. **运行**：按 F5 开始调试应用程序。
3. **验证应用程序**：你的默认浏览器将自动打开并显示主页。

### 步骤 5：探索你的项目结构

在深入编码之前，让我们快速浏览一下项目结构。

1. **解决方案管理器 (Solution Explorer)**：在解决方案管理器中，你会找到所有的文件和文件夹。
2. **Controllers（控制器）**：`Controllers` 文件夹包含处理请求的类。
3. **Views（视图）**：`Views` 文件夹包含渲染 HTML 的 Razor 视图。
4. **Models（模型）**：`Models` 文件夹包含数据实体。



# 第 2 章

## 理解构建块：变量、数据类型和运算符

在 C# 和 ASP.NET Core 3 Web 开发的世界中，掌握变量、数据类型和运算符的基础知识至关重要。这些构建块构成了代码的基础，并使你能够有效地处理数据。让我们深入了解每一个概念，并探索它们如何为你的开发之旅做出贡献。

### 变量

变量是占位符，用于存储在程序执行过程中可能会更改的数据。它们拥有名称、数据类型和值。

```csharp
// 在 C# 中声明变量的示例
int age = 25;
string name = "John Doe";
double salary = 2500.50;
bool isEmployed = true;
```

在上述示例中：

- `age` 是一个存储值为 25 的整数变量。
- `name` 是一个存储值为 "John Doe" 的字符串变量。
- `salary` 是一个存储值为 2500.50 的双精度浮点数变量。
- `isEmployed` 是一个存储布尔值的布尔变量。

变量允许你在 ASP.NET Core 应用程序中动态地管理和操作数据。

### 数据类型

数据类型规定了变量能够存储的数据种类。C# 支持多种数据类型，包括原始类型、结构化类型和用户定义类型。

#### 原始类型

原始类型是内建于 C# 语言中的基础数据类型。它们包括整数、浮点数、字符和布尔值。

```csharp
// C# 中原始数据类型的示例
int age = 25; // 整数
double salary = 2500.50; // 双精度浮点数
char grade = 'A'; // 字符
bool isEmployed = true; // 布尔
```

#### 结构化类型

结构化类型由多个原始类型或其他结构化类型组成。示例包括数组、枚举和结构体（`struct`）。

```csharp
// C# 中结构化数据类型的示例
int[] numbers = { 1, 2, 3, 4, 5 }; // 数组
enum Days { Monday, Tuesday, Wednesday, Thursday, Friday }; // 枚举
struct Point { int x; int y; }; // 结构体
```

#### 用户定义类型

用户定义类型是程序员创建的类型。它们包括类和接口，这是面向对象编程的基础。

```csharp
// C# 中用户定义数据类型的示例
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

interface IEmployee
{
    void CalculateSalary();
}
```

### 运算符

运算符是用于对变量和值执行操作的符号或关键字。C# 支持广泛的运算符，包括算术、比较、逻辑、赋值和位运算符。

#### 算术运算符

算术运算符用于执行加、减、乘、除和取模等数学操作。

```csharp
// C# 中算术运算符的示例
int a = 10;
int b = 5;
int sum = a + b; // 加
int difference = a - b; // 减
int product = a * b; // 乘
int quotient = a / b; // 除
int remainder = a % b; // 取模
```

#### 比较运算符

比较运算符用于比较两个值并确定它们的关系，返回一个布尔值（`true` 或 `false`）。

```csharp
// C# 中比较运算符的示例
int x = 10;
int y = 5;
bool isEqual = x == y; // 等于
bool notEqual = x != y; // 不等于
bool isGreater = x > y; // 大于
bool isLess = x < y; // 小于
bool isGreaterOrEqual = x >= y; // 大于等于
bool isLessOrEqual = x <= y; // 小于
```

#### 逻辑运算符

逻辑运算符用于组合多个条件，并评估给定的表达式为真为假。

```csharp
// C# 中逻辑运算符的示例
bool isAdult = age >= 18 && isEmployed; // 与
bool hasDiscount = age < 12 || age >= 65; // 或
bool isValid = !isValid; // 非
```

#### 赋值运算符

赋值运算符用于为变量赋值。

```csharp
// C# 中赋值运算符的示例
int a = 10;
int b = 5;
a += b; // 等于：a = a + b;
b -= a; // 等于：b = b - a;
```

理解变量、数据类型和运算符是精通 C# 和 ASP.NET Core 3 Web 开发的基础。通过掌握这些构建块，你获得了在你的应用程序中操作数据、创建逻辑表达式和执行操作的能力。有了这个坚实的基础，你完全能够应对更高级的概念并自信地构建复杂的解决方案。

## 掌握控制流：做出决策

控制流结构是 C# 和 ASP.NET Core 3 Web 开发中的基本元素，允许开发者控制代码的执行流。通过掌握控制流，你获得了做出决策、对集合进行迭代以及根据特定条件执行代码的能力。

### 条件语句

```csharp
// C# 中条件语句的示例
int age = 25;

if (age < 18)
{
    Console.WriteLine("你未成年。");
}
else if (age >= 18 && age < 65)
{
    Console.WriteLine("你是成年人。");
}
else
{
    Console.WriteLine("你是老年人。");
}
```

在上述示例中，`if` 语句检查 `age` 变量是否小于 18。如果为真，它打印“你未成年。”。`else if` 语句检查年龄是否在 18 到 65 之间。`else` 则打印“你是老年人。”

### 循环

循环允许你重复执行代码块，直到满足特定条件。C# 支持多种类型的循环，包括 `for`、`while` 和 `do-while`。

```csharp
// C# 中循环的示例
for (int i = 0; i < 5; i++)
{
    Console.WriteLine("Iteration: " + i);
}

int j = 0;
while (j < 5)
{
    Console.WriteLine("Iteration: " + j);
    j++;
}

int k = 0;
do
{
    Console.WriteLine("Iteration: " + k);
    k++;
} while (k < 5);
```

### 控制流关键字

C# 提供了诸如 `break`、`continue` 和 `return` 等控制流关键字来操作执行流。

```csharp
// C# 中控制流关键字的示例
for (int i = 0; i < 10; i++)
{
    if (i == 5)
    {
        break; // 退出循环
    }
    if (i % 2 == 0)
    {
        continue; // 跳过当前迭代
    }
    Console.WriteLine("Number: " + i);
}

bool IsPositive(int num)
{
    if (num >= 0)
    {
        return true; // 如果数字为正则返回真
    }
    return false; // 否则返回假
}
```

在上述示例中，`break` 关键字在 `i` 达到 5 时退出循环。`continue` 关键字跳过偶数。在 `IsPositive` 方法中，`return` 关键字根据特定条件返回布尔值。

## 函数

C# 中的函数可以有零或多个参数，这些参数是调用函数时传递给函数的值的占位符。此外，函数可以有一个返回类型，用于指定函数返回的值的类型。

```csharp
// C# 中带有参数和返回类型的函数示例
public int Multiply(int x, int y)
{
    return x * y;
}
```

在上面的示例中，`Multiply` 函数接收两个整数参数 `x` 和 `y` 并返回它们的乘积。

### 空函数（Void Functions）

返回类型为 `void` 的函数不返回任何值。它们用于执行某项任务或操作，而不返回结果。

```csharp
// C# 中空函数的示例
public void PrintMessage(string message)
{
    Console.WriteLine("Message: " + message);
}
```

在上面的示例中，`PrintMessage` 函数接收一个字符串参数 `message` 并将其打印到控制台，而不返回任何值。

### 函数的优势

1. 代码复用：函数允许封装可以在应用程序中重复使用的逻辑，减少了代码冗余并增强了可维护性。
2. 模块化：将复杂逻辑拆分为较小的、模块化的函数使得代码更容易理解和管理，促进了协作和团队工作。
3. 抽象：函数提供了一层抽象，允许开发者关注高级功能，而不必担心实现细节。
4. 测试：函数可以独立进行单元测试，确保每项功能的行为都符合预期，从而编写更健壮、更可靠的代码。

函数是 C# 和 ASP.NET Core 3 Web 开发中基本的构建块，使开发者能够创建可复用、模块化且高效的代码。通过定义具有良好参数和返回类型的函数，你可以封装逻辑、促进代码复用并提高代码的可维护性。无论是在执行简单的算术运算还是实现复杂的业务逻辑，函数都能让你编写出整洁、简洁且可扩展的代码，满足 Web 应用程序的需求。

## 整合一切：构建你的第一个 C# 程序

现在我们已经涵盖了 C# 和 ASP.NET Core 3 Web 开发的基础构建块，是时候通过构建你的第一个 C# 程序来将一切付诸实践了。在本指南中，我们将介绍创建两个简单程序的过程：一个控制台应用程序和一个基础 ASP.NET Core Web 应用程序。

### 构建控制台应用程序

让我们从创建一个简单的控制台应用程序开始，计算用户输入的两个数字之和。

#### 1. 生成 ASP.NET Core 应用程序项目

打开 Visual Studio 并选择 File > Project。在 C# 类别下选择 Console App (.NET Core) 模板。命名项目并点击 Create。

#### 2. 定义 Main 函数

在 `Program.cs` 文件中定义 `Main` 函数，作为程序的入口。

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter two numbers:");
        int num1 = Convert.ToInt32(Console.ReadLine());
        int num2 = Convert.ToInt32(Console.ReadLine());
        int sum = num1 + num2;

        Console.WriteLine("Sum: " + sum);
    }
}
```

#### 3. 运行控制台应用程序

按下 `F5` 或选择 **Debug > Start Debugging**。按照提示输入两个数字，程序将计算它们的和。

### 构建 ASP.NET Core Web 应用程序

接下来，让我们创建一个显示欢迎消息的基础 ASP.NET Core Web 应用程序。

#### 1. 创建 ASP.NET Core Web 应用程序项目

打开 Visual Studio 并选择 File > Project。在 C# 类别下选择 ASP.NET Core Web Application。命名项目并点击 Create。

#### 2. 定义带有视图的控制器

在 `Controllers` 文件夹中添加一个新的控制器类，并定义一个处理请求的方法。

```csharp
using Microsoft.AspNetCore.Mvc;

public class HomeController : Controller
{
    public IActionResult Index()
    {
        ViewData["Message"] = "Welcome to my first ASP.NET Core web application!";
        return View();
    }
}
```

#### 3. 创建视图

在 `Views` 文件夹中添加名为 `Index.cshtml` 的新视图并显示欢迎消息。

```html
@model dynamic

<h1>Welcome</h1>

<p>@ViewData["Message"]</p>
```

#### 4. 配置路由

打开 `Startup.cs` 文件并配置路由，将请求映射到相应的控制器和方法。

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllersWithViews();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }
        app.UseRouting();
        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllerRoute(
                name: "default",
                pattern: "{controller=Home}/{action=Index}/{id?}");
        });
    }
}
```

#### 5. 运行 ASP.NET Core Web 应用程序

按下 `F5` 或选择 **Debug > Start Debugging** 运行应用程序。浏览器应该打开并显示欢迎消息。恭喜！你成功创建了一个简单而实用的 ASP.NET Core Web 应用程序。

# 第 3 章

## ASP.NET Core 3 简介：使用 C# 构建 Web 应用程序

ASP.NET Core 3 是一个用于使用 C# 语言构建现代 Web 应用程序的强大且多功能的框架。它为开发者提供了一个跨平台、开源且高性能的健壮平台。在本指南中，我们将探索 ASP.NET Core 3 是什么，并深入研究其背后的框架。

### 什么是 ASP.NET Core 3？

ASP.NET Core 3 是 ASP.NET Core 框架的最新迭代，旨在解决不断发展的 Web 开发需求。它是一个使用 C# 构建程序的跨平台、高性能且开源的框架。ASP.NET Core 3 提供了广泛的功能和优势，包括：

1. 跨平台兼容性：ASP.NET Core 3 运行在 Windows、macOS 和 Linux 上，让开发者能够轻松地跨操作系统构建和部署 Web 应用程序。
2. 性能：与之前的版本相比，ASP.NET Core 3 在速度和扩展方面进行了优化。它利用现代 Web 开发技术和工具提供高性能的 Web 应用程序。
3. 模块化和活性：ASP.NET Core 3 的设计考虑了模块化，允许开发者仅选择和使用应用程序所需的组件和功能。这使得 Web 应用程序更加轻量和高效。
4. 开源：ASP.NET Core 3 是开源的，这意味着源代码供开发者自由查看、修改和贡献。这培养了活跃的开发者社区并促进了 ASP.NET 生态系统内的协作与创新。
5. 与 Visual Studio 集成：ASP.NET Core 3 与微软的集成开发环境（IDE）Visual Studio 无缝集成，为开发者提供了构建、调试和部署 Web 应用程序的丰富工具和功能。
6. 支持现代 Web 开发实践：ASP.NET Core 3 采用了 HTTP/2、WebSockets 和响应式设计等现代 Web 开发实践和标准，使开发者能够创建满足今天用户需求的尖端 Web 应用程序。

### 理解背后的框架

ASP.NET Core 3 的核心构建模块化且可扩展的架构之上，由各种组件和层组成，共同工作处理传入的 HTTP 请求、处理业务逻辑并生成响应。让我们探索 ASP.NET Core 3 框架的一些关键组件：

**5. wwwroot：** `wwwroot` 文件夹包含 CSS、JavaScript 和图像等静态文件。

**6. Startup.cs：** `Startup.cs` 文件是配置服务和中间件的入口点。

### 步骤 6：开始编码！

现在你的开发环境已就绪且 ASP.NET Core 项目已创建，你已经准备好开始编码了！



## ASP.NET Core 3 的核心概念

1. **中间件（Middleware）**：ASP.NET Core 3 中的中间件组件负责在 HTTP 请求和响应流过应用程序管道时对其进行处理。中间件组件可以执行路由、身份验证、日志记录和错误处理等任务。

2. **路由（Routing）**：ASP.NET Core 3 中的路由系统负责根据预定义的路由将传入的 HTTP 请求映射到相应的控制器和操作方法。路由使用路由模板定义，这些模板指定了 URL 的模式以及从中提取的参数。

```csharp
// ASP.NET Core 3 中的路由定义示例
endpoints.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

3. **控制器与操作（Controllers and Actions）**：控制器是用于处理传入的 HTTP 请求并生成响应的 C# 类。每个控制器包含一个或多个操作方法，这些方法代表应用程序中的单个端点。操作方法执行特定任务，例如检索数据、处理表单或渲染视图。

```csharp
// ASP.NET Core 3 中的控制器和操作方法示例

public class HomeController : Controller
{
    public IActionResult Index()
    {
        return View();
    }
}
```

4. **视图（Views）**：ASP.NET Core 3 中的视图负责渲染发送回客户端的 HTML 内容。视图通常使用 Razor 语法编写，它允许开发者在 HTML 标记中嵌入 C# 代码，以创建动态且具交互性的网页。

```html
<!-- ASP.NET Core 3 中的 Razor 视图文件示例 -->

@page

@model IndexModel

@{
    ViewData["Title"] = "Home";
}

<h1>@ViewData["Title"]</h1>

<p>欢迎来到我的 ASP.NET Core 3  应用程序</p>
```

5. **模型绑定（Model Binding）**：ASP.NET Core 3 中的模型绑定是将来自传入的 HTTP 请求中的数据映射到控制器操作方法参数的过程。模型绑定自动从查询字符串、表单字段、路由值和请求体中提取数据，并将其绑定到操作方法的相应参数。

```csharp
// ASP.NET Core 3 中的模型绑定示例
public IActionResult UpdateProduct(Product product)
{
    // 更新数据库中的产品
    return RedirectToAction("Index");
}
```

ASP.NET Core 3 是一个使用 C# 语言构建现代 Web 应用程序的多功能且强大的框架。凭借其跨平台兼容性、性能优化、模块化以及对现代 Web 开发实践的支持，ASP.NET Core 3 为开发者提供了一个全面的平台，用于创建高性能和可扩展的 Web 应用程序。通过理解魔法背后的框架，开发者可以充分利用 ASP.NET Core 3 的潜力，构建满足当今用户需求的健壮且功能丰富的 Web 应用程序。

## 探索项目结构：组织你的 Web 开发项目

在 ASP.NET Core 3 的 C# Web 开发领域，理解项目结构对于有效组织和管理代码库至关重要。良好的项目结构可以提高代码的质量。

ASP.NET Core Web 应用程序项目包含了构建和运行 Web 所需的所有组件，包括控制器、视图、模型和配置文件。

```plaintext
MyWebApp
| Controllers      <-- 控制器类
| Views            <-- Razor 视图文件
| Models           <-- 数据模型类
| wwwroot          <-- 静态文件 (CSS, JavaScript, images)
| appsettings.json <-- 应用程序设置
| Startup.cs       <-- 应用程序启动配置
L-- Program.cs      <-- 应用程序入口点
```

1. **控制器（Controllers）**：`Controllers` 文件夹包含负责处理传入 HTTP 请求并生成响应的控制器类。每个控制器通常由操作方法组成，这些方法代表应用程序中的单个端点。

2. **视图（Views）**：`Views` 文件夹包含负责渲染发送回客户端的 HTML 内容的 Razor 视图文件。视图通常包含结合了 Razor 语法的 C# 代码，以创建动态交互网页。

3. **模型（Models）**：`Models` 文件夹包含表示应用程序实体的数据模型类。模型定义了数据实体的结构和行为，包括属性、方法和关系。

4. **wwwroot**：`wwwroot` 文件夹包含直接提供给客户端的静态文件，如 CSS、JavaScript、图像和其他资源。这些文件可以通过浏览器中的相对路径访问。

5. **appsettings.json**：`appsettings.json` 文件包含应用程序设置和配置，例如数据库连接字符串、API 密钥和日志设置。它为管理应用程序设置提供了集中位置。

6. **Startup.cs**：`Startup.cs` 文件是 ASP.NET Core 应用程序中配置服务和中间件的入口点。它定义了应用程序的请求处理管道，并设置了路由、日志记录和依赖注入等服务。

7. **Program.cs**：`Program.cs` 文件作为应用程序的入口点，包含引导 ASP.NET Core 启动并配置 Web 主机的 `Main` 方法。

## 自定义项目结构

虽然 ASP.NET Core 3 提供的默认项目结构适用于许多 Web 应用程序，但开发者可以根据特定需求和偏好自定义并扩展项目结构。

- **区域（Areas）**：ASP.NET Core 允许开发者将相关功能组织到区域，每个区域都有自己的控制器、视图和模型。区域为组织大型应用程序提供了分级结构。
- **额外文件夹（Additional Folders）**：开发者可以在项目中创建额外的文件夹以进一步组织代码。常见示例包括服务、工具文件夹。
- **关注点分离（Separation of Concerns）**：遵循关注点分离原则，可以根据功能边界（如表示层、业务逻辑和数据访问）将代码组织到单独的项目或模块中。

它提供了一种结构化的代码组织代码的方法，使应用程序更容易理解、维护和扩展。在本指南中，我们将深入探讨模型-视图-控制器（MVC）模式及其在 ASP.NET Core 3 中的实现方式。

## 什么是模型-视图-控制器模式？

模型-视图-控制器（MVC）模式是一种软件架构设计，它将应用程序分为三个相互关联的元素：

1. **模型（Model）**：表示应用程序的数据和操作逻辑。它封装了应用程序的状态和行为，包括数据验证、操作和持久化。
2. **视图（View）**：代表应用程序的表示层。它负责渲染用户界面并向用户显示数据。视图通常是结合了嵌入代码的 HTML 模板。
3. **控制器（Controller）**：作为模型和视图之间的中间件。它通过视图接收用户输入，处理请求，与模型交互以执行业务逻辑，并选择合适的视图来渲染响应。

### 1. 模型（Model）

ASP.NET Core MVC 中的模型代表应用程序的数据和业务逻辑。它们通常被定义为类，封装了数据属性以及与数据交互的方法。

```csharp
// Example of a model class in ASP.NET Core MVC

public class Product
{
    // 这表示一个公共整数标识符 { get; set; }

    // 这表示一个公共字符串标识符 { get; set; }

    // 这代表一个公共的小进制值 { get; set; }
}
```

### 2. 视图（View）

ASP.NET Core MVC 中的视图负责渲染用户界面并向用户显示数据。它们通常使用 Razor 语法编写，该语法允许开发者在 HTML 标记中嵌入 C# 代码。

```html
<!-- Example of a Razor view file in ASP.NET Core MVC -->
@model MyWebApp.Models.Product
<h1>Product Details</h1>
<p>Name: @Model.Name</p>
<p>Price: @Model.Price</p>
```

### 3. 控制器（Controller）

ASP.NET Core MVC 中的控制器处理用户请求、处理数据并选择适当的视图来渲染响应。它们通常被定义为继承自 `Controller` 基类的类，并包含代表应用程序中各个端点的操作方法（action methods）。

```csharp
// Example of a controller class in ASP.NET Core MVC

public class ProductController : Controller
{
    private readonly ProductService _productService;

    public ProductController(ProductService productService)
    {
        _productService = productService;
    }

    public IActionResult Details(int id)
    {
        var product = _productService.GetProductById(id);
        if (product == null)
        {
            return NotFound();
        }
        return View(product);
    }
}
```

## ASP.NET Core MVC 的优势

在 ASP.NET Core 中实现 MVC 模式具有以下几个优势：

- **关注点分离（Separation of Concerns）**：MVC 将数据、演示和用户交互分离，使得代码更容易管理维护。
- **模块化（Modularity）**：MVC 通过将代码组织成不同的组件促进模块化，允许开发者独立地处理应用程序的不同部分。
- **可测试性（Testability）**：MVC 通过允许对应用程序的单个组件（如控制器）进行单元测试来提高可测试性。
- **灵活性（Flexibility）**：MVC 提供了自定义应用程序各个组件的灵活性，允许开发者满足特定需求。

ASP.NET Core MVC 是一个使用 Model-View-Controller 模式构建现代 Web 应用的强大框架。通过将应用程序分为三个关联的组件——模型、视图和控制器——它促进了代码组织、关注点分离和可维护性。无论你是在构建小型应用程序还是企业级解决方案，ASP.NET Core MVC 都提供了轻松创建强大且扩展的 Web 应用所需的结构。

## 创建你的第一个 ASP.NET Core Web 应用

现在我们已经探索了 ASP.NET Core 开发的理论，让我们通过创建第一个 ASP.NET Core Web 应用将这些知识付诸实践。在本指南中，我们将创建一个显示欢迎信息的简单 Web 应用。

### 步骤 1：创建一个 ASP.NET Core Web 项目

1. 打开 Visual Studio。
2. 选择文件 > 新 > 项目。
3. 从模板列表中选择 ASP.NET Core Web。
4. 为你的项目命名并点击创建。
5. 选择 ASP.NET Core 3.x 作为目标框架。
6. 选择 Web（Model-View-Controller）模板并点击创建。

### 步骤 2：定义带有操作方法的控制器

1. 在解决方案管理器中，展开`Controllers`文件夹。
2. 右键点击文件夹并选择添加 > 控制器。
3. 选择 MVC 控制器 - 空并点击添加。
4. 为控制器命名（例如 `HomeController`）并点击添加。
5. 在控制器内定义操作方法以处理请求并返回视图。

```csharp
// HomeController.cs
using Microsoft.AspNetCore.Mvc;

public class HomeController : Controller
{
    public IActionResult Index()
    {
        ViewData["Message"] = "Welcome to my first ASP.NET Core web application!";
        return View();
    }
}
```

### 步骤 3：创建一个显示欢迎信息的视图

1. 在解决方案管理器中，打开`Views`目录。
2. 在`Home`文件夹内部，右键并选择添加 > 视图。
3. 为视图命名（例如 `Index`）并点击添加。
4. 编写 HTML 标记来显示欢迎信息。

```html
<!-- Index.cshtml -->
@{
  ViewData["Title"] = "Home";
}

<h1>Welcome</h1>

<p>@ViewData["Message"]</p>
```

### 步骤 4：在 Startup.cs 中配置路由

1. 打开 `Startup.cs` 文件。
2. 在 `Configure` 方法中，配置路由将请求映射到适当的控制器和操作方法。

```csharp
// Startup.cs
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.DependencyInjection;

public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllersWithViews();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperPage();
        }

        app.UseRouting();
        app.UseEndpoints(endpoints => {
          endpoints.MapControllerRoute(
            name: "default",
            pattern: "{controller=Home}/{action=Index}/{id?}"
          );
        });
    }
}
```

### 步骤 5：运行你的 ASP.NET Core Web 应用

1. 按 `F5` 或选择调试来运行应用程序。
2. 网页浏览器会自动打开并显示来自你的 ASP.NET Core Web 应用的欢迎信息。

恭喜！你成功地使用 Model-View-Controller 模式创建了第一个 Core Web 应用。通过定义控制器、视图和路由，你构建了一个简单的功能性应用程序。这只是你进入 ASP.NET Core Web 开发之旅的开始，随着你继续构建和增强 Web 应用，还有更多可以探索和学习的内容。编码愉快！

# 第 4 章

## 使用 Razor Pages：简化 Web 开发

Razor Pages 是 ASP.NET Core 的一个功能，它通过提供更精简的页面构建方法来简化 Web 应用程序的开发。通过 Razor Pages，开发者可以在单个文件中创建包含 HTML 标记和 C# 代码的页面，使得复杂的 Web 应用更容易管理和维护。在本指南中，我们将探索 Razor Pages 的基础，并演示如何利用这一强大模型在 ASP.NET Core 3 中构建动态页面。

### Razor Pages 简介

Razor Pages 是引入 ASP.NET Core 的轻量级 Web 框架，它构建在 MVC（模型-视图-控制器）架构之上。虽然 MVC 将应用程序拆分为三个主要组件（模型、视图和控制器），但 Razor Pages 将视图和控制器合并到单个页面中，从而带来了更贯贯直观的开发体验。

### Razor Page 的结构

一个 Razor Page 由两个主要部分组成：HTML 标记和相关的 C# 代码。让我们拆解 Razor Page 的结构：

1. **HTML 标记**：HTML 标记定义了 Web 页的结构和布局，包括标题、段落、表单和按钮等元素。Razor Pages 使用`.cshtml`扩展名来表示它们包含了 HTML 标记和 C# 代码。

```html
<!-- Example of HTML markup in a Razor Page -->

@page
@model MyWebApp.Pages.IndexModel

<!DOCTYPE html>
<html>
<head>
<title>My Razor Page</title>
</head>
<body>
<h1>Welcome</h1>
</body>
</html>
```

<p>@Model.Message</p>

</body>

</</html>

2. **C# 代码**：Razor Page 中的 C# 代码被封装在`@{ }`块中，用于定义页面的行为、处理用户输入以及与数据交互。



```csharp
// Example of C# code in a Razor Page

using Microsoft.AspNetCore.Mvc.RazorPages;

namespace MyWebApp.Pages
{
    public class IndexModel : PageModel
    {
        public string Message { get; set; }

        public void OnGet()
        {
            Message = "Hello, Razor Pages!";
        }
    }
}
```

在上面的示例中，`Index.cshtml` Razor Page 包含了 HTML 标记和 C# 代码。文件顶部的 `@page` 指令表示它是一个 Razor Page，而 `@model` 指令指定了与页面关联的模型类型。

## Razor Pages 的核心概念

**1. 页面模型 (Page Model)：** 页面模型是一个 C# 类，充当 Razor Page 的控制器。它包含了定义页面行为、处理 HTTP 请求以及与数据交互的属性和方法。

**2. 路由 (Routing)：** Razor Pages 使用基于约定的路由系统将 URL 映射到页面处理程序。默认情况下，URL 路径对应于页面文件路径和名称。

**3. 处理器 (Handlers)：** 处理器是页面模型中的方法，用于响应 HTTP 请求并执行特定操作。例如，`OnGet()` 方法处理 HTTP GET 请求，而 `OnPost()` 则处理 HTTP POST 请求。

**4. 模型绑定 (Model Binding)：** Razor Pages 支持模型绑定，允许将来自 HTTP 请求的数据自动绑定到页面模型的属性上。这简化了处理用户输入和与数据交互的过程。

## Razor Pages 的优势

1. **简单性：** 与传统的 MVC 相比，Razor Pages 提供了更简单、直观的开发体验，因为它将视图（View）和控制器（Controller）合并到了页面中。

2. **减少模板代码：** 与 MVC 相比，使用 Razor Pages 需要的模板代码更少，使得代码更加整洁简洁。

3. **提高生产力：** Razor Pages 允许开发者更快、更高效地构建网页，减少了实现常用 Web 应用功能所需的时间和精力。

4. **提高可测试性：** Razor Pages 通过将页面行为封装在页面模型中提高了可测试性，使得单元测试页面功能变得更容易。

Razor Pages 是 ASP.NET Core 中一个强大且多功能的特性，简化了动态网页的开发。通过在单个文件中结合 HTML 标记和 C# 代码，Razor Pages 提供了更全面、更直观的开发体验，让开发者能够更快速地构建 Web 应用。无论你是构建简单的 CRUD（增删改查）应用程序还是具有复杂用户界面的 Web 应用，Razor Pages 都为 ASP.NET Core 3 提供了一种灵活且高效的 Web 开发方法。

## 使用 Razor Pages 创建交互式表单：处理用户输入

在 ASP.NET Core 3 中，Razor Pages 提供了一种方便的方法来创建交互式表单，允许用户输入数据并提交到服务器进行处理。你可以轻松地处理用户输入、验证表单数据并响应用户操作。在本指南中，我们将探索如何使用 Razor Pages 创建交互式表单并有效地处理用户输入。

## 在 Razor Pages 中创建表单

要在 Razor Pages 中创建表单，你需要在 Razor Page (`.cshtml` 文件) 中定义表单元素的 HTML 标记。你可以使用标准的 HTML 表单元素，如 `<input>`、`<textarea>` 和 `<select>` 来收集用户输入。

```html
<!-- Example of a form in a Razor Page -->
@page
@model MyWebApp.Pages.ContactModel

<form method="post">
    <div>
        <label for="name">Name:</label>
        <input type="text" id="name" name="Name" />
    </div>
    <div>
        <label for="email">Email:</label>
        <input type="email" id="email" name="Email" />
    </div>
    <div>
        <label for="message">Message:</label>
        <textarea id="message" name="Message"></textarea>
    </div>
    <button type="submit">Submit</button>
</form>
```

在上面的示例中，我们创建了一个简单的表单，包含用户姓名、电子邮件和消息字段。该表单配置为在用户点击“提交”（Submit）按钮时使用 HTTP POST 方法将数据提交到服务器。

## 在 Razor Pages 中处理表单提交

要在 Razor Pages 中处理表单提交，你需要在页面模型 (`.cshtml` 文件) 中定义一个对应的处理器方法。该处理器方法负责处理表单数据并响应用户的操作。

```csharp
// Example of handling form submissions in a Razor Page

using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;

namespace MyWebApp.Pages
{
    public class ContactModel : PageModel
    {
        [BindProperty]
        public ContactFormModel ContactForm { get; set; }

        public void OnGet()
        {
            // 初始化表单数据如果需要
        }

        public IActionResult OnPost()
        {
            if (!ModelState.IsValid)
            {
                return Page();
            }
            // 处理表单数据
            return RedirectToPage("Index");
        }
    }

    public class ContactFormModel
    {
        [Required(ErrorMessage = "Please enter your name")]
        public string Name { get; set; }

        [Required(ErrorMessage = "Please enter your email")]
        [EmailAddress(ErrorMessage = "Please enter a valid email address.")]
        public string Email { get; set; }

        [Required(ErrorMessage = "Please enter a message.")]
        public string Message { get; set; }
    }
}
```

```html
<!-- Razor Page 数据绑定的示例 -->

@page

@model MyWebApp.Pages.IndexModel
```

<h1>欢迎，@Model.UserName!</h1>

<p>您的电子邮箱地址是：@Model.UserEmail</p>

在上面的示例中，我们将页面模型（`IndexModel`）的 `UserName` 和 `UserEmail` 属性绑定到了 Razor Page 内部的 HTML 元素上。当页面渲染时，这些属性的值将动态地插入到相应的 HTML 元素中。

## 使用循环渲染数据

Razor Pages 支持如 `foreach` 和 `for` 循环等循环结构，允许您对数据集合进行迭代，并为集合中的每个项目动态渲染内容。

```html
<!-- Razor Page 中使用 foreach 循环渲染数据的示例 -->
@foreach (var item in Model.Items)
{
  <div>
    <h2>@item.Title</h2>
    <p>@item.Description</p>
  </div>
}
```

在上面的示例中，我们正在遍历一个项目集合（`Model.Items`），并使用 `@foreach` 循环为每个项目渲染 HTML 标记。这允许我们动态地显示带有标题和描述的项目列表。

### 条件渲染

Razor Pages 支持条件渲染，允许您根据某些条件显示或隐藏 HTML 元素。这对于根据用户输入或服务器端逻辑条件地显示内容非常有用。

```html
<!-- Razor Page 中条件渲染的示例 -->
@if (Model.IsAdmin)
{
    <p>欢迎，管理员！</p>
}
else
{
    <p>欢迎，用户！</p>
}
```

在上面的示例中，我们根据页面模型中 `IsAdmin` 属性的值条件地渲染欢迎消息。如果用户是管理员，我们显示一条欢迎其作为管理员的消息；否则，我们显示一条欢迎其作为普通用户的消息。

## 利用局部视图（Partial Views）

Razor Pages 支持局部视图，局部视图是可重用的 HTML 标记和 C# 代码分块，可以被包含在多个页面中。局部视图允许您对 UI 组件进行模块化，并促进应用程序不同部分之间的代码复用。

```html
<!-- 在 Razor Page 中使用局部视图的示例 -->
<div>
<h2>最近文章</h2>

@await Html.PartialAsync("_RecentPosts", Model.RecentPosts)
</div>
```

在上面的示例中，我们使用 `Html.PartialAsync` 方法在 Razor Page 中包含了一个名为 `_RecentPosts.cshtml` 的局部视图。该局部视图显示最近文章列表，并且可以在应用程序的多个页面中复用。

在 ASP.NET Core 3 中使用 Razor Pages 显示数据是简单且强大的。通过利用数据绑定、循环、条件渲染和局部视图，您可以创建动态且引人注目的界面，响应用户交互并以用户友好的方式显示数据。无论您是构建简单的 CRUD 应用程序还是具有复杂用户界面的 Web 应用程序，Razor Pages 都为显示数据和构建引人入胜的用户体验提供了灵活且直观的解决方案。

## 构建布局和局部视图：复用代码以一致的设计

在 ASP.NET Core 3 中，构建布局（Layouts）和局部视图（Partials）是创建一致且视觉良好的 Web 应用的关键。布局为页面提供了一致的结构，而局部视图允许在多个页面之间复用常用组件。在本指南中，我们将探索如何在 ASP.NET Core 3 中构建布局和局部视图，以创建一个协调且用户友好的设计。

## 在 ASP.NET Core 中创建布局

布局是一个共享模板，定义了 Web 应用中页面的整体结构和设计。布局通常包含常用元素，如页眉、页脚、导航菜单和动态内容的占位符。在 ASP.NET Core 中，布局使用 `_Layout.cshtml` 文件中的 Razor 语法定义。

```html
<!-- 布局的示例 -->
<!DOCTYPE html>
<html>
<head>
  <title>@ViewData["Title"] - 我的应用程序</title>
  <link rel="stylesheet" href="~/css/site.css" />
</head>
<body>
  <header>
    <h1>我的应用程序</h1>
    <nav>
      <ul>
        <li><a href="/">首页</a></li>
        <li><a href="/about">关于</a></li>
        <li><a href="/contact">联系</a></li>
      </ul>
    </nav>
  </header>
  <main>
    @RenderBody()
  </main>
  <footer>
    &copy; 2024 我的应用程序
  </footer>
</body>
</html>
```

在上面的示例中，我们定义了一个包含导航菜单、主内容区域和页脚的布局。`@RenderBody()` 函数用于在布局中显示特定页的内容。

## 用于复用组件的局部视图

局部视图是可重用的 HTML 标记和 C# 代码分块，可以包含在多个页面中。局部视图允许代码复用并促进应用程序不同部分的设计一致性。在 ASP.NET Core 中，局部视图在单独 `.cshtml` 文件中使用 Razor 语法定义。

```html
<!-- 局部视图的示例 -->
<!-- _RecentPosts.cshtml -->

@model List<Post>

<h2>最近文章</h2>

<ul>

@foreach (var post in Model)
{
<li>@post.Title</li>
}

</ul>
```

在上面的示例中，我们定义了一个名为 `_RecentPosts.cshtml` 的局部视图，它显示最近文章列表。该局部视图可以在需要显示的多个页面或布局中复用。

## 在布局或页面中包含局部视图

要在布局或页面中包含局部视图，您可以在 Razor 语法中使用 `Html.Partial` 或 `Html.PartialAsync` 方法。这允许您将局部视图的 HTML 标记和 C# 代码包含在父视图中。

```html
<!-- 在布局中包含局部视图的示例 -->
<!-- _Layout.cshtml -->

<!DOCTYPE html>
<html>
<head>
  <title>@ViewData["Title"] - 我的应用程序</title>
  <link rel="stylesheet" href="~/css/site.css" />
</head>
<body>
  <header>
    <h1>我的应用程序</h1>
    <nav>
      <ul>
        <li><a href="/">首页</a></li>
        <li><a href="/about">关于</a></li>
        <li><a href="/contact">联系</a></li>
      </ul>
    </nav>
  </header>
  <main>
    @RenderBody()
    @await Html.PartialAsync("_RecentPosts", Model.RecentPosts)
  </main>
  <footer>
    &copy; 2024 我的应用程序
  </footer>
</body>
</html>
```

在上面的示例中，我们使用 `Html.PartialAsync` 方法在布局的 `main` 内容区域内包含了 `_RecentPosts.cshtml` 局部视图。这允许我们在使用该布局的每个页面上显示最近文章。

要处理 ASP.NET Core 中的表单提交，你需要在控制器中定义相应的动作方法（action method）。该动作方法处理表单数据并执行所需的操作，例如将数据保存到数据库或发送电子邮件。

```csharp
// ASP.NET Core 处理表单提交的示例

[HttpPost]
public IActionResult FormHandler(string name, string email)
{
    // 处理表单数据并执行操作
    // 示例：保存数据到数据库，发送电子邮件

    return RedirectToAction("ThankYou");
}
```

在上面的示例中，我们在控制器中定义了一个名为 `FormHandler` 的 POST 动作方法。该方法接收与表单输入字段（`name` 和 `email`）对应的参数，并处理表单数据。在处理数据后，该方法使用 `RedirectToAction` 方法将用户重定向到“感谢”页面。

## ASP.NET Core 中的模型绑定（Model Binding）

ASP.NET Core 支持模型绑定，它可以根据命名规范自动将表单数据绑定到模型类的属性上。这简化了处理表单提交的过程，并减少了所需的样板代码量。

```csharp
// ASP.NET Core 模型绑定的示例
public class ContactFormModel
{
    public string Name { get; set; }
    public string Email { get; set; }
}
```

```csharp
[HttpPost]
public IActionResult FormHandler(ContactFormModel model)
{
    // 使用模型对象访问表单数据
    // 示例：string name = model.Name;

    return RedirectToAction("ThankYou");
}
```



在上面的示例中，我们定义了一个名为`ContactFormModel`的模型类，其属性与表单输入字段对应。`FormHandler`动作方法接收类型为`ContactFormModel`的参数，ASP.NET Core 会自动将表单数据绑定到该模型类的属性上。

## ASP.NET Core 中的表单验证（Form Validation）

ASP.NET Core 提供了内置的验证机制，可以使用数据注解（data annotations）或自定义验证逻辑来验证表单数据。这确保了用户提交的数据在处理之前是有效的，并且符合某些标准。

```csharp
// ASP.NET Core 表单验证插图

public class ContactUserModel
{
    [Required(ErrorMessage = "请输入您的姓名.")]
    public string Name { get; set; }

    [Required(ErrorMessage = "请输入您的电子邮件地址.")]
    [EmailAddress(ErrorMessage = "请输入有效的电子邮件地址.")]
    public string Email { get; set; }
}
```

在上面的示例中，我们为`ContactUserModel`类添加了数据注解，以为每个属性指定验证规则。这些注解对表单数据实施了约束，并在数据无效时显示错误消息。

理解 ASP.Net Core 3 中的表单对于获取用户数据和构建交互式 Web 应用程序至关重要。通过定义 HTML 表单、处理表单提交、利用模型绑定以及实现表单验证，你可以创建无缝的用户体验，并确保用户提交的数据是准确且有效的。无论你是构建简单的联系表单还是复杂的数据输入表单，ASP.NET Core 都提供了你所需的工具和能力来有效且安全地处理表单。

## 处理表单数据：验证和清洗用户输入

在 ASP.NET Core 3 中，处理表单数据不仅涉及捕用户输入，还涉及确保数据有效且经过清洗（sanitized），以防止安全漏洞。对用户输入进行适当的验证和清洗是构建安全可靠的 Web 应用程序的关键步骤。在本指南中，我们将探索如何在 ASP.Net Core 3 中处理表单数据，包括验证和清洗技术。

## 处理表单提交

当用户在网页上提交表单时，表单数据会被发送到服务器进行处理。在 ASP.NET Core 中，你可以通过在控制器中定义与表单提交生成的 HTTP POST 请求相对应的动作方法来处理表单提交。

```csharp
// ASP.NET Core 处理表单提交的示例

[HttpPost]
public IActionResult SubmitForm(string name, string email)
{
    // 处理表单数据

    // 示例：保存数据到数据库，发送电子邮件

    return RedirectToAction("ThankYou");
}
```

在上例示例中，我们在控制器中定义了一个名为`SubmitForm`的 POST 动作方法。该方法接收与表单输入字段（`name`和`email`）对应的参数，并处理表单数据。在处理数据后，该方法将用户重定向到“感谢”页面。

### 表单验证

表单验证涉及验证用户提供的信息是否正确并符合特定标准。ASP.NET Core 提供了内置的验证机制，允许你使用数据注解或自定义验证逻辑为表单输入字段定义验证规则。

```csharp
// ASP.NET Core 表单验证插图

public class ContactFormControl
{
    [Required(ErrorMessage = "请输入您的姓名.")]
    public string Name { get; set; }

    [Required(ErrorMessage = "请输入您的电子邮件地址.")]
    [EmailAddress(ErrorMessage = "请输入有效的电子邮件地址.")]
    public string Email { get; set; }
}
```

在上例示例中，我们定义了一个名为`ContactFormControl`的模型类，其属性与表单输入字段对应。我们还添加了数据注解（`[Required]`和`[EmailAddress]`）来为每个属性指定验证规则。这些注解对表单数据实施了约束，并在数据无效时显示错误消息。

## 清洗用户输入（Sanitizing User Input）

清洗用户输入是移除或编码潜在有害的字符或脚本的过程，以防止跨站脚本攻击（XSS）攻击等安全漏洞。ASP.NET Core 提供了清洗用户输入的内置机制，例如`HtmlEncoder`类。

```csharp
// ASP.NET Core 清洗用户输入的示例

public IActionResult SubmitForm(string name, string email)
{
    name = HtmlEncoder.Default.Encode(name);

    email = HtmlEncoder.Default.Encode(email);

    // 处理清洗后的表单数据

    // 示例：保存数据到数据库，发送电子邮件

    return RedirectToAction("ThankYou");
}
```

在上面的示例中，我们使用了`HtmlEncoder.Default.Encode`方法在处理表单数据之前对`name`和`email`变量进行清洗。这确保了任何潜在的字符或脚本都被正确编码，降低了 XSS 攻击的风险。

在 ASP.NET Core 3 中处理表单数据涉及验证和清洗用户输入，以确保 Web 应用程序的安全可靠。通过使用数据注解或自定义验证逻辑正确验证表单输入，你可以对用户提交的数据实施约束并为无效输入提供有意义的错误消息。此外，通过使用`HtmlEncoder`类等机制清洗用户输入，你可以防止安全漏洞并防御 XSS 攻击。通过将这些最佳实践纳入表单处理工作流，你可以构建出有效处理用户输入的安全强大的 Web 应用程序。

## 使用模型：用 C# 类表示你的数据

在 ASP.NET Core 3 中，模型在表示数据和定义应用程序领域对象的结构方面起着至关重要的作用。模型封装了数据实体的属性和行为，使得在整个应用程序中处理和操作数据变得更容易。在本指南中，我们将探索如何在 ASP.NET Core 3 中使用模型，包括创建模型类以及使用它们来表示数据。

## 创建模型类

ASP.NET Core 中的模型类是简单的 C# 类，用于表示应用程序中的数据实体。这些类通常包含表示实体属性的属性，例如名称、年龄、电子邮件等。让我们创建一个示例模型类来表示用户配置。

```csharp
// Example of a model class in ASP.NET Core

public class UserProfile
{
    // 这表示一个整数标识符
    public int Id { get; set; }
    // 这声明了一个字符串标识符
    public string Name { get; set; }
    // 这指定了年龄的整数标识符
    public int Age { get; set; }
    // 这表示了用于电子邮件地址的字符串标识符
    public string Email { get; set; }
}
```

在上面的示例中，我们定义了一个名为`UserProfile`的模型类，其属性表示用户配置的特质，包括`id`、`name`、`age`和`email`。每个属性都对应数据库中用户配置表中的一列。

## 使用模型表示数据

一旦你定义了模型类，就可以使用它们在整个应用程序中表示数据。模型作为创建数据实体实例的蓝图，允许你以结构化和组织化的方式处理和操作数据。

```csharp
// Example of using a model class in ASP.NET Core

public class UserController : Controller
{
    private readonly ApplicationDbContext _context;

    public UserController(ApplicationDbContext context)
    {
        _context = context;
    }

    public IActionResult UserProfile(int id)
    {
        UserProfile user = _context.UserProfiles.Find(id);
        return View(user);
    }
}
```

在上面的示例中，我们创建了一个`UserController`类，其中有一个名为`UserProfile`的操作方法。该方法使用提供的`id`从数据库中检索用户配置，并将其传递给视图进行渲染。`UserProfile`模型类用于表示从数据库检索的数据。

## 使用模型注解验证数据

模型注解提供了一种直接在模型类中为模型属性定义验证规则和约束的方法。ASP.NET Core 提供了内置的验证程序，你可以将它们应用于模型属性，以强制数据完整性并确保数据符合某些标准。

```csharp
// Example of model validation using annotations in ASP.NET Core

public class UserProfile
{
    public int Id { get; set; }

    [Required(ErrorMessage = "Please enter your name.")]
    public string Name { get; set; }

    [Range(18, 120, ErrorMessage="The age should fall within the range of 18 to 120.")]
    public int Age { get; set; }

    [EmailAddress(ErrorMessage = "Please enter a valid email address.")]
    public string Email { get; set; }
}
```

在上面的示例中，我们向`UserProfile`模型类的属性添加了数据注解（`Required`）、（`Range`）、（`EmailAddress`），以为每个属性定义验证规则。这些注解对数据实施了约束，并在数据不符合指定标准时显示错误消息。

在 ASP.NET Core 3 中处理模型对于表示数据实体和定义应用程序领域对象的结构至关重要。通过创建模型类来表示数据实体并在整个应用程序中使用它们，你可以确保数据是结构化、组织化且易于处理的。此外，通过应用模型注解来定义验证规则和约束，你可以强制数据完整性并确保数据符合某些标准。通过将这些最佳实践纳入应用程序的数据建模工作流，你可以构建出健壮且可靠的 Web 应用程序，有效地管理和操作数据。

## 持久化用户数据：Entity Framework Core 简介

在 ASP.NET Core 3 中，持久化用户数据是构建 Web 应用的基本方面。Entity Framework Core (EF Core) 是一种广泛的对象关系映射（ORM）框架，它可以简化 ASP.NET Core 应用程序中的数据库交互。在本指南中，我们将介绍 Entity Framework Core 并演示如何使用它在 ASP.NET Core 3 中持久化用户数据。

### 什么是 Entity Framework Core？

Entity Framework Core 是 Entity Framework 数据访问技术的一种灵活、适应且平台独立的迭代。它允许开发者使用领域特定对象处理数据，并为数据库交互提供了高层抽象。EF Core 支持多种数据库提供程序，包括 SQL Server、SQLite、MySQL、PostgreSQL 等。

### 设置 Entity Framework Core

要在 ASP.NET Core 3 应用程序中开始使用 EF Core，你需要安装必要的 NuGet 包，并配置 EF Core 与你选择的数据库提供程序工作。让我们以 SQL Server 为例。

一旦安装了所需的包，你可以在`Startup.cs`文件的`ConfigureServices`方法中配置 EF Core。

```csharp
// Startup.cs
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.DependencyInjection;
using YourAppName.Data;

public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
}
```

## 创建模型类

接下来，你需要定义模型类来表示数据库中的实体。这些模型类将被 Entity Framework Core 用于将数据库表映射到领域对象。

```csharp
// Example of a model class representing a profile
public class UserProfile
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
    public string Email { get; set; }
}
```

### 创建 DbContext

`DbContext`是协调特定数据模型 Entity Framework 功能的主类。它代表与数据库的会话，并允许你查询和保存数据。

```csharp
// Example of a DbContext
using Microsoft.EntityFrameworkCore;

public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    public DbSet<UserProfile> UserProfiles { get; set; }
}
```

### 执行迁移

一旦你定义了模型类和`DbContext`，就可以使用 EF Core 迁移来创建或更新数据库架构。在终端中运行以下命令创建初始迁移：

```bash
dotnet ef migrations add InitialCreate
```

然后，应用迁移以更新数据库：

```bash
dotnet ef database update
```

# 第 6 章

## 使用 ASP.NET Core 3 构建 Web API

在当今互联互的世界中，构建 Web API（应用程序编程接口）已成为不同应用程序之间通信和数据交换的关键。ASP.NET Core 3 提供了一个功能强大的框架，用于开发健壮且可扩展的 Web API，从而向客户端应用程序暴露数据和功能。在本指南中，我们将向您介绍 Web API 的概念，并演示如何使用 ASP.NET Core 3 构建它们。

### Web API 简介

Web API 是一组在互联网上暴露数据和功能的端点（URL），允许客户端应用程序与服务器进行交互并执行各种操作。Web API 实现了不同系统、平台和设备之间的无缝集成，以标准化且高效的方式促进了数据交换。Web API 的常见用例包括检索数据、更新记录、执行计算等。

### 入门 ASP.NET Core 3 Web API

要使用 ASP.NET Core 3 构建 Web API，你可以从使用 Visual Studio 或 .NET CLI 创建一个新的 ASP.NET Core Web API 项目开始。让我们使用 .NET CLI 创建一个简单的 Web API 项目：

```bash
# 生成一个全新的 ASP.NET Core Web API 项目。
dotnet new webapi -n MyWebApi
```

此命令创建了一个名为 "MyWebApi" 的新 ASP.NET Core Web API 项目。

### 创建控制器

在 ASP.NET Core Web API 中，控制器负责处理传入的 HTTP 请求并生成响应。你可以创建一个控制器为你的 Web API 定义端点和操作。

```csharp
// 基础 Web API 控制器的插图

using Microsoft.AspNetCore.Mvc;

namespace MyWebApi.Controllers
{
    [ApiController]
    [Route("api/{controller}")]
    public class ValuesController : ControllerBase
    {
        [HttpGet]
        public IActionResult Get()
        {
            return Ok(new string[] { "value1", "value2" });
        }
    }
}
```



在上面的示例中，我们创建了一个 `ValuesController`，它包含一个单一的操作方法 `Get`，该方法通过返回字符串值数组来响应 HTTP GET 请求。`[Route]` 属性指定了控制器的端点 URL 模式，而 `[HttpGet]` 属性指定了 `Get` 方法处理 HTTP GET 请求。

### 测试 Web API

你可以使用 Postman 等工具，或者通过从客户端应用程序发送 HTTP 请求来测试 Web API。要测试 `ValuesController` 的 `Get` 操作，你可以使用网络浏览器或 Postman 等工具向以下 URL 发送 HTTP GET 请求：

```text
http://localhost:5000/api/values
```

如果一切配置正确，你应该会收到一个包含字符串值 `value1` 和 `value2` 的响应。

## 处理 HTTP 动词

ASP.NET Core Web API 支持各种 HTTP 动词（GET、POST、PUT、DELETE 等），用于对资源执行不同的操作。你可以在控制器中创建操作方法来处理不同的 HTTP 动词并执行相应的操作。

```csharp
// Web API 控制器中处理不同 HTTP 动词的示例

public class ProductsController : ControllerBase
{
    [HttpGet]
    public IActionResult GetAllProducts()
    {
        // 从数据库检索所有产品
        return Ok(products);
    }

    [HttpGet("{id}")]
    public IActionResult GetProductById(int id)
    {
        // 根据 ID 从数据库检索特定产品
        return Ok(product);
    }

    [HttpPost]
    public IActionResult CreateProduct([FromBody] Product product)
    {
        // 修改数据库中已存在的产品
        return CreatedAtAction(nameof(GetProductById), new { id = product.Id }, product);
    }

    [HttpPut("{id}")]
    public IActionResult UpdateProduct(int id, [FromBody] Product product)
    {
        // 更新数据库中的现有产品
        return NoContent();
    }

    [HttpDelete("{id}")]
    public IActionResult DeleteProduct(int id)
    {
        // 从数据库中删除产品
        return NoContent();
    }
}
```

在上面的示例中，我们创建了处理不同 HTTP 动词的操作方法来管理产品。`[HttpGet]` 属性用于 HTTP GET 请求，`[HttpPost]` 用于 HTTP POST 请求，`[HttpPut]` 用于 HTTP PUT 请求，`[HttpDelete]` 用于 HTTP DELETE 请求。

### 数据传输对象（DTO）

在处理 Web API 时，使用数据传输对象（DTO）来封装在客户端和服务器之间传输的数据是一个良好的做法。DTO 有助于将数据的内部表示与外部表示解耦，从而提高可维护性和活性。

```csharp
// 数据传输对象（DTO）示例

public class ProductDto
{
    // 表示一个整数标识符 { get; set; }

    // 声明一个字符串标识符 { get; set; }

    // 表示一个公共十浮点数值 { get; set; }
}
```

使用 ASP.NET Core 3 构建 Web API 允许你为客户端应用程序暴露数据和功能。通过创建控制器定义端点和操作、处理不同的 HTTP 动词并使用 DTO 进行数据传输，你可以开发出强大且可扩展的 API，满足现代 Web 应用程序的需求。无论你是构建单页应用程序（SPA）还是为移动应用提供数据服务，ASP.NET Core 都提供了一个灵活且高效的解决方案。

```csharp
{
    var users = _userService.GetAllUsers();

    return Ok(users);
}

[HttpGet("{id}")]
public ActionResult<User> GetUserById(int id)
{
    var user = _userService.GetUserById(id);

    if (user == null)
    {
        return NotFound();
    }

    return Ok(user);
}
```

```csharp
}

// Other CRUD actions (POST, PUT, DELETE) can be defined similarly
}
}
```

在上面的示例中，我们创建了一个 `UserController` 来管理用户资源。该控制器定义了 HTTP GET 端点，用于获取所有用户以及通过 ID 获取特定用户。其他的 CRUD 操作（POST、PUT、DELETE）也可以定义类似的操作。

### 实现 CRUD 操作

若为了在 RESTful Web API 中实现 CRUD（创建、读取、更新、删除）操作，你可以使用 HTTP 方法对资源执行相应的操作。

- **POST**：创建新资源。
- **GET**：获取一个或多个资源。
- **PUT**：更新现有的资源。
- **DELETE**：删除现有的资源。

### 版本控制

版本控制是构建 RESTful Web API 的基本环节，以确保向后兼容并支持不断变化的需求。你可以使用基于 URL 的版本控制、查询字符串参数或 HTTP Header 对你的 API 进行版本控制。

```csharp
// ASP.NET Core 3 中基于 URL 的控制示例

[Route("api/v{version:apiVersion}/[controller]")]
public class UsersController : ControllerBase
{
    // Controller actions
}
```

使用 ASP.NET Core 3 构建 RESTful Web API 涉及遵循最佳实践并遵守 RESTful 原则。通过设计资源和操作来表示 CRUD 操作，实现版本控制策略，并确保无状态和统一接口，你可以创建出可扩展、可维护且可操作的 API。ASP.NET Core 3 提供了强大的工具和框架，用于构建满足现代 Web 应用需求的 RESTful Web API。

# 在应用程序中消费 Web API：集成外部数据和服务

在当今这个互联的世界中，将外部数据和服务集成到你的应用程序中，对于提供丰富的动态用户体验至关重要。Web API（应用程序接口）在启用不同系统之间的通信方面起着至关重要的作用，允许应用程序从外部源消费数据和服务。在本指南中，我们将探索如何使用 C# 在 ASP.NET Core 3 应用程序中消费 Web API，允许你无缝集成外部数据和服务。

## 消费 Web API 简介

消费 Web API 向外部端点发送 HTTP 请求以检索数据或执行操作。ASP.NET Core 提供了多种消费 Web API 的机制，包括 `HttpClient` 类，它允许你通过编程发送 HTTP 请求并接收响应。

## 使用 HttpClient 消费 Web API

ASP.NET Core 中的 `HttpClient` 类提供了一种简单且高效的方法来消费 Web API。你可以用它向外部端点发送 HTTP 请求并异步接收响应。

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class MyApiClient
{
    private readonly HttpClient _httpClient;

    public MyApiClient(HttpClient httpClient)
    {
        _httpClient = httpClient;
    }

    public async Task<string> GetDataFromApi()
    {
        HttpResponse response = await _httpClient.GetAsync("https://api.example.com/data");

        if (response.IsSuccessStatusCode)
        {
            string data = await response.Content.ReadAsAsync();
            return data;
        }
        else
        {
            throw new HttpRequestException(
                $"Failed to retrieve data. Status code: {response.StatusCode}");
        }
    }
}
```

在上面的示例中，我们创建了一个 `ApiClient` 类，它使用 `HttpClient` 向外部 API 端点（`https://api.example.com/data`）发送 HTTP GET 请求。我们异步等待响应，并在请求成功时读取内容。

### 配置 HttpClient

在使用 `HttpClient` 消费 Web API 时，正确配置它非常重要，以便处理超时、重试和默认请求头等各个方面。你可以使用 ASP.NET Core 中的 `HttpClientFactory` 来配置 `HttpClientFactory` 实例，它提供了一种集中的方式来管理和配置跨应用程序的 `HttpClient` 实例。

```csharp
// 在 Startup.cs 中配置 HttpClient

public void ConfigureServices(IServiceCollection services)
{
    services.AddHttpClient<MyApiClient>(client =>
    {
        client.BaseAddress = new Uri("https://api.example.com/");
        client.Timeout = TimeSpan.FromSeconds(30);
        client.DefaultRequestHeaders.Add("Accept", "application/json");
    });
}
```

在 `Startup.cs` 文件中，你可以使用 `AddHttpClient` 方法配置 `HttpClient` 实例。在这里，我们正在配置 `MyApiClient` 使用基础地址 `https://api.example.com/`、30 秒的超时时间，并将默认请求头设置为接受 JSON 响应。

## 处理身份验证

如果 Web API 需要身份验证，你可以在由 `HttpClient` 发送的 HTTP 请求中包含身份验证头。这可以通过向 `HttpClient` 实例的 `DefaultRequestHeaders` 集合中添加授权头来实现。

```csharp
public async Task<string> GetDataApiWithAuthentication(string accessToken)
{
    _httpClient.DefaultRequestHeaders.Authorization =
        new AuthenticationHeaderValue("Bearer", accessToken);

    HttpResponseMessage response =
        await _httpClient.GetAsync("https://api.example.com/data");

    if (response.IsSuccessStatusCode)
    {
        return await response.Content.ReadAsAsync();
    }

    return null;
}
```

在上面的示例中，我们创建了一个 `ApiClient` 类，它使用 `HttpClient` 向外部 API 端点（`https://api.example.com/data`）发送 HTTP GET 请求。我们异步等待响应，并在请求成功时读取内容。（注：此处原文代码不完整，逻辑已根据上下文重构。）

# 第 7 章

## Web 应用的安全实践

Web 应用安全是现代软件开发中至关重要的方面，因为互联网带来了各种可能损害应用程序机密性、完整性和可用性的威胁。ASP.NET Core 3 凭借其强大的安全功能和框架，为开发者提供了缓解安全威胁的工具。在本指南中，我们将探索应用程序的安全实践，包括理解安全威胁并实施保护它们的安全措施。

### 理解安全威胁

在探索安全实践之前，理解 Web 应用面临的不同威胁至关重要。常见的安全威胁包括：

1. **跨站脚本（XSS）**：跨站脚本（XSS）攻击涉及向其他用户看到的网页插入有害脚本。这些脚本可能会窃取机密数据、劫持话或破坏网站。
2. **SQL 注入（SQLi）**：当攻击者向 Web 应用程序的输入字段注入恶意 SQL 查询时，就会发生 SQL 注入攻击。成功的 SQLi 攻击会导致未经授权访问数据库、数据泄露或数据篡改。
3. **跨站请求伪造（CSRF）**：CSRF 攻击欺骗用户在未经许可的情况下在 Web 应用程序中执行意外操作。攻击者利用用户的活动会话执行未经授权的操作，如转账或更改设置。
4. **身份验证和授权缺陷**：弱的身份验证机制（如弱密码或缺少多因素认证）会导致未经授权访问敏感资源。授权缺陷可能导致用户获得他们没有权限访问的资源。
5. **敏感数据暴露**：未能正确加密和保护敏感数据（如用户凭据或财务信息），会导致数据泄露和身份盗用。

## 实现安全最佳实践

为了缓解 Web 安全威胁带来的风险，开发者可以在 ASP.NET Core 3 Web 应用中实施多种安全最佳实践。一些关键安全措施包括：

1. **输入验证与清理**：始终验证并清理用户输入，以防止 XSS 和 SQL 注入攻击。使用服务器端验证和编码库（如 AntiXSS 或 ESAPI）对用户输入进行清理，以防止恶意代码执行。
2. **参数化查询和 ORM 使用**：使用参数化查询或对象关系映射（ORM）框架（例如 Entity Framework Core）来防止 SQL 注入攻击。参数化查询确保用户输入被视为数据而非可执行的 SQL 代码。
3. **跨站请求伪造（CSRF）保护**：实现 CSRF 保护机制（例如反 CSRF 令牌），以防止攻击者代表已验证的用户执行未经授权的操作。在表单和 AJAX 请求中包含反 CSRF 令牌，以验证请求的来源。
4. **身份验证与授权**：实现强有身份验证机制，例如密码哈希和加盐、多因素身份验证（MFA）以及用于第三方身份验证的 OAuth/OpenID Connect。使用基于角色的访问控制（RBAC）或基于声明的授权来执行访问控制和权限。
5. **HTTPS 加密**：始终使用 HTTPS 加密来保护客户端与服务器之间的通信，并保护敏感数据免受拦截和窃听。从信任的证书颁发机构（CA）获取 SSL/TLS 证书，并配置您的 Web 服务器以强制执行 HTTPS。
6. **安全响应头**：使用安全响应头（如内容安全策略 CSP、`X-Content-Type-Options`、`X-Frame-Options` 和 `X-XSS-Protection`）来缓解各种 Web 安全威胁，包括 XSS、点击劫持和 MIME 类型嗅攻击。配置这些头部以限制浏览器行为并防止恶意活动。
7. **会话管理**：实现安全的会话管理实践（例如使用安全的 `HttpOnly` Cookie、会话超时和会话固定保护），以防止会话劫持和对用户会话的未经授权访问。
8. **内容安全策略（CSP）**：实施内容安全策略（CSP）以限制 Web 应用程序加载内容的来源，缓解 XSS 和数据注入攻击。指定允许的内容源、脚本执行策略和内联脚本限制以增强安全性。

## 示例：在 ASP.NET Core 3 中实现输入验证和清理

让我们来看一个如何使用 ASP.NET Core 3 中间件实现输入验证和清理的示例。

```csharp
// Startup.cs

public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options =>
    {
        options.Filters.Add(new AutoValidateAntiforgeryTokenAttribute());
    });
}

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    app.UseHttpsRedirection();
    app.UseStaticFiles();
}
```



```
app.UseRouting();

app.UseAuthentication();

app.UseAuthorization();

app.Use(async (context, next) =>
{
    context.Request.EnableBuffering();
    await next();
});

app.UseMiddleware<InputValidationMiddleware>();

app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller=Home}/{action=Index}/{id?}");
});
```

在上面的示例中，我们在 ASP.NET Core 中间件管道中添加了`InputValidationMiddleware`来执行输入验证和清理。该中间件拦截传入请求，验证并清理用户输入，然后将请求传递给管道中的下一个中间件组件。

保护使用 ASP.NET Core 3 构建的 Web 应用程序需要主动的方法，包括理解常见的安全威胁并实施适当的安全措施来缓解它们。通过遵循安全最佳实践（例如输入验证、CSRF 保护、HTTPS 加密以及安全的身份验证和授权机制），开发者可以保护其 Web 应用程序免受各种安全漏洞的影响，并确保用户数据的安全完整性。跟进新兴的安全威胁并定期审计和审查您的 Web 应用程序的安全态势，以应对任何潜在漏洞并保持强大的安全态势至关重要。

## 实现用户身份验证和授权：控制对安全数据的访问

用户身份验证和授权是 Web 应用程序安全的组成部分，允许您控制对敏感资源的访问，并确保只有经过验证和授权的用户才能与之进行交互。ASP.NET Core 3 提供了实现用户身份验证和授权的强大功能和框架。开发者可以有效地这些身份验证和授权来保护 Web 应用程序。

### 用户身份验证

用户身份验证涉及通过验证凭据（如用户名和密码）来确认访问 Web 应用程序的用户身份。ASP.NET Core 3 支持多种身份验证机制，包括基于 Cookie、JWT（JSON 令牌）身份验证、OAuth 和 OpenID Connect。本指南将探索如何在 ASP.NET Core 3 中实现身份验证和授权。

### 基于 Cookie 的身份验证

基于 Cookie 的身份验证是 ASP.NET Core 应用程序常用的机制之一。它涉及向客户端发放包含身份信息的 Cookie，该 Cookie 会随随后的请求发送。

```csharp
// Startup.cs
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
      .AddCookie(options =>
      {
          options.LoginPath = "/Account/Login";
          options.AccessDeniedPath = "/Account/AccessDenied";
      });
}

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // ...中间件配置
    app.UseAuthentication();
    app.UseAuthorization();
}
```

### 用户授权

用户授权确定经过验证的用户是否有权限访问特定资源或执行某些操作。ASP.NET Core 3 支持基于角色、基于策略和基于声明的授权，以执行访问控制和权限。

### 基于角色的授权

基于角色的授权涉及为用户分配角色（例如管理员、版主、用户），并根据其角色限制访问。ASP.NET Core 提供了对基于角色的授权内置支持，允许对控制器操作或 Razor 页面使用`[Authorize(Roles = "Admin")]`属性来限制特定角色的访问。

```csharp
// 在 ASP.NET Core 3 中基于角色的授权示例
[Authorize(Roles = "Admin")]
public IActionResult AdminDashboard()
{
    // 管理员仪表板代码
}
```

### 基于策略的授权

基于策略的授权允许您定义自定义授权策略，根据各种因素（如角色、声明或自定义需求）封装访问控制逻辑。您可以在`Startup.cs`文件中定义授权策略，并使用`[Authorize(Policy = "策略名称")]`属性将其应用到控制器操作或 Razor 页面上。

```csharp
// 在 ASP.NET Core 3 中基于策略的授权示例
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthorization(options =>
    {
        options.AddPolicy("AdminPolicy", policy =>
            policy.RequireRole("Admin"));
    });
}

[Authorize(Policy = "AdminPolicy")]
public IActionResult AdminDashboard()
{
    // 管理员仪表板代码
}
```

实现用户身份验证和授权对于控制使用 ASP.NET Core 3 构建的 Web 应用对安全数据和资源的访问至关重要。通过利用内置的身份验证中间件和服务，开发者可以实现各种身份验证机制，例如基于 Cookie 的身份验证、JWT 身份验证以及 OAuth/OpenID Connect，从而有效地验证用户。同样，基于角色的授权、基于策略的授权和基于声明的授权机制允许开发者根据用户角色、声明或自定义需求执行访问控制和权限。通过将这些身份验证和授权机制与安全密码哈希、HTTPS 加密和会话管理等最佳实践相结合，开发者可以构建安全稳健的 Web 应用，保护敏感数据并确保用户交互的完整性。

## 处理错误和异常：构建健壮且韧性的应用程序

有效处理错误和异常对于构建健壮且具有韧性的 Web 应用至关重要。ASP.NET Core 3 为开发者提供了强大的工具和框架，用于优雅地管理错误和异常，提高用户体验并确保应用程序的稳定性。在本指南，我们将探索如何在 ASP.NET Core 3 中处理错误和异常，包括最佳实践和代码示例。

### 理解错误和异常

错误和异常可能发生在 Web 应用执行过程的各个点，包括请求处理期间、数据库操作或第三方服务集成。常见的错误和异常类型包括：

1. HTTP 错误：这些错误发生在服务器遇到无效请求或在处理请求时遇到内部错误。示例包括 404 Not Found、500 Internal Server Error 和 403 Forbidden。

2. 应用程序异常：这些异常发生在应用程序代码内部，由于编程错误、无效输入或意外情况引起。示例包括空引用异常、数据库连接错误和算术溢出异常。

3. 验证错误：当用户输入无法满足指定的验证标准（例如必填字段、数据类型验证或长度限制）时，就会验证错误。

## 在 ASP.NET Core 3 中处理错误

ASP.NET Core 提供了多种机制在应用程序的不同层级处理错误和异常，包括中间件、过滤器和全局错误处理。

### 中间件

ASP.NET Core 中的中间件组件允许你在请求处理管道中拦截请求和响应。你可以通过注册自定义中间件组件来捕获并处理请求处理期间抛出的异常，从而处理错误和异常。

```csharp
// ASP.NET Core 3 中错误处理中间件的示例
public class ErrorHandlingMiddleware
{
    private readonly RequestDelegate _next;

    public ErrorHandlingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (Exception ex)
        {
            // 记录异常
            ILogger<ErrorHandlingMiddleware> logger = context.RequestServices.GetService<ILogger<ErrorHandlingMiddleware>>();
            logger.LogError(ex, "An error occurred while processing the request");

            // 返回自定义错误响应
            context.Response.StatusCode = StatusCode.Status500InternalServerError;
            await context.Response.WriteAsync("An error occurred. Please try again later.");
        }
    }
}
```

在上面的示例中，我们创建了一个自定义中间件组件（`ErrorHandlingMiddleware`），它捕获请求处理期间抛出的异常，并返回状态码为 500 Internal Server Error 的自定义错误响应。

### 异常过滤器

ASP.NET Core 中的异常过滤器允许你通过对控制器操作或操作方法应用`[ExceptionHandler]`特性，在操作方法级别拦截并处理异常。

```csharp
// ASP.NET Core 3 中异常过滤器的示例
public class CustomExceptionFilterAttribute : ExceptionFilterAttribute
{
    public override void OnException(ExceptionContext context)
    {
        // 记录异常
        ILogger<CustomExceptionFilterAttribute> logger = context.HttpContext.RequestServices.GetService<ILogger<CustomExceptionFilterAttribute>>();
        logger.LogError(context.Exception, "An error occurred while processing the request");

        // 返回自定义错误响应
        context.Result = new StatusCodeResult(StatusCodes.Status500InternalServerError);
    }
}

[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    [HttpGet]
    [CustomExceptionFilter]
    public IActionResult GetAllUsers()
    {
        // 获取所有用户的代码
    }
}
```

在上面的示例中，我们创建了一个自定义异常过滤器（`CustomExceptionFilterAttribute`），它拦截由`GetAllUsers`操作方法抛出的异常，并返回状态码为 500 Internal Server Error 的自定义错误响应。

### 全局错误处理

ASP.NET Core 中的全局错误处理允许你集中管理和处理整个应用程序中错误和异常。你可以使用`UseExceptionHandler`中间件在`Startup.cs`文件中配置全局错误处理。

```csharp
// Startup.cs
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // 其他中间件配置
    app.UseExceptionHandler("/Error");
    // 其他端点配置
}
```




在上面的示例中，我们配置了全局错误处理，以便在发生未处理的异常时将用户重定向到`Error`端点。

有效处理错误和异常对于构建使用 ASP.NET Core 3 的健壮且具有韧性的 Web 应用至关重要。通过使用中间件、异常过滤器和全局错误处理，开发者可以优雅地拦截、记录和处理错误，提高用户体验并确保应用程序的稳定性。

## 部署您的应用程序

1. **发布您的应用程序**：在 Visual Studio 中，右键点击您的 ASP.NET Core 项目，选择“发布”（Publish），并选择“Azure App Service”作为目标。按照提示选择 Azure 订阅、App Service 实例和部署设置。
2. **部署您的应用程序**：点击“发布”将您的应用程序部署到 Azure App Service。Visual Studio 将构建并将您的应用程序文件发布到所选 App Service 实例。
3. **配置部署设置**：在 Azure 门户或 Visual Studio 中配置额外的部署设置，例如部署插槽、持续集成和环境变量。
4. **监控和管理您的应用程序**：使用 Azure 监控工具监控应用程序的性能、日志和指标。使用 Azure DevOps 或 GitHub Actions 实现自动化部署和持续集成/持续部署（CI/CD）流水线。

## 部署最佳实践

为了确保部署过程顺畅并优化您的 ASP.NET Core 3 应用程序性能和安全性，请考虑以下最佳实践：

- **自动化部署**：使用 Azure DevOps、GitHub Actions 或 Jenkins 等自动化工具实现部署过程，减少人工错误。
- **版本控制**：使用 Git 或其他版本控制系统将应用程序代码和部署脚本置于版本控制下，以便跟踪更改并有效协作。
- **环境配置**：使用特定环境的配置文件或环境变量来管理跨部署环境（如开发、测试、生产）的配置设置，例如连接字符串、API 密钥和功能开关。
- **安全性**：通过应用安全最佳实践（如使用 HTTPS、启用防火墙、定期更新依赖以及实施基于角色的访问控制（RBAC））来确保您的应用程序和服务器环境的安全。
- **监控与日志**：使用 Serilog 或 Application Insights 等日志框架监控应用程序的健康、性能和错误。设置警报和通知以主动检测并解决问题。

将您的 ASP.NET Core 3 应用程序部署到全球涉及选择正确的部署选项、配置托管环境并遵循最佳实践以确保部署过程的顺畅和安全。无论您是自托管、部署到 IIS、容器化应用程序，还是利用 Azure、AWS 或 Google Cloud 等云平台，了解部署选项和最佳实践对于向用户提供可靠且扩展的 Web 应用程序至关重要。通过遵循部署实践并利用自动化工具和云服务，您可以简化部署流程，最大限地减少停机时间，并为用户提供通过互联网访问您的应用程序的无缝体验。

## 理解托管选项：为您的需求选择合适的平台

选择正确的托管平台对于您的 ASP.NET Core 3 Web 应用程序的成功至关重要。

托管平台决定了运行应用程序的基础设施、扩展性、可靠性和成本。ASP.NET Core 3 支持多种托管选项，每个选项都有其优势和适用场景。在本指南中，我们将探索 ASP.NET Core 3 应用程序的不同托管选项，并讨论在为您的需求选择正确平台时需要考虑因素。

### ASP.NET Core 3 的托管选项

1. **自托管（Self-Hosting）**：通过自托管，您可以使用 Kestrel（ASP.NET Core 内置的跨平台 Web 服务器）将 ASP.NET Core 应用程序作为独立应用程序部署。自托管适用于小型应用程序或您对托管环境具有完全控制权的场景。
2. **信息信息服务（IIS）**：可以使用 ASP.NET Core Module 将 ASP.NET Core 应用程序部署到 Windows 服务器上的 IIS 上。这种方法允许您利用现有基础设施并在同一台服务器上管理多个应用程序。
3. **使用 Docker 进行容器化**：使用 Docker 进行容器化允许您将 ASP.NET Core 应用程序及其依赖打包到容器镜像中。容器化应用程序具有可移植性、可扩展性，并能够在不同环境中一致运行，这使其成为微服务架构和云部署的理想选择。
4. **云托管**：Azure、AWS 和 Google Cloud 等云平台为托管 ASP.NET Core 应用程序提供了可扩展且可靠的基础设施。云托管提供了自动伸缩、负载均衡和托管数据库等功能，简化了部署和维护任务。

### 选择托管平台时需要考虑的因素

为您的 ASP.NET Core 3 应用程序选择托管平台时，请考虑以下因素：

- **扩展性**：评估应用程序的扩展性需求。它需要处理大量并发用户或流量激增吗？选择提供可扩展基础设施的托管平台。
- **可靠性**：确保托管平台提供高可用性和可靠性。寻找如冗余基础设施、数据复制和 SLA（服务等级协议）保证等功能，以减少停机时间。
- **成本**：考虑在不同平台托管应用程序的成本影响。比较按需付费、订阅制和基于用量的定价模型，并选择符合您的预算和成本要求的托管选项。
- **管理与维护**：评估每个托管选项所需的管理和维护程度。与托管云服务相比，自托管和容器化可能需要更多的手动配置和维护。选择符合您团队知识和资源可用性的平台。
- **集成与生态系统**：考虑托管平台的集成能力和生态系统。它是否与您开发栈中的其他服务和工具无缝集成？选择支持您现有工作流和工具的平台。
- **安全与合规**：确保托管平台满足您的安全合规要求。寻找内置的安全控制、合规认证和数据加密功能，以保护您的应用程序和数据免受威胁和法规影响。

### 示例：部署到 Azure App Service

让我们演示将 ASP.NET Core 3 应用程序部署到 Azure App Service 的过程，这是一个全托管的 Web 应用平台。

1. **创建 Azure App Service**：登录 Azure 门户，创建新的 App Service 资源，并配置必要的设置，例如订阅、资源组和应用名称。
2. **发布您的应用程序**：在 Visual Studio 中，右键点击您的 ASP.NET Core 项目，选择“发布”（Publish），并选择“Azure App Service”作为目标。按照提示选择 Azure 订阅、App Service 实例和部署设置。
3. **部署您的应用程序**：点击“发布”将您的应用程序部署到 Azure App Service。Visual Studio 将构建并将您的应用程序文件发布到所选 App Service 实例。
4. **配置部署设置**：在 Azure 门户或 Visual Studio 中配置额外的部署设置，例如部署插槽、持续集成和环境变量。

为您的 ASP.NET Core 3 应用程序选择正确的托管平台对于确保扩展性、可靠性和成本效益至关重要。无论您选择自托管、部署到 IIS、容器化应用程序，还是利用 Azure、AWS 或 Google Cloud 等云平台，在做决定时请考虑扩展性、可靠性、成本、管理与维护、集成与生态系统以及安全与合规等因素。

## 配置提供程序

ASP.NET Core 3 提供了配置提供程序，允许你从各种源加载配置设置，例如 JSON 文件、环境变量、命令行参数和 Azure Key Vault。通过使用配置提供程序，你可以轻松地管理特定环境的配置设置，并根据需要覆盖默认值。

### 环境配置的最佳实践

在将 ASP.NET Core 3 应用程序部署到不同的环境时，请考虑以下管理配置设置的最佳实践：

1. **配置**：使用 JSON 配置文件（`appsettings.json`）存储应用程序的默认配置设置。你可以在单独的 JSON 文件中定义特定环境配置，例如 `appsettings.development.json`、`appsettings.staging.json` 和 `appsettings.production.json`。
2. **环境变量**：使用环境变量在运行时覆盖配置设置。环境变量提供了一种灵活的方法，可以在不修改配置文件的情况下配置应用程序设置。你可以直接在托管平台上设置环境变量，或使用 Docker 等工具将环境变量传递给容器化应用程序。
3. **密钥管理**：使用 Azure Key Vault 或其他密钥管理解决方案安全地存储敏感配置，例如连接字符串、API 密钥和密码。避免在配置文件或环境变量中存储敏感信息，以降低泄露风险。
4. **配置构建器**：使用配置构建器根据当前环境动态构建配置设置。配置构建器允许你通过编程方式构造配置设置，结合来自多个源的值并根据需要应用特定环境的覆盖。

## 示例：在 ASP.NET Core 3 中配置基于环境的配置

让我们来看如何在 ASP.NET Core 3 应用程序中配置基于环境的配置示例：

```csharp
// Startup.cs

public class Startup
{
    public Startup(IConfiguration configuration, IWebHostEnvironment environment)
    {
        Configuration = configuration;
        Environment = environment;
    }

    public IConfiguration Configuration { get; }
    public IWebHostEnvironment Environment { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        // 根据环境配置服务
        if (Environment.IsDevelopment())
        {
            // 开发环境配置
            services.AddDbContext<ApplicationDbContext>(options =>
                options.UseSqlServer(Configuration.GetConnectionString("DevelopmentConnection")));
        }
        else if (Environment.IsStaging())
        {
            // 阶段环境配置
            services.AddDbContext<ApplicationDbContext>(options =>
                options.UseSqlServer(Configuration.GetConnectionString("StagingConnection")));
        }
        else if (Environment.IsProduction())
        {
            // Production环境配置
            services.AddDbContext<ApplicationDbContext>(options =>
                options.UseSqlServer(Configuration.GetConnectionString("ProductionConnection")));
        }

        // 其他服务配置
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }
        else
        {
            app.ExceptionHandler("/Error");
            app.UseHsts();
        }

        // 其他中间件配置
    }
}
```

在上面的示例中，我们使用 `IWebHostEnvironment` 接口确定当前环境（开发、阶段、生产）并相应地配置服务。我们使用 `GetConnectionString` 方法从配置设置加载特定环境的连接字符串，并根据当前环境配置应用程序的行为。

将 ASP.NET Core 3 应用程序部署到不同的环境需要配置基于环境的配置设置，以确保在开发、阶段和生产环境中的行为一致性。通过利用配置提供程序、环境变量和密钥管理解决方案，你可以有效地管理配置设置并使你的应用程序适应不同的部署场景。遵循管理基于环境配置的最佳实践（例如使用配置文件、环境变量和密钥管理解决方案），以确保你的 ASP.NET Core 3 应用程序在不同环境下的安全性、可靠性和可扩展性。通过实施有效的配置管理，你可以放心地将你的 ASP.NET Core 3 应用程序部署到不同的环境，确保用户在各种部署情况下都能体验到一致且可靠的性能。

# 第 9 章：测试你的 Web 应用程序：确保质量和可靠性

测试是软件开发过程中不可缺的一部分，确保你的 Web 应用程序运行正常、性能良好并符合用户预期。ASP.NET Core 3 提供了健壮的测试框架和工具，用于编写和执行测试以验证代码的行为并确保质量和可靠性。在本指南中，我们将关注使用 C# 进行单元测试，并探索如何编写测试来验证你的 ASP.NET Core 3 Web 应用程序代码。

## 使用 C# 进行单元测试

单元测试是一种软件测试技术，通过隔离测试软件应用程序的单个单元或组件来验证其行为和功能。在 ASP.NET Core 3 中，你可以使用流行的测试框架（如 MSTest、xUnit 和 NUnit）编写单元测试。这些框架提供了高效编写、组织和执行单元测试的工具和实用程序。

## 编写测试

为你的 ASP.NET Core 3 Web 应用程序编写单元测试时，通常关注测试单个组件，如控制器（Controllers）、服务（Services）、存储库（Repositories）和工具类。你使用依赖注入等技术将这些组件与其依赖项分离，并使用 Mock 框架来确保测试是可靠且重复的。

## 示例：测试 ASP.NET Core 3 中的控制器

让我们查看如何使用 xUnit 和 Moq（一个流行的 .NET Mock 框架）为 ASP.NET Core 3 Web 应用程序中的控制器编写单元测试：

```csharp
// UserController.cs

public class UserController : ControllerBase
{
    private readonly IUserService _userService;

    public UserController(IUserService userService)
    {
        _userService = userService;
    }

    [HttpGet("{id}")]
    public IActionResult GetUser(int id)
    {
        var user = _userService.GetUserById(id);

        if (user == null)
        {
            return NotFound();
        }

        return Ok(user);
    }
}
```

```csharp
// UserControllerTests.cs

public class UserControllerTests
{
    private readonly Mock<IUserService> _userServiceMock;
    private readonly UserController _controller;

    public UserControllerTests()
    {
        _userServiceMock = new Mock<IUserService>();
        _controller = new UserController(_userServiceMock.Object);
    }

    [Fact]
    public void GetUser_ReturnsUser_WhenUserExists()
    {
        // 准备
        int userId = 1;
        var expectedUser = new User { Id = userId, Name = "Charlie Brown" };

        _userServiceMock
            .Setup(service => service.GetUserById(userId))
            .Returns(expectedUser);

        // 执行
        var result = _controller.GetUser(userId) as OkObjectResult;

        // 断言
        Assert.NotNull(result);
        Assert.Equal(expectedUser, result.Value);
    }

    [Fact]
    public void GetUser_ReturnsNotFound_WhenUserDoesNotExist()
    {
        // 准备
        int userId = 1;

        _userServiceMock
            .Setup(service => service.GetUserById(userId))
            .Returns((User)null);

        // 执行
        var result = _controller.GetUser(userId) as NotFoundResult;

        // 断言
```




```csharp
Assert.NotNull(result);
```

## 单元测试最佳实践

为你的 ASP.NET Core 3 Web 应用程序编写单元测试时，请考虑以下最佳实践：

1. **测试覆盖率**：通过为关键组件和边界情况编写测试，以实现高测试覆盖率为目标。关注测试行为而非实现细节，以确保测试的健壮和可靠。
2. **隔离**：使用依赖注入和模拟（mocking）框架等技术将被测单元与其依赖项隔离。这确保了测试是独立的、可重复的且不依赖外部因素。
3. **测试命名**：为测试使用描述性且有意义的名字，以传达其目的和预期行为。遵循一致的命名规范，例如 `MethodName_StateUnderTest_ExpectedBehavior`，使测试更易理解和维护。
4. **安排-执行-断言（AAA）**：使用 AAA 模式结构化测试，即安排测试环境、对被测单元执行操作、并断言预期行为。这有助于组织测试并使意图更加清晰。
5. **参数化测试**：使用参数化测试通过单个测试方法测试多个输入和场景。这减少了代码重复并提高了不同用例的测试覆盖率。

使用 C# 进行单元测试是确保你的 ASP.NET Core 3 Web 应用程序质量和可靠的关键实践。通过编写测试验证单个组件及其行为，你可以及早发现 Bug、防止回归并提高代码库的可维护性。遵循单元测试最佳实践（如实现高测试覆盖率、隔离被测单元、使用描述性测试名称以及遵循 AAA 模式），为你的 ASP.NET Core 3 Web 应用程序编写高效可靠的测试。有了稳健的单元测试策略，你可以自信地构建和部署 Web 应用程序，它们符合质量标准并提供良好的用户体验。

## 集成测试与 UI 测试：构建全面的测试策略

虽然单元测试专注于孤立测试单个组件，但集成测试和 UI 测试旨在验证你的 ASP.NET Core 3 Web 应用程序中多个组件之间的交互和行为。通过集成测试和 UI 测试补充单元测试，你可以构建一个全面的测试策略，确保应用程序在不同层级上的质量、可靠性和功能性。在本指南中，我们将探索 ASP.NET Core 3 Web 开发背景下的集成测试和 UI 测试，包括最佳实践和代码示例。

### 集成测试

集成测试验证应用程序不同组件之间（如控制器、服务、仓库和外部依赖项）的交互和通信。在 ASP.NET Core 3 中，你可以使用 xUnit、MSTest 或 NUnit 等测试框架编写集成测试，并结合 Entity Framework Core 等库进行数据库集成测试。

### 示例：ASP.NET Core 3 控制器的集成测试

让我们来看如何为 ASP.NET Core 3 Web 应用程序中的控制器编写集成测试示例：

```csharp
// UserControllerIntegrationTests.cs

public class UserControllerIntegrationTests : IClassFixture<WebApplicationFactory<Startup>>
{
    private readonly WebApplicationFactory<Startup> _factory;

    public UserControllerIntegrationTests(WebApplicationFactory<Startup> factory)
    {
        _factory = factory;
    }

    [Fact]
    public async Task GetUser_ReturnsUser_WhenUserExists()
    {
        // Arrange
        var client = _factory.CreateClient();
        var userId = 1;

        // Act
        var response = await client.GetAsync($"api/users/{userId}");

        // Assert
        response.EnsureSuccessStatusCode();

        var user = await response.Content.ReadAsAsync<User>();

        Assert.NotNull(user);
        Assert.Equal(userId, user.Id);
    }
}
```

在上面的示例中，我们使用 ASP.NET Core 提供的 `WebApplicationFactory` 类创建一个托管我们应用程序的内存测试服务器。然后，我们使用 `HttpClient` 类向服务器发送 HTTP 请求并验证响应。

### UI 测试

UI 测试（也称为端到端测试或功能测试）从用户的角度验证应用程序用户界面的行为和功能。在 ASP.NET Core 3 中，你可以使用 Selenium WebDriver 等框架编写 UI 测试，它通过与浏览器交互来模拟用户操作并验证应用程序的行为。

### 示例：在 ASP.NET Core 3 中使用 Selenium 进行 UI 测试

```csharp
// MyHomePageUITests.cs

public class HomePageUITests
{
    private readonly IWebDriver _driver;

    public HomePageUITests()
    {
        _driver = new ChromeDriver();
    }

    [Fact]
    public void HomePage_ShouldDisplayWelcomeMessage()
    {
        // Arrange
        _driver.Navigate().GoToUrl("http://localhost:5000");

        // Act
        var welcomeMessage = _driver.FindElement(By.Id("welcome-message")).Text;

        // Assert
        Assert.Equal("Welcome to our ASP.NET Core 3 application!", welcomeMessage);
    }

    public void Dispose()
    {
        _driver.Quit();
        _driver.Dispose();
    }
}
```

在上面的示例中，我们使用 Selenium WebDriver 自动化与浏览器的交互。我们导航到 ASP.NET Core 3 应用程序的首页，并验证欢迎消息显示正确。

### 集成测试与 UI 测试的最佳实践

为你的 ASP.NET Core 3 Web 应用程序编写集成测试和 UI 测试时，请考虑以下最佳实践：

1. **隔离**：使用模拟或内存数据库等技术，将集成测试从数据库和外部服务等外部依赖中隔离。
2. **测试数据**：使用测试数据和固件（fixtures）为集成测试设置应用程序的初始状态。这确保了测试的可重复性和可靠。
3. **页面对象模式（Page Object Pattern）**：使用页面对象模式封装 UI 测试中与网页的交互。这提高了测试的可读性、可维护性和重用性。
4. **无头测试**：考虑在无头模式下运行 UI 测试以提高测试性能和可靠性，特别是在 CI/CD 流水线。
5. **持续集成**：将集成测试和 UI 测试集成到你的 CI/CD 流水中，以实现测试测试并确保每次发布的质量一致。

集成测试和 UI 测试是 ASP.NET Core 3 Web 应用程序全面测试策略的重要组成部分。通过集成测试和 UI 测试补充单元测试，你可以验证应用程序内部多个组件的交互和行为，并确保其在不同层级上的质量、可靠性和功能。遵循编写集成测试和 UI 测试的最佳实践，如将测试与外部依赖隔离、使用测试数据和固件、在 UI 测试中使用页面对象模式以及将测试集成到 CI/CD 流水中。有了稳健的测试策略，你可以自信地构建和部署 ASP.NET Core 3 Web 应用程序，知道它们符合质量标准并提供良好的用户体验。

# 第 10 章

## 探索高级 ASP.NET Core 3 特性

ASP.NET Core 3 带有旨在增强开发体验、提高性能并便于代码维护的高级特性。其中一个此类特性是依赖注入（DI），这是一种管理对象依赖并促进 ASP.NET Core 应用程序松耦合的强大技术。在本教程中，我们将检查 ASP.NET Core 3 中的依赖注入、其优势以及如何使用代码说明高效地将其纳入其中。

## 依赖注入（DI）

依赖注入是一种用于在软件应用程序中实现控制反转（IoC）的设计技术。它允许将对象依赖的创建和管理从使用它们的对象解耦，从而产生更模块化、更可维护且更可测试的代码。

### 依赖注入的好处

1. **低耦合**：依赖注入通过消除硬编码依赖来促进组件之间的松耦合。组件仅依赖于抽象（接口）而非具体实现，使其更加灵活且更容易被替换或扩展。
2. **可测试性**：依赖注入通过允许你轻松用模拟对象（mock objects）或存根（stubs）替换依赖，简化单元测试。这使得更容易隔离并测试单个组件，从而提高了应用程序的可测试性。
3. **模块化**：依赖注入通过将复杂的系统分解为更小、更易控制的元素，促进模块化设计。这使得你的代码库随着时间的推移更容易理解、维护和演进。
4. **可重用**：依赖注入通过使组件独立于特定的实现，促进了组件的重用。这允许你在应用程序的不同部分甚至在完全不同的应用程序中重用组件。

## 在 ASP.NET Core 3 中实现依赖注入

ASP.NET Core 3 通过其内置的 IoC 容器为依赖注入提供了内置支持，该容器基于 `Microsoft.Extensions.DependencyInjection` 命名空间。你可以在 `Startup` 类的 `ConfigureServices` 方法中注册和服务依赖，并使用构造函数注入将依赖注入到控制器、服务和其他组件中。

### 示例：在 ASP.NET Core 3 中实现依赖注入

让我们看看如何在 ASP.NET Core 3 应用程序中实现依赖注入的示例：

```csharp
// IService.cs

public interface IService
{
    void DoSomething();
}
```

```csharp
// Service.cs

public class Service : IService
{
    public void DoSomething()
    {
        Console.WriteLine("Doing something...");
    }
}

// Startup.cs

public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddTransient<IService, Service>();
    }

    // 其他配置方法
}

// HomeController.cs

public class HomeController : Controller
{
    private readonly IService _service;

    public HomeController(IService service)
    {
        _service = service;
    }

    public IActionResult Index()
    {
        _service.DoSomething();
        return View();
    }
}
```

在上面的示例中，我们定义了一个接口 `IService` 和一个具体实现 `Service`。然后，我们使用 `Startup` 类中的 `ConfigureServices` 方法向 IoC 容器中注册 `IService` 和 `Service`。最后，我们将 `IService` 注入到 `HomeController` 类的构造函数中，并使用它在 `Index` 方法中执行某些操作。

## 高级依赖注入功能

ASP.NET Core 3 的依赖注入容器提供了若干有效管理依赖的高级功能：

1. **生命周期管理**：ASP.NET Core 支持不同的生命周期，包括瞬时（transient）、作用域（scoped）和单例（singleton）。瞬时服务每次被请求时创建，作用域服务每个请求创建一个，单例服务创建一次并在整个应用程序中共享。
2. **配置**：你可以使用 ASP.NET Core 中的选项和设置来配置服务。这允许你根据特定环境的设置或应用程序需求自定义服务的行为和配置。
3. **服务组合**：ASP.NET Core 支持服务组合，允许你从多个较小的组合组合复杂的服务。通过将大型组件分解为更小、更易管理的部分，促进了模块化和可重用性。
4. **构造函数注入**：构造函数注入是 ASP.NET Core 中向组件注入依赖的首选方法。它确保在创建组件时依赖是用的，提升了代码的一致性和清晰度。

## 依赖注入的最佳实践

在 ASP.NET Core 3 中使用依赖注入时，考虑以下最佳实践：

1. **使用构造函数注入**：优先使用构造函数注入而非属性注入或方法注入等其他注入方法。构造函数注入促进了一致性并确保在创建组件时依赖项可用。
2. **保持依赖显式**：在组件的构造函数中清晰地定义和声明依赖。避免隐藏或隐含的依赖，因为它们会增加代码理解和维护的复杂度。
3. **明智使用生命周期管理**：根据每个服务的用法和需求，选择合适的服务生命周期（瞬时、作用域、单例）。在使用作用域或单例服务时，注意资源利用和内存泄漏的风险。
4. **避免服务定位**：避免使用“服务定位器”（Service Locator）反模式，即组件在方法内部直接从 IoC 容器检索依赖。相反，通过构造函数注入显式地注入依赖。
5. **独立测试依赖**：单独测试每个组件及其依赖，以确保它们在隔离状态下的行为符合预期。在单元测试中使用模拟框架将依赖替换为模拟对象或存根。

依赖注入是 ASP.NET Core 3 中的一项强大功能，促进了应用程序的松耦合、模块化和可测试性。通过将组件与其依赖解耦并使用构造函数注入依赖，你可以构建更具模块化、可维护且可测试的代码。遵循依赖注入的推荐实践（包括采用构造函数注入、维护显式依赖、高效管理服务生命周期以及避免定位），以保证你的 ASP.NET Core 3 应用程序的质量和可靠性。通过依赖注入，你可以构建灵活、可扩展且可维护的应用程序，有效满足用户需求和业务要求。

## 中间件：拦截请求和响应以高级功能

ASP.NET Core 3 中的中间件是一个强大的概念，允许你拦截 HTTP 请求和响应，从而为你的应用程序请求处理管道添加自定义功能。中间件位于客户端和服务器之间，为处理跨交叉关注点（如身份验证、日志记录、错误处理等）提供了灵活机制。在本指南中，我们将探索 ASP.NET Core 3 中的中间件、其功能以及如何实现自定义中间件。

### 理解中间件

ASP.NET Core 3 中的中间件由在请求处理管道中顺序执行的组件组成。每个中间件组件都有能力在将请求或响应转发给下一个中间件之前进行检查、修改或跳过。这允许你在不弄乱控制器逻辑的情况下为应用程序添加交叉关注点和高级功能。

### 内置中间件

ASP.NET Core 3 自带了一组内置中间件组件，处理路由、静态文件提供、身份验证和日志等常见任务。这些中间件在 `Startup` 类中使用 `Use` 扩展方法进行配置，允许你轻松将它们添加到应用程序的请求处理管道中。

### 示例：在 ASP.NET Core 3 中使用内置中间件

```csharp
// Startup.cs

public class Startup
{
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }

        app.UseRouting();
        app.UseAuthentication();
        app.UseAuthorization();

        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllers();
        });
    }
}
```

在上面的示例中，我们使用 `Startup` 类中 `Configure` 方法的 `Use` 扩展方法配置了内置中间件组件，如开发者异常页、路由、身份验证和授权。这些中间件按照指定的顺序在请求处理管道中执行。

### 编写自定义中间件

除了内置中间件组件，ASP.NET Core 3 还允许你编写自定义中间件组件为应用程序添加自定义功能。自定义中间件是实现 `Delegate` 委托类型的简单 C# 类，该类型表示处理 HTTP 请求的函数。

### 示例：在 ASP.NET Core 3 中编写自定义中间件

```csharp
// CustomMiddleware.cs

public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }
}
```



```csharp
public async Task Invoke(HttpContext context)
{
    // 在将请求传递给下一个中间件之前执行自定义逻辑
    await context.Response.WriteAsync("Custom Middleware: Before\n");

    await _next(context);

    // 在下一个中间件处理请求后执行自定义逻辑
    await context.Response.WriteAsync("Custom Middleware: After\n");
}
```

在你的 ASP.NET Core 3 中使用自定义中间件，你需要使用 `UseMiddleware` 扩展方法在 `Startup` 类的 `Configure` 方法中注册它。

## 示例：在 ASP.NET Core 3 中注册自定义中间件

```csharp
// Startup.cs
public class Startup
{
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        app.UseMiddleware<CustomMiddleware>();
        app.UseRouting();
        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllers();
        });
    }
}
```

在上面的示例中，我们使用 `UseMiddleware` 扩展方法在 `Startup` 类的 `Configure` 方法中注册了 `CustomMiddleware` 类。这把我们的自定义中间件组件添加到请求处理管道中，允许它拦截并处理 HTTP 请求。

## 中间件的优势

ASP.NET Core 3 中的中间件具有以下几个优势：

1. **模块化：** 中间件组件是模块化且可组合的，允许你在应用程序的不同部分封装和重用常见功能。
2. **灵活性：** 中间件为扩展和自定义请求处理管道提供了一种灵活的机制。你可以添加、删除或重新排序中间件组件以满足应用程序的特定需求。
3. **关注点分离：** 中间件允许你将身份验证、日志和错误处理等交叉关注点封装在独立的中间件组件中，从而促进关注点的分离。
4. **可测试性：** 中间件组件可以很容易地进行隔离单元测试，允许你独立于应用程序中的其他组件验证其行为和功能。

ASP.NET Core 3 中的中间件是一个强大的概念，它允许你拦截 HTTP 请求和响应，使你能够为应用程序的请求处理管道添加自定义功能。无论你是使用内置的中间件组件还是编写自定义中间件，中间件都为处理交叉关注点和为 ASP.NET Core 3 添加高级功能提供了灵活机制。通过理解中间件的原理以及如何有效地实现和使用它，你可以构建出更模块化、灵活且易于维护的 Web 应用程序，满足用户和业务需求。

## 后台处理：在后台运行耗时任务

ASP.NET Core 3 中的后台处理允许你将耗时或资源密集型任务从主请求处理线程卸载，确保你的 Web 应用程序保持响应和可扩展性。通过在后台执行这些任务，你可以提高应用程序的整体性能、响应能力稳定性。在本指南中，我们将探索 ASP.NET Core 3 中的后台处理、其优势以及如何使用各种技术和库来实现它。

## ASP.NET Core 中的后台任务

在 ASP.NET Core 3 中，可以使用不同的技术实现后台处理，包括托管服务（Hosted Services）、托管后台任务、Hangfire 和 Azure Functions。每种技术都有其优势，并根据你的应用程序的复杂度、可扩展性和需求适用于不同的场景。

### 1. 托管服务（Hosted Services）

托管服务是由 ASP.NET Core 运行时管理的长时间运行后台任务。它们异步运行，且独立于主请求处理线程，允许你在后台执行周期性数据同步、缓存刷新或消息处理等任务。

示例：在 ASP.NET Core 3 中实现托管服务。

```csharp
// MyBackgroundService.cs
public class MyBackgroundService : BackgroundService
{
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            // 执行后台处理任务
            await Task.Delay(TimeSpan.FromSeconds(30), stoppingToken);

            // 执行一些事情...
        }
    }
}
```

在你的 ASP.NET Core 3 应用程序中使用托管服务，你需要使用 `AddHostedService` 扩展方法在 `Startup` 类的 `ConfigureServices` 方法中注册它。

```csharp
// Startup.cs
public void ConfigureServices(IServiceCollection services)
{
    services.AddHostedService<MyBackgroundService>();
}
```

### 2. Hangfire

Hangfire 是一个用于 ASP.NET Core 3 应用程序后台作业处理的流行库。它提供了一个灵活和易用的 API，用于调度和执行后台作业，包括周期任务、触发后忽略（fire-and-forget）任务、延迟任务等。Hangfire 与 ASP.NET Core 无缝集成，允许你使用基于 Web 的仪表板监控、管理和扩展后台作业。

示例：在 ASP.NET Core 3 中使用 Hangfire 进行后台处理。

```csharp
// Startup.cs
public void ConfigureServices(IServiceCollection services)
{
    services.AddHangfire(config =>
        config.UseSqlServerStorage(
            Configuration.GetConnectionString("HangfireConnection")));
}

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    app.UseHangfireDashboard();
    app.UseHangfire();
}
```

### 3. Azure Functions

Azure Functions 是一种无服务器计算服务，允许你在无需配置或管理服务器的情况下运行事件驱动代码。Azure Functions 与 ASP.NET Core 无缝集成，并为后台处理提供了可扩展的解决方案。

示例：创建一个用于后台处理的 Azure Function。

```csharp
// MyFunction.cs
public static class MyFunction
{
    [FunctionName("MyFunction")]
    public static async Task Run(
        [TimerTrigger("0 */5 * * *")] TimerInfo myTimer,
        ILogger log)
    {
        log.LogInformation(
            "C# 触发函数执行于: {DateTime.Now}",
            DateTime.Now);
    }
}
```

## 后台处理的优势

1. **提高性能：** 将耗时或资源密集型任务卸载到后台可以提高 Web 应用程序的整体性能和响应能力，确保其快速且可扩展。
2. **可扩展性：** 后台处理通过释放主请求处理线程来处理传入请求，允许应用程序更高效地扩展。这确保了应用程序能够处理流量高峰而不会变得无响应或过载。
3. **可靠性：** 通过在后台执行关键任务，可以确保即使在主请求流发生故障或中断的情况下也能可靠地完成。
4. **更好的用户体验：** 后台处理通过最小化耗时任务对 Web 应用程序响应和可用性的影响，提升了用户体验。当后台任务异步执行时，用户可以继续与应用程序交互。

# 附录

## C# 和 ASP.NET Core 概念（快速参考）

作为一名使用 ASP.NET Core 3 的 Web 开发者，深入常用的 C# 和 ASP.NET Core 概念至关重要。本快速参考指南提供了关键概念和特性的概述，帮助你高效地导航和开发 ASP.NET Core 应用程序。

### C# 基础

#### 变量与数据类型

```csharp
int age = 30;

string name = "John";

double salary = 2500.50;

bool isActive = true;
```

#### 控制流语句

```csharp
if (age >= 18)
{
    Console.WriteLine("You are an adult.");
}
else
{
    Console.WriteLine("You are a minor.");
}

for (int i = 0; i < 5; i++)
{
    Console.WriteLine($"Iteration {i}");
}

while (isActive)
{
    Console.WriteLine("Active");
}
```

#### 函数

```csharp
public int Add(int a, int b)
{
    return a + b;
}

public void SayHello(string name)
{
    Console.WriteLine($"Hello, {name}!");
}
```

#### 类与对象

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

Person person1 = new Person();

person1.Name = "Alice";
person1.Age = 25;
```

### ASP.NET Core 基础

#### 中间件

```csharp
public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext context)
    {
        // 在将请求传递给下一个中间件之前执行自定义逻辑
        await _next(context);

        // 在请求被下一个中间件处理后执行自定义逻辑
    }
}
```

#### 控制器与动作

```csharp
[Route("api/[controller]")]
[ApiController]
public class UsersController : ControllerBase
{
    private readonly IUserService _userService;

    public UsersController(IUserService userService)
    {
        _userService = userService;
    }

    [HttpGet("{id}")]
    public IActionResult GetUser(int id)
    {
        var user = _userService.GetUserById(id);

        if (user == null)
        {
            return NotFound();
        }

        return Ok(user);
    }
}
```

#### 依赖注入

```csharp
public interface IUserService
{
    User GetUserById(int id);
}

public class UserService : IUserService
{
    public User GetUserById(int id)
    {
        // 从数据库检索用户的逻辑
    }
}
```

#### Razor Pages

```html
@page
@model IndexModel
@{
    ViewData["Title"] = "Home page";
}

<h1>Welcome</h1>
<p>Hello, @Model.Name</p>
```

### 高级 ASP.NET Core 概念

#### 后台处理

```csharp
public class MyBackgroundService : BackgroundService
{
    protected override async Task ExecuteAsync(
        CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            // 执行后台处理任务
            await Task.Delay(
                TimeSpan.FromSeconds(30),
                stoppingToken);
        }
    }
}
```

#### Web APIs

```csharp
[Route("api/[controller]")]
[ApiController]
public class UsersController : ControllerBase
{
    private readonly IUserService _userService;

    public UsersController(IUserService userService)
    {
        _userService = userService;
    }

    [HttpGet("{id}")]
    public IActionResult GetUser(int id)
    {
        var user = _userService.GetByUserId(id);

        if (user == null)
        {
            return NotFound();
        }

        return Ok(user);
    }
}
```

#### 中间件流水线

```csharp
public void Configure(
    IApplicationBuilder app,
    IWebHostEnvironment env)
{
    app.UseMiddleware<CustomMiddleware>();
    app.UseRouting();
    app.UseAuthentication();
    app.UseAuthorization();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });
}
```

### 测试

```csharp
public class UsersControllerTests
{
    [Fact]
    public void GetUser_ReturnsUser_WhenUserExists()
    {
        // 准备
        var userServiceMock = new Mock<IUserService>();
        userServiceMock
            .Setup(s => s.GetUserById(1))
            .Returns(new User { Id = 1, Name = "Alice" });

        var controller = new UsersController(
            userServiceMock.Object);

        // 执行
        var result = controller.GetUser(1);

        // 断言
        Assert.IsType<OkObjectResult>(result);
    }
}
```

## 可能的原因

- CORS 配置缺失或错误。
- 浏览器安全策略不兼容。
- 对预检请求（preflight requests）的处理不当。

## 故障排除

1. 配置 CORS 中间件：确保在 `Startup` 类的 `Configure-Services` 方法中正确配置了 CORS 中间件，以允许来自所需源的请求。

```csharp
services.AddCors(options =>
{
    options.AddPolicy("AllowAll",
```



`builder =>`

```
{
    builder.AllowAnyOrigin()
    .AllowAnyMethod()
    .AllowAnyHeader();
});
```

2. 处理预检请求：实现对预检请求（`OPTIONS`）的处理，响应相应的 `CORS` 头部并允许实际请求继续。

## 5. 数据库连接问题

可能的原因：

- 连接字符串配置错误。
- 数据库服务器宕机或配置错误。
- 访问数据库的权限不足。

故障排除：

1. 验证连接字符串：双检查应用程序配置文件（`appsettings.json`）中的连接字符串，确保它是正确的，并指向正确的数据库服务器和数据库。

2. 测试数据库连接性：使用数据库管理工具或命令行实用程序验证与数据库服务器的连接，并测试 `SQL` 查询或命令。

3. 检查服务器日志：检查服务器日志，查找任何与数据库连接、身份验证或权限问题相关的错误消息或警告。

在 `ASP.NET Core 3` 中排查常见的 `Web` 开发错误需要系统的方法、对的关注以及对 `ASP.NET Core` 框架和 `C#` 语言的熟悉。通过遵循本指南提供的故障排除技巧，并利用开发环境中可用的调试工具和技术，你可以有效地识别并解决 `ASP.NET Core` 应用程序中的错误。请记住彻底测试你的更改，并监控应用程序的行为，以确保问题已成功解决。通过耐心和坚持，你可以克服常见的 `Web` 开发挑战，并使用 `ASP.NET Core 3` 构建稳健可靠的 `Web` 应用程序。
