
Q1Results.NumberResponded 可以为我们提供第二个值。接下来，我们只需在应用运行时将这些值显示给用户。再往下，我们还有第三条语句在应用运行时打印 Hello world，让我们把它改得更实用一些。在 C# 中，我们可以用美元符号作为字符串前缀，这样处理变量会更方便。这个特殊字符允许我们使用花括号将变量直接注入字符串。所以我们把文本改为 Response Percentage 加一个冒号，然后添加一对花括号并传入 responseRate 变量。由于美元符号前缀，C# 在打印字符串时会自动从该变量中取出对应的值。接下来，我们复制这行代码并粘贴到下一行，然后把文本改为 Unanswered Surveys，并将变量改为 unansweredCount。这样我们现在有六条语句。前两条是声明语句，用于声明新变量。接下来两条是表达式语句，用于计算并给这些变量赋值。最后这两条也是表达式语句，用于打印存储在变量中的值。稍后我们会更详细地讨论表达式语句，但它们是你在 C# 中编写的最常见的语句类型，尤其是像这样简单的单行语句。语句设置完成后，让我们运行应用，看看会发生什么。Visual Studio 需要一点时间来编译并启动我们的程序，然后过一会儿，我们应该会看到完成调查的人的百分比数字，以及未响应人数。

![](img/0155736aec718cf18821e9f10a5d308d_525_0.png)

我确实想说明一下，这段代码故意写得冗长，以便清晰地展示不同类型的语句，但实际上它可以用几种方式优化。例如，我们可以在初始化变量的同时进行加法运算。我们可以删掉计算值的语句，直接将它们与上面的声明语句合并，一步完成所有工作，就像这样：

```
double responseRate = Q1Results.NumberResponded / Q1Results.NumberSurveyed;
double unansweredCount = Q1Results.NumberSurveyed - Q1Results.NumberResponded;

Console.WriteLine($"Response Percentage: {responseRate}");
Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
}
```

这种风格更接近你在大多数 C# 应用中实际看到的写法，而且更加简洁。所以我们有了一个良好的开端。我们已经使用了几条简单语句来检索、存储和显示一些基本数据。接下来，让我们更深入地探讨这类语句的结构。

## 第4章 如何探索语句和表达式

让我们以更具技术性的思路来研究语句，以更好地理解它们的结构。之前，我们看到了语句的概念性定义。现在，让我们将其扩展为更具体的 C# 语言术语。语句是使用 C# 关键字和表达式的组合编写的完整指令。你已经接触过 C# 关键字。这些是 C# 语言本身的保留字，具有特殊含义，例如 public、int、bool 或 new。某些特定类型的语句也有自己的保留关键字，例如我们稍后会探讨的 if/else 选择语句。现在，让我们专注于定义中的表达式部分，它是语句的核心构建块。表达式就是操作数和运算符的序列。这个定义听起来比实际要吓人得多。表达式实际上只是一小段代码，通常会产生一个值，如果我们看一些示例，会更容易理解。举个简单的例子，2 x 3 是一个表达式，结果为 6。在这种情况下，2 和 3 被称为操作数，乘号是运算符。HighScore +1 是一个表达式，因为它有两个操作数：变量 highScore 和数字 1，以及一个加法运算符。New Survey 也是一个表达式，因为 new 是运算符，Survey 类型是操作数。甚至单独的数字 5 在技术上也是一个表达式，因为简单的数字就是一个操作数，并且会产生一个值。因此，运算符只是对操作数应用某种类型的运算来产生结果。你可以宽松地把它们想象成名词和动词：操作数是名词，运算符是作用于该名词的动词。

| 算术 | + | / | - |
| 比较 | > | < | >= |
| 布尔逻辑 | ! | && | \|\| |

C# 中有几十个运算符可用于构建语句，这里列出了其中的一小部分。运算符可以包括从加法数学符号到大于或小于比较，再到判断条件为真或假的逻辑运算符等各种符号。退一步说，理解表达式本身并不是语句这一点很重要。语句使用表达式，但表达式不能单独作为完整指令存在。这个区别非常重要，所以让我们比较一些表达式和语句。2 + 2 是一个表达式，但我们不能在没有上下文的情况下直接在 C# 程序中单独写 2 + 2。应用甚至无法编译这段代码。表达式语句会使用这个表达式，但会将结果存储在变量中，并用我们信赖的分号结束，从而形成一条完整指令。计算 true 或 false 布尔值也是表达式的常见用途，但完整的语句同样需要赋值和分号。有些表达式大多可以独立存在，例如创建新对象或执行方法，但它们仍然需要结尾的分号才能形成完整语句。这本书当然不是对表达式的深入探讨。就我们的目标而言，我们只需要在语句的上下文中理解几个关键概念。语句由 C# 关键字和表达式组成，并以分号或花括号结尾。表达式是运算符和操作数的组合，通常会产生一个值。运算符作用于操作数以产生该值。当我们开始处理其他类型的语句时，表达式将变得更加重要。但现在，让我们练习编写不同类型的简单表达式语句。在此过程中，只要你记住这些概念并开始识别代码中的一些通用模式，你将会在前进的道路上处于更好的位置。

让我们扩展之前用 C# 语句所做的练习，尝试一些不同的表达式。在我们的 Main 方法中，前两条语句都明显使用了表达式。例如，第一条语句使用除法运算符作用于这两个操作数，以计算平均值。第二条语句使用减法运算符再次作用于两个值（或操作数），以计算差值。

```
double responseRate = Q1Results.NumberResponded / Q1Results.NumberSurveyed;
double unansweredCount = Q1Results.NumberSurveyed - Q1Results.NumberResponded;

Console.WriteLine($"Response Percentage: {responseRate}");
Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
```

等号运算符也被用来将计算出的值赋给变量。好了，让我们切换到调查数据，探索另一种可以使用表达式语句完成任务的情景。

```
double responseRate = Q1Results.NumberResponded / Q1Results.NumberSurveyed;
 double unansweredCount = Q1Results.NumberSurveyed - Q1Results.NumberResponded;

double overallScore = (Q1Results.ServiceScore + Q1Results.CoffeeScore + Q1Results.FoodScore + Q1Results.Price
Console.WriteLine($"Response Percentage: {responseRate}");
Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
Console.WriteLine($"Overall Score: {overallScore}");
```

假设市场部门想知道所有四个主要类别的总体平均分。目前我们只有单个分数，如果能有一个总体平均值来跟踪，那就太好了。那么，让我们切换回 Program.cs 中的 Main 方法。在现有计算的下方，我们先声明另一个变量。这个变量也需要存储一个小数值，所以让我们再次使用 double 数据类型，并将其命名为 overallScore。要计算总体得分，我们必须将四个单独分数相加，然后除以总类别数，就像任何其他标准数学平均值一样。因此，在 overallScore 的分号前，让我们开始访问不同的类别。让我们输入 Q1Results.ServiceScore，然后使用加号运算符加上 Q1.CoffeeScore，再加 Q1.FoodScore，最后加上 Q1.PriceScore。我们还必须将这些项目的总和除以 4，才能得到平均值。C# 遵循数学运算顺序，就像任何其他编程语言一样。因此在这种情况下，除法实际上会先执行，然后其他所有分数才会相加。这肯定不是我们想要的结果。我们可以通过简单地将加法括在一组括号中来修复这个问题，这将确保分数在除法之前相加。最后，让我们复制一条 Console.WriteLine 语句并粘贴到底部。我们可以将标签改为 Overall Score，然后传入匹配的变量。一切就绪后，让我们运行应用，看看会得到什么结果。
