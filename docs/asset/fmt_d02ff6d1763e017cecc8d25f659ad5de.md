
为了简化操作，我在这里硬编码了一些值来表示汇总后的调查数据。不过，你并不需要理解类也能读这本书。你只需要知道这个文件中包含了一些基本的调查结果数据。在真实的应用程序中，你通常会从其他来源读取这类数据，比如数据库、Web 服务或文本文件。我们跳过了这一步，以便把精力集中在语句和程序流程上。这个项目中的最后一个文件叫做 `SurveyExample.html`。这个文件实际上只是用来说明问题。我们在整本书中都不会实际动手操作它。例如，如果我选择“打开包含文件夹”，这会在文件系统中打开我们的项目。这会显示一个示例调查，其中包含公司向客户提出的问题类型。

![](img/0155736aec718cf18821e9f10a5d308d_515_0.png)

这些问题的答案就体现在我们刚才在 `Q1Results` 中查看的数据里。为了开始使用我们的数据，

```csharp
// declare and assign a variable

string greeting = "hello world";

// add two numbers and store the result

int sum = 2 + 2;

// Log an error to the console

Console.WriteLine("Something went wrong.");

// Run method to get the current user

var user = getCurrentUser();
```

一条语句可以简单到只是声明一个变量并为其赋值。基本的数学计算也是通过语句完成的。如果你曾经向控制台写过字符串或值，那也是一条语句。我们还可以通过语句执行几乎任何函数或方法。像这样的简单语句必须以分号结尾，就像句子以句号结尾一样，这也是一种识别它们的简单方法。由于程序流程是由不同类型的语句组成的，所以这些语句在被处理时也会影响流程。像我们刚才看到的简单语句通常只是一行一行地按顺序执行；但是，某些特殊类型的语句也可以在代码中的其他语句或函数之间创建分支路径。其他类型的语句甚至可以让一段代码连续运行多次。所以，举个例子，之前我们讨论过一些常见问题，比如：我如何根据某些条件决定运行哪段代码？在这种情况下，我们可以使用选择语句，也就是通常所说的 `if/else` 语句。

```csharp
if (todayIsMonday)
{
    sendPhoneReminder();
}
else
{
    sendTextReminder();
}
```

选择语句允许我们使用花括号定义多个代码块，然后根据某些条件决定执行哪一个。所以，如果今天是星期一，我们就发送一个更显眼的电话提醒，而在其他日子则只发送一条短信。这是语句改变程序流程的一个例子，因为只有一个代码块会运行。我们还问过一个问题：我如何用最少的工作一再重复同一项任务？这正是迭代语句派上用场的地方，迭代语句通常被称为循环。

```csharp
// Sends an email to every customer
on the list
foreach (customer in mailingList)
{
    sendEmail(customer);
}
```

循环定义一个会重复执行的代码块，直到满足某个条件为止，例如向邮件列表中的每一位客户发送电子邮件，直到所有客户都发送完。在循环结束之前，程序流程不会继续越过这一点，这同样是通过语句控制程序流程的一种方式。选择语句和迭代语句只是语句中的两种，我们稍后会深入探讨它们，但除此之外还有很多其他类型。我们已经看到了声明语句的例子，它可以用来创建变量。表达式语句则处理常见的任务，比如计算值或执行方法。

| 选择语句 | `if (condition) { // do something }` |
| 迭代语句 | `foreach (item in list) { // do something }` |
| 声明语句 | `string greeting;` |
| 表达式语句 | `int sum = 50 + 50;` |
| 异常处理语句 | `try { // risky code } catch { // fallback }` |

异常处理语句允许我们捕获并解决代码中的问题。同样，语句是在 C# 语言中实际执行操作的完整指令，除了这里列出的基本类型之外，还有其他选择。你可能已经注意到，语句在应用程序中可以跨一行或多行。

```csharp
public decimal GetSalesTax(product item)
{
    var price = item.Price;
    var salesTax = price * 1.06;
    return salesTax;
}
```

单行语句很简单。它们只是一行执行任务并以分号结尾的代码。这里的每一行都是一条语句，它们共同构成了一个完整函数的逻辑。多行语句或复合语句则更有趣一些。

```csharp
if (todayIsMonday)
{
    sendReminderEmails();
    submitTimesheets();
    orderMoreCoffee();
```

