

## REVIEW

List at least three differences between classes and structures:

One of the following is NOT a good reason to use an enumeration. Which one?

- Enumerations make passing parameters more reliable.
- Enumerations make a list of options easier to remember.
- Enumerations guarantee that the argument passed to a method will be valid.
- You can (sometimes) avoid a lot of code by using the constant names.

The statement Int32 MyProperty {get; set;} can mean two different things depending on where it's used. What two types allow the statement, and what does it mean in each case?

Using the example class hierarchy from this chapter, what code would you need to pass an instance of Component to a method with the signature DoSomething(Ingredient)?

What keyword do you need to use to persist changes made to an argument once a method exits? Where must you use it?

Congratulations! You've finished the chapter. Take a minute to think about what you've accomplished before you move on to the next one...

List three things you learned in this chapter:

- 1
- 2
- 3

Why do you think you need to know these things in order to be a C# programmer?

Is there anything in this chapter that you think you need to understand in more detail? If so, what are you going to do about that?

## 第1部分：类库

在过去几章中，你学习了如何创建 .NET Framework 类型和成员的基础知识。现在是时候稍微退后一步，查看框架类库 (FCL) 中为你提供的庞大类型库了。在本章中，我们将查看核心数据类型，这些类型将帮助你处理数值数据、字符数据以及日期和时间。在下一章中，我们将继续学习允许你处理对象多个实例的类型，以及一种称为泛型的特殊构造，它允许你在运行时指定类型。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_317_0.png)

## 如何契合

与类一样，结构体、枚举和接口是使用 C# 类型和成员关键字（其中许多你已经了解）实现的，最终会被转换为 .NET Framework CTS（公共类型系统）类型。在本章中，我们将查看这些剩余类型，以及它们如何融入 CTS。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_318_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_318_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_318_2.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_318_3.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_318_4.png)

## .NET 框架

## 类库

类库按命名空间组织。System 是根。

## 其他核心类型

## 可空类型

## 布尔类型

## System 命名空间

我们将在本章详细介绍这些类型。

## 字符类型

## 字符串

## 字符

## 字符串生成器

## 时间与日期

## 日期时间

## 时间跨度

## 日期时间偏移量

## 时区信息

## 数值类型

## 数学

## Int32 等

元类型用于创建其他类型或提供有关它们的信息。

## 元类型

## 类型

## 对象

## 聚合类型

我们将在下一章讨论这些内容。

## 示例...

为了了解 .NET Framework 类库为你提供了多少功能，请看看这个厨房计算器，以及创建它所涉及的类列表。

字符串——除此之外，String 类知道如何从一组字符创建自身，将自身与另一个字符串进行比较，并在自身中查找单个字符。

窗口——Window 类充当容器。它显示主计算器窗口、标题栏以及“最小化”、“最大化”和“关闭”按钮。它提供移动、调整大小和关闭应用程序的功能。

Int32——它知道如何对自身执行基本数学函数，并将自身显示为字符串。

文本框——计算结果显示在 TextBox 中。它支持选择字体和大小、显示文本，并提供所有标准 Windows 编辑功能，如剪切、复制和粘贴。它甚至允许你对其内容进行拼写检查。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_320_0.png)

按钮——这些小部件是 Button 类的实例。按钮知道如何显示自身，以及如何响应单击事件。

网格——Grid 知道如何以行和列显示其内容，并在窗口大小改变时调整大小和重新排列它们。

单选按钮——窗体顶部的三个按钮是 RadioButton 类的实例。它们知道自己处于一个组中，当用户单击其中一个时，它不仅保持选中状态，还会“取消选中”组中的所有其他按钮。

Can you imagine writing all this from scratch?

## 任务列表

在本章中，我们将首先了解 FCL 的组织方式，以及几种在其中找到方向的方法。然后我们将研究支持三类核心数据的类型：数值、字符和时间。

### 命名空间

我们将首先了解命名空间，这是 .NET Framework 中将类型组织成逻辑组的主要方式，以及如何访问和创建它们。

### 对象浏览器

我们已经使用过对象浏览器，但在本章中我们将更详细地了解它——它是浏览类库的最佳工具之一。

### 数值数据

迄今为止，我们主要使用 Int32 类来存储数值数据，但 FCL 提供了近十种（确切地说是十一种）用于存储不同类型数值数据的类型，我们将在此处进行考察。我们还将快速查看 Math 类，它提供对三角函数、对数函数及其他高级数学函数的支持。

### 字符数据

在查看完数字后，我们将查看文本，具体是 String、Char 和 StringBuilder 类，它们允许你存储和操作字符数据。

### 时间数据

大多数人倾向于将日期和时间视为数字，事实是它们通常以这种方式表示，但时间是一件棘手的事情，FCL 提供了一些类型，使其（如果不容易的话，至少）更容易操作。

## 命名空间

这里有两个你可能习惯看到的识别代码。第一个是北美电话号码，第二个是美国社会安全号码。在这两种情况下，我们通常不会过多思考最终代码中各个组件的含义；我们只是将它们视为黑盒。但它们确实有含义，有时解码它们很有用。

3-digit country code. You'll need this for international calls.

3-digit exchange code. In the early days of telephony, you only needed this when dialing a different exchange.

+999 (999) 999-9999

3-digit area code. You'll need this for out-of-area calls.

4-digit subscriber number. You always need this and sometimes you need an extension number, as well.

Encoded date of issue

999-99-9999

State in which code was issued

Individual identifier

There are two ways of identifying a class in the FCL. Like a phone number, sometimes you can ignore parts of them, and sometimes you can’t. Namespaces are used to organize types into logical groups. This is how you’ll refer to a type in your code, just like the phone number you use to call someone.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_323_0.png)

The object hierarchy defines the capabilities of the type. You’ll need it to understand where the type lives in the hierarchy, because it inherits the capabilities of all its ancestors.

```
System.Object
System.Windows.Threading.DispatcherObject
System.Windows.DependencyObject
System.Windows.Media.Visual
System.Windows.UIElement
System.Windows.FrameworkElement
System.Windows.Controls.Control
System.Windows.Controls.ContentControl
System.Windows.Controls.Primitives.ButtonBase
System.Windows.Controls.Button
```

The class hierarchy and namespace hierarchy aren’t related. Notice that Button inherits from types in the Threading, Media and Controls namespaces, but Button itself is in the Controls namespace.

