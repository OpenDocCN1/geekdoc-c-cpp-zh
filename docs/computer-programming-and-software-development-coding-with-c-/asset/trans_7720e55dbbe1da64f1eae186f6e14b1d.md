

manipulate that code, tools that tend to work better in C# than they do in many other languages. And indeed, throughout this book, I casually slipped in little moments when I used those automated tools. For example, I used features like AutoComplete to write code, or AutoCorrect to fix errors in the code, and AutoCorrect is not just about fixing errors. It can also fix the style of your code. For example, I just realized that I declare that this methods says static public, but the officially recommended style for method declarations is that access modifiers like public should come first. It should be public static float, and the same for these other methods, but I don't have to remember these details.

```
```csharp
static public float FahrenheitToCelsius(float temperatureFahrenheit)
{
```
```

I can ask Visual Studio to reorder the modifiers for me. So it helps me fix errors and also to keep a uniform coding style.

![](img/0155736aec718cf18821e9f10a5d308d_507_0.png)

Small things, but especially important on large projects with many developers. And besides AutoComplete and AutoCorrect, Visual Studio has other features that take advantage of the IDE understanding the code, like navigation features to jump from a method to its declaration quickly, and so on. We also saw how smart the debugger is in Visual Studio, and that's also in part because Visual Studio understands your code, so it can do things like only show you the most interesting, most relevant variables at a given time. And also

the refactorings we did. Remember when we asked Visual Studio to remove temporary variables, or replace a string concatenation with the string interpolation, and that was only basic refactorings.

![](img/0155736aec718cf18821e9f10a5d308d_508_0.png)

There are plugins for Visual Studio or other C# IDEs that give you amazingly powerful automated refactorings. Sometimes I can go on coding for minutes and I barely ever type code. I just use refactorings to change code like I want it.

![](img/0155736aec718cf18821e9f10a5d308d_508_1.png)

And Visual Studio sometimes can even generate snippets of code for you. In the beginning, we generated a Hello World program. That was a terrible example, maybe, but you might remember that at some point, Visual Studio said, what's this console with two l's saying? Maybe you want me to generate it for you? We did not use that feature, but it was there. So yes, you have to write a lot of code in C#, but you often don't type all that code yourself. Your IDE

## c#
## 编码基础
## 控制流语句和表达式
RICHIE MILLER

## 引言

程序流程是我在开发中最喜欢的话题之一，因为在很多方面它确实描述了编程的核心。你每天都在实践程序流程，即使你还没有意识到。假设有位鲍勃，他有一个例行公事，就像我们所有人一样。每天早上醒来时，他的生活会根据各种因素以不同的方式展开。他当天处理的任务以及完成的顺序在一周内会不断变化。周一，鲍勃醒来，去上班，然后回家吃晚饭放松。他在整个星期重复这种基本的活动例行公事。当然，他吃的东西或在工作中的事情会有细微变化，但那个核心循环保持不变。周末，鲍勃的例行公事则完全不同。不是去上班，他会带着狗去公园，周末晚上和朋友外出。这里的关键概念是，鲍勃的活动以及他完成的顺序会根据各种因素而改变。每一天都是由常量和变量组成的例行公事。每天都会起床。工作日每天都会去上班。每天都会吃晚饭，但食物选择不同。有些任务每天完全不同。随着时间的推移，我们被编程去执行这类例行公事以实现更大的目标。好吧，这些同样的想法也适用于我们的应用程序。当很多人想到一个应用时，他们通常会想象许多行代码简单地按顺序执行并产生某种结果。在某些情况下这是真的，但就像我们自己的例行公事一样，随着应用程序的成熟和复杂性增长，事情并不总是这么简单。大多数重要的应用必须根据各种条件以不同的顺序执行不同的代码片段。也许前几行会执行，然后接下来的几行执行只有管理员才被允许执行的任务。代码不会立即运行，而是跳转到另一个文件来判断该用户是否有权限执行此操作。如果没有，该代码段将被跳过，而不同逻辑会运行，告诉用户他们没有访问权限。这是一个简单的程序流程示例。程序流程管理应用程序代码的不同部分在何种顺序和条件下被执行。它为我们的应用何时以及如何采取某些行动或做出决策、处理重复性任务等提供了结构。如果你正在阅读这本书，你可能已经具备了一些基本的 C# 技能，比如知道如何创建和使用变量。你了解代码文件是什么，并且可能熟悉 C# 程序的总体结构。这些是入门的关键构建块，也是我们将开始用程序流程来控制的部分。本书将帮助你利用这一基础开始构建更有意义、更复杂的应用程序。我们将解决 C# 中常见的程序流程挑战。我们将回答诸如我的应用如何根据特定数据做出决策、我的程序如何多次重复一个任务，或者更一般地说，我的程序还能采取哪些其他类型的操作来影响程序流程等问题。好吧，在开始回答这些问题之前，让我们先设置一个简单的应用程序来做实验。

## 第 1 章 如何设置示例项目

让我们探索一下我们将在整个课程中用来学习 C# 程序流程的示例应用。假设一家公司是一家不断发展的区域连锁咖啡店。为了优化增长，他们希望了解产品和服务在消费者中的反响如何。市场团队快速制作了一份季度客户调查来实现这一目标。调查已发送给客户，随着时间的推移，大多数结果终于回来了。不幸的是，调查工具非常基础，只能以简化的数据格式导出结果，因此市场团队要求开发人员分析这些数据以寻找关注点并回答某些问题。而这就是我们要做的。我们将使用一个简单的 C# 控制台应用程序，并利用控制流、语句和 C# 逻辑来处理这些数据。在 Visual Studio 中我打开了我们的项目，你应该能看到这个解决方案节点。解决方案基本上只是一个项目的容器，我们有一个项目，即我们的报告应用程序。该项目中目前有几个感兴趣的文件。第一个是我们的 Program.cs，这应该有点熟悉，所以让我们快速打开它。

```
```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello world!");
    }
}
```
```

Program.cs 是我们 C# 应用的主要入口点。当我们启动应用程序时，这里 main 方法将执行其中的内容。目前，我们只有一些代码用于在控制台显示 Hello world。就程序流程而言，一切都将从这里开始。为了确保应用程序能够正确编译和运行，让我们按下 Visual Studio 顶部的开始按钮来启动应用。于是我们应该很快看到 Hello world 消息打印到控制台。这意味着一切设置正常，让我们关闭这里并返回到我们的项目。

![](img/0155736aec718cf18821e9f10a5d308d_514_0.png)

现在在我们的解决方案资源管理器中，我们还有一个名为 Q1Results 的文件。该文件包含一个类，用于保存一些示例调查结果数据。在 C# 中，类代表我们代码中的对象或概念，并且可以使用属性为我们保存数据，比如我们在这里看到的 CoffeeScore 或 FoodScore。

```
14    public static double PriceScore { get; set; } = 6.0;
15
16    public static double FoodScore { get; set; } = 7.5;
17
18    public static double WouldRecommend { get; set; } = 7.5;
19
20    public static string FavoriteProduct { get; set; } = "Cappucino";
21
22    public static string LeastFavoriteProduct { get; set; } = "Granola mix";
23
24    // Aggregate counts
25    public static double NumberSurveyed { get; set; } = 500;
26
27    public static double NumberResponded { get; set; } = 325;
28
29    public static double NumberRewardsMembers { get; set; } = 130;
30    }
31 }
```