这些语句会利用额外嵌入的语句或代码块来执行，这些代码块用左花括号和右花括号定义。在 C# 中，花括号用于标记作用域或定义（如方法或类）的开始和结束。这些代码块可以包含一系列嵌套语句来执行额外的逻辑。复合语句通常会借助特殊的 C# 关键字，这一点我们稍后会介绍。语句有很多类型。在这本书中，我们关注的是那些能显著影响程序流程的最核心语句。首先，我们主要关注较简单的语句类型和相关表达式。接下来，我们将探讨这些概念如何与选择语句结合以影响程序流程，之后还会针对迭代语句做同样的探讨。最后，我们会将许多这些概念汇集起来，探讨管理流程的其他方法。那么，让我们先更仔细地看看一些更简单的单行语句吧。

## 第3章 如何编写简单语句

让我们先通过在应用程序中解决一个简单的任务来熟悉如何编写语句。回到 Visual Studio，让我们重新看看这里的 `Main` 方法。

![](img/0155736aec718cf18821e9f10a5d308d_523_0.png)

现在，这个方法只是像我们之前看到的那样向控制台输出一条简单的消息。在整本书中，我们都会使用我们的调查结果数据，所以让我们看看如何通过语句开始处理这些数据。举一个简单的例子，假设市场团队想知道参与调查的受访者所占的百分比。他们还希望了解未回答调查的具体数量，以便开始跟踪目标数字，为后续改进提供依据。在我们的数据集中并没有直接提供这些具体值，但我们可以用几条语句轻松计算出来。在我们的 `Main` 方法中，让我们先草拟出几个变量来保存这些所需的值。

![](img/0155736aec718cf18821e9f10a5d308d_524_0.png)

```csharp
double responseRate;
double unansweredCount;
responseRate = Q1Results.NumberResponded / Q1Results.NumberSurveyed;
unansweredCount = Q1Results.NumberSurveyed - Q1Results.NumberResponded;
Console.WriteLine($"Response Percentage: {responseRate}");
Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
```

首先，让我们创建一个 `double` 类型的变量，对于必须支持小数的数字来说，这是一个简单易用的选择，就把它叫作 `responseRate`。同时确保用分号结束这条语句。在下一行，让我们再创建一个名为 `unansweredCount` 的 `double` 变量，当然结尾也要加上分号。变量是用来保存数据的，所以让我们计算想要存储的值。在新的一行，我们写上 `responseRate =`，请记住在 C# 中单个等号表示赋值，因此我们需要一个值赋给这个变量。为此，让我们访问调查数据。我会输入 `Q1Results` 来访问那个类或数据集，然后我们可以使用点语法来访问它的属性，也就是那个类上的数据。Visual Studio 会显示所有可访问的属性，所以我们选择 `NumberResponded`。要得到平均值，我们必须用它除以受访人数，并且和往常一样，确保用分号结束语句。这个计算结果会存储在我们的变量中，供之后使用。我们想用同样的步骤来找出未回答调查的数量。让我们在下一行处理这个，以加深对这种模式的印象。所以让我们输入 `unansweredCount = Q1Results.NumberSurveyed - Q1Results.NumberResponded` 可以为我们提供第二个值。接下来，我们只需在应用运行时将这些值显示给用户。再往下，我们还有第三条语句在应用运行时打印 Hello world，让我们把它改得更实用一些。在 C# 中，我们可以用美元符号作为字符串前缀，这样处理变量会更方便。这个特殊字符允许我们使用花括号将变量直接注入字符串。所以我们把文本改为 Response Percentage 加一个冒号，然后添加一对花括号并传入 `responseRate` 变量。由于美元符号前缀，C# 在打印字符串时会自动从该变量中取出对应的值。接下来，我们复制这行代码并粘贴到下一行，然后把文本改为 Unanswered Surveys，并将变量改为 `unansweredCount`。这样我们现在有六条语句。前两条是声明语句，用于声明新变量。接下来两条是表达式语句，用于计算并给这些变量赋值。最后这两条也是表达式语句，用于打印存储在变量中的值。稍后我们会更详细地讨论表达式语句，但它们是你在 C# 中编写的最常见的语句类型，尤其是像这样简单的单行语句。语句设置完成后，让我们运行应用，看看会发生什么。Visual Studio 需要一点时间来编译并启动我们的程序，然后过一会儿，我们应该会看到完成调查的人的百分比数字，以及未响应人数。

![](img/0155736aec718cf18821e9f10a5d308d_525_0.png)

我确实想说明一下，这段代码故意写得冗长，以便清晰地展示不同类型的语句，但实际上它可以用几种方式优化。例如，我们可以在初始化变量的同时进行加法运算。我们可以删掉计算值的语句，直接将它们与上面的声明语句合并，一步完成所有工作，就像这样：

```csharp
double responseRate = Q1Results.NumberResponded / Q1Results.NumberSurveyed;
double unansweredCount = Q1Results.NumberSurveyed - Q1Results.NumberResponded;
Console.WriteLine($"Response Percentage: {responseRate}");
Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
}
```

