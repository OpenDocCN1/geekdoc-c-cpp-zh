
if(condition)
{
	statement;
	statement;
	statement;
}
else if(another condition)
{
	statement;
	statement;
}
else
{
	statement;
	statement;
}

- 关系运算符 ==、!=、<、>、<= 和 >= 的工作原理也与其他编程语言非常相似——它们分别用于检查值是否相等、是否不相等、是否小于、是否大于、是否小于等于或是否大于等于。
- 布尔类型通过 ! 运算符取反。
- AND（&&）运算符和 OR（||）运算符用于同时比较多个条件，其工作方式与 Java 和 C++ 中完全相同。
- 你可以嵌套 if 语句——但不要过度使用。

## 下一步是什么？

if 语句是编程中至关重要的一部分，因为它们是决策的核心。所有计算机编程语言都包含某种形式的 if 语句，正因如此，尽管有些人可能不认同，HTML 并不是一种真正的编程语言。

接下来，我们将了解 switch 语句，它是一种与 if 语句功能类似但实现方式不同的结构。

## Switch 语句

在上一节中，我们讨论了决策和 if 语句的使用。现在我们将讨论一种与这些 if 语句类似的结构；它被称为 switch 语句。

说实话，任何用 switch 语句能完成的事情都可以轻松地用 if 语句完成。本指南后面不会再使用其他 switch 语句，但你在编程之旅中很可能会遇到它们，因此你确实需要理解它们。

### Switch 语句基础

变量是 C# 编程中常见的一部分，根据变量的值执行不同的操作是很常见的。例如，假设我们有一个包含五个不同选项的菜单。程序用户输入他们的选择，我们将该值放入一个变量中。无论他们选择菜单中的哪个选项，都会导致执行不同的操作。

利用你已经学到的知识，你可以编写一个复杂的 if else-if 语句，看起来就像 if else-if、else-if、else-if else。它大致如下所示：

```csharp
int menuChoice = 3;

if (menuChoice == 1)
{
    Console.WriteLine("You chose the first option.");
}
else if (menuChoice == 2)
{
    Console.WriteLine("You chose the second option. That’s a good one!");
}
```

```csharp
} 
else if (menuChoice == 3)
{
	Console.WriteLine("I can't believe you chose the third option.");
}
else if (menuChoice == 4)
{
	Console.WriteLine("You can do better than choosing the fourth option....");
}
else if (menuChoice == 5)
{
	Console.WriteLine("? You really want the fifth option?");
}
else
{
	Console.WriteLine("Hey! That option doesn't exist!");
}
```

这样做的确可以完成任务，但我们也可以使用 switch 语句来完成同样的事情。这需要使用 switch 关键字，并且对于菜单中的每个 case 或选项，使用 case 关键字。还包括我们稍后将讨论的另外两个关键字——default 和 break。

作为 switch 语句，上面的 if 语句现在看起来像这样：

```csharp
int menuChoice = 3;
```

```csharp
switch (menuChoice)
{
  case 1:
    Console.WriteLine("You chose the first option");
    break;
  case 2:
    Console.WriteLine("You chose the second option. That's a good one!");
    break;
  case 3:
    Console.WriteLine("I can't believe you chose the third option.");
    break;
  case 4:
    Console.WriteLine("You can do better than choosing the fourth option....");
    break;
  case 5:
    Console.WriteLine("? 5? You really want the fifth option?");
    break;
  default:
    Console.WriteLine("Hey! That option doesn't exist!");
    break;
}
```

正如你所看到的，我们以 switch 语句开始，并将要切换的变量括在括号中。可以把 switch 想象成铁路道岔；当它被使用时，它会改变火车的行驶方向。

接下来，我们有一系列 case 语句。这些也被称为 case 标签，用于指示变量是否与 case 语句的值匹配，以及代码块是否是执行流程将要前往的地方。

需要特别注意的一点是，执行流程只会准确进入一个 case 标签，因此永远不会出现两个或多个 case 块被执行的情况。

在每个 case 块的末尾，必须有 break 关键字；这就是将执行流程送出 switch 语句并进入下一个代码段的关键。注意，我们还有一个 default 标签。它用于表示，如果没有其他 case 标签匹配，执行流程应转向此处。你不必把 default 标签放在最后，但通常这是最常用的位置，也是最佳实践。这是因为 default 块会捕获不属于任何 case 标签特定情况的任何内容。此外，它还可替代原来冗长的 if 语句中的最后一个 else 块。

请注意，switch 语句中的 case 条件不接受一般逻辑。if 语句可以是这样：

```
if(x < 10)
```

然而，你不能这样做：

```
case x < 10:
```

你也不能这样做：

```
case < 10:
```

如果你需要复杂的逻辑，那就改用 if 语句。

### 用于 Switch 语句的类型

在上面的示例中，我们使用了 int 类型。虽然许多类型可以用于 switch 语句，但并非所有类型都可以。可以使用的类型包括：

- bool
- char
- string
- int
- byte
- short
- long
- ulong
- ushort
- ubyte
- uint

枚举类型也可以用于 switch 语句——我们还没有讲到这些。

### 隐式贯穿

如果你使用过 Java 或 C++，你可能已经知道一个技巧：当省略 break 语句时，case 块会“贯穿”到下一个 case 块。因此，在这两种语言中，你可以这样写：

```
// This won’t work in C#
switch (menuChoice)
{
case 1:
Console.WriteLine("You chose option 1.");
case 2:
Console.WriteLine("You chose option 2.  Or maybe you chose option 1.");
break;
}
```

因为第一个 case 没有 break，代码会执行，然后继续向下执行到第二个 case，直到遇到 break 语句。在 C# 中，这种情况不会发生，因为每个 case 块都必须有一个 break 语句。

这样要求的原因是，在很多情况下，break 语句可能会被意外遗漏，从而产生 bug。这个 bug 并不容易修复；为了防止这种情况发生，C# 不允许省略 break 语句，从而消除了贯穿现象。

然而，在 C# 中，如果你有几个 case 块之间没有任何代码，也可以这样做：

```
// This will work in C#
switch (menuChoice)
{
case 1:
case 2:
Console.WriteLine("You chose option 1 or 2.");
break;
```

这样做的效果是，无论值是 1 还是 2，都执行相同的操作。尽管 case 1 没有 break 语句，但实际上并不需要；我们只是在说 case 1 和 case 2 是相同的。

你也可以使用 if 语句完成完全相同的事情。

### 快速入门

switch 语句是编写多个 if else-if 块的另一种方式。与其这样写：

```
int menuChoice = 2;
if(menuChoice == 1)
{
Console.WriteLine("You chose the first option");
}
else if(menuChoice == 2)
```

```csharp
{
Console.WriteLine("You chose the second option. That's a good one!");
}
else
{
Console.WriteLine("I don't know what to do with that number.");
}
```

你应该这样写：

```csharp
int menuChoice = 2;

switch (menuChoice)
{
case 1:
	Console.WriteLine("You chose the first option");
	break;
case 2:
	Console.WriteLine("You chose the second option. That's a good one!");
	break;
default:
	Console.WriteLine("I don't know what to do with this number.");
	break;
}
```

- 你可以在 switch 语句中使用 bool、char、string、int、uint、long、ulong、short、ushort、byte 和 ubyte 类型。