这种风格更接近你在大多数 C# 应用中实际看到的写法，而且更加简洁。所以我们有了一个良好的开端。我们已经使用了几条简单语句来检索、存储和显示一些基本数据。接下来，让我们更深入地探讨这类语句的结构。

## 第4章 如何探索语句和表达式

让我们以更具技术性的思路来研究语句，以更好地理解它们的结构。之前，我们看到了语句的概念性定义。现在，让我们将其扩展为更具体的 C# 语言术语。语句是使用 C# 关键字和表达式的组合编写的完整指令。你已经接触过 C# 关键字。这些是 C# 语言本身的保留字，具有特殊含义，例如 `public`、`int`、`bool` 或 `new`。某些特定类型的语句也有自己的保留关键字，例如我们稍后会探讨的 `if/else` 选择语句。现在，让我们专注于定义中的表达式部分，它是语句的核心构建块。表达式就是操作数和运算符的序列。这个定义听起来比实际要吓人得多。表达式实际上只是一小段代码，通常会产生一个值，如果我们看一些示例，会更容易理解。举个简单的例子，`2 x 3` 是一个表达式，结果为 6。在这种情况下，2 和 3 被称为操作数，乘号是运算符。`HighScore +1` 是一个表达式，因为它有两个操作数：变量 `highScore` 和数字 1，以及一个加法运算符。`New Survey` 也是一个表达式，因为 `new` 是运算符，`Survey` 类型是操作数。甚至单独的数字 5 在技术上也是一个表达式，因为简单的数字就是一个操作数，并且会产生一个值。因此，运算符只是对操作数应用某种类型的运算来产生结果。你可以宽松地把它们想象成名词和动词：操作数是名词，运算符是作用于该名词的动词。

| 算术 | `+` | `/` | `-` |
| 比较 | `>` | `<` | `>=` |
| 布尔逻辑 | `!` | `&&` | `\|\|` |

C# 中有几十个运算符可用于构建语句，这里列出了其中的一小部分。运算符可以包括从加法数学符号到大于或小于比较，再到判断条件为真或假的逻辑运算符等各种符号。退一步说，理解表达式本身并不是语句这一点很重要。语句使用表达式，但表达式不能单独作为完整指令存在。这个区别非常重要，所以让我们比较一些表达式和语句。`2 + 2` 是一个表达式，但我们不能在没有上下文的情况下直接在 C# 程序中单独写 `2 + 2`。应用甚至无法编译这段代码。表达式语句会使用这个表达式，但会将结果存储在变量中，并用我们信赖的分号结束，从而形成一条完整指令。计算 `true` 或 `false` 布尔值也是表达式的常见用途，但完整的语句同样需要赋值和分号。有些表达式大多可以独立存在，例如创建新对象或执行方法，但它们仍然需要结尾的分号才能形成完整语句。这本书当然不是对表达式的深入探讨。就我们的目标而言，我们只需要在语句的上下文中理解几个关键概念。语句由 C# 关键字和表达式组成，并以分号或花括号结尾。表达式是运算符和操作数的组合，通常会产生一个值。运算符作用于操作数以产生该值。当我们开始处理其他类型的语句时，表达式将变得更加重要。但现在，让我们练习编写不同类型的简单表达式语句。在此过程中，只要你记住这些概念并开始识别代码中的一些通用模式，你将会在前进的道路上处于更好的位置。

让我们扩展之前用 C# 语句所做的练习，尝试一些不同的表达式。在我们的 `Main` 方法中，前两条语句都明显使用了表达式。例如，第一条语句使用除法运算符作用于这两个操作数，以计算平均值。第二条语句使用减法运算符再次作用于两个值（或操作数），以计算差值。

```csharp
double responseRate = Q1Results.NumberResponded / Q1Results.NumberSurveyed;
double unansweredCount = Q1Results.NumberSurveyed - Q1Results.NumberResponded;
Console.WriteLine($"Response Percentage: {responseRate}");
Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
```

等号运算符也被用来将计算出的值赋给变量。好了，让我们切换到调查数据，探索另一种可以使用表达式语句完成任务的情景。

```csharp
double responseRate = Q1Results.NumberResponded / Q1Results.NumberSurveyed;
double unansweredCount = Q1Results.NumberSurveyed - Q1Results.NumberResponded;
double overallScore = (Q1Results.ServiceScore + Q1Results.CoffeeScore + Q1Results.FoodScore + Q1Results.Price
Console.WriteLine($"Response Percentage: {responseRate}");
Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
Console.WriteLine($"Overall Score: {overallScore}");
```
