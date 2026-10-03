
`print(firstInt + " = " + secondInt);`

}

```

正如我们看到的，当我们开始熟悉 C# 的工作原理时，有很多选择。重要的是不要让所有选项让我们感到困惑。同时，知道如何用不同的方式完成单项任务是很好的，我们应该找到一种比另一种更方便的方法。

此外，`ref` 还允许你在函数内部使用该变量。这意味着 `ref` 同时具有输入和输出的可用性。

最后，由你自己决定如何编写和使用函数，以及它们如何改变值。你对这些决定允许你通过代码表达自己的想法和方法。某些编程语言具有不同程度的表达能力。基本上，某些语言更严格，而另一些允许用多种方法执行任何任务。

C# 的表达能力相当高，允许你尝试许多方法来完成某件事。虽然有常见的做法，但绝不意味着你受限于常用的语法。如果你觉得某种不常用的语法更有帮助，请尽管使用它。

## 6.20 数字的类型转换

在开始理解类型转换为什么重要之前，我们需要了解更多关于各种不同数据类型以及它们如何使用的知识。此时，我们需要更多从一种类型到另一种类型的转换。现在我们已经有机会使用了各种数据类型，是时候开始学习在它们之间转换的必要性了。

我们将对象转换为对象，但为什么需要这样做呢？C# 是一种类型安全的编程语言。这意味着你的代码在编译成机器可读代码之前，会对其混合类型进行检查。当在不同类型之间转换时，我们通常看不到太多的错误。在下面的代码示例中，我们演示了为什么我们不想用整数来设置对象的位置。

```csharp
using UnityEngine;
using System.Collections;

public class TypeConversion : MonoBehaviour
{
    public int Zmove;

    // 使用此进行初始化
    void Start ()
    {
        // 每帧被调用一次
        {
            transform.position = new Vector3(0,0,Zint);
        }
    }
}
```

这样做的结果是从一个位置跳到另一个位置的立方体。在新场景中将名为`TypeConversion.cs`的脚本分配给立方体。启动游戏并使用场景编辑器观察修改`Zmove`时立方体的移动。立方体在点与点之间跳跃。整数不能持有分数。然而，其他类型可以。`float`是一个存储小数点位置的数字。

简单来说，整数是一个整数，如 1、2 和 3。分数可以有一个 1 和 2 之间的值，例如 1.5625。因此，如果我们从`int`变为`float`，当我们修改`Zmove`值时，将获得更平滑的移动。然而，当我们把`float`转换为`int`时会发生什么？

```csharp
void Update ()
{
    int Zint = (int)Zmove;
    transform.position = new Vector3(0, 0, Zint);
}
```

在这个代码段中，我们从一个可修改的`Zmove`开始，然后在`Update()`中创建了从`Zmove`到`Zint`的转换。这导致了我们之前观察到的同样的抖动移动。然而，你可能会看到在转换过程中丢失了一些信息。

![](img/05ac639a69dd6f0bc)

对于半字节（nibble）而言，这将 0100 变为正1，而 1100 变为负1。负3 是 1110，负7 是 1111，或者说“负 + 1 + 2 + 4”。

| 类型 | 位数 | 范围 |
| :--- | :--- | :--- |
| `sbyte` | 8 bits | -128 to 127 |
| `Byte` | 8 bits | 0 to 255 |
| `Short` | 16 bits | -32,768 to 32,767 |
| `Unsigned short` | 16 bits | 0 to 65,535 |
| `Int` | 32 bits | -2,147,483,648 to 2,147,483,647 |
| `Unsigned int` | 32 bits | 0 to 4,294,967,295 |
| `Long` | 64 bits | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `Unsigned long` | 64 bits | 0 to 18,446,744,073,709,551,615 |

上表表示了整数的大多数用途。它们中没有一个用于表示小数。带有小数的数字被称为浮点数。到目前为止，我们也使用了`float`和`double`；只是这一点并不那么显易。

## 6.2.3 浮点数

浮点数多年一直是计算机科学家关注的焦点。获得浮点精度是许多早期计算机科学家的目标。因为小数点后面可以跟随无限种可能的数字，因此使用二进制计算无法真实地表示任何分数。

一个常见的例子是 π，我们称其为 pi。假设 3.14 后面有无尽的数字。即使在今天，计算机也可以精确计算出小数点后的几百亿位数字。计算机设置浮点数的某些位来表示小数点的位置，但即使这样也是有限的。

第一部分是通过符号位，设置数字的负正值范围。接下来的 8 位用于指数，其余位是出现在小数点周围的数字。一个`float`值可以将小数点向任意方向移动 3 位，但它限于其能够存储的值。

我们将在第 8.9 节中进一步探讨数字如何用 1 和 0 实际存储。现在只需理解数字只能表示有限的位数。在没有特殊考虑的情况下，计算机无法处理任意大的数字。

将`float`转换为`int`更加显式。这就是为什么 C 要求你使用强制类型转换，并且你需要在`int z = (int)move;`中添加`(int)`。`(int)`是强制转换运算符；或者`(type)`充当从右侧到左侧所需类型的转换器。

## 6.2.4 我们学到了什么

关于数字还有一点需要复习，但我们暂将其放在一边。对于 CPU 来说，它将每个翻译器的信号解释为开启或关闭的开关。计算机将这些翻译器分组以完成任务。浮点运算单元（FPU）是组合在一起的晶体管集合，用于辅助处理浮点数。图形处理器（GPU）是另一组晶体管，专门用于计算图形。

晶体管组是由高度复杂的设计构建的。它们由软件设计的结构被用于构建运行更多软件的硬件。这听起来有点像“先有鸡还是先有蛋”的问题，但至少我们有一些历史参考可以说明这一切的来源。

## 6.2.5 类型与运算符

我们使用的大部分运算符用于相等性判断。在处理数字时，这工作运行良好。然而，对于非数字的类型，我们可以使用比较运算符吗？

比较值从一开始就应该配合类型使用。我们还可以比较什么？

对于数字类型，我们可以使用关系运算符来设置布尔值，例如大于`>`、小于、大于等于`≥`和小于等于`≤`。这些运算符都会产生布尔结果。

```c
float a = 1.0f;
float b = 3.0f;
bool c = a > b;//false
bool d = a < b;//true
```

正如你可能想到的，所有的数学运算符`+`、`-`、`*`、`/`和取模`%`都适用于任何数字类型。然而，我们也可以在字符串类型上使用`+`。

```csharp
// 用于初始化
void Start ()
{
    string a = "hello";
    string b = "world";
    print(a + b);//
}
```

在`print()`中，我们使用`(a + b)`来连接两个字符串。然而，我们不能对字符串使用乘法、减法、除法或取模等比较运算符。

```csharp
// 用于初始化
void Start ()
{
    string a = "hello";
    string b = "world";
    print(a == b);//False
}
```

比较运算符`!=`或不相等在字符串和数字上同样有效。这需要一些直觉，但重要的是学习类型如何相互作用。

```csharp
// 用于初始化
void Start ()
{
    string a = "hello";
    string b = "world";
    print (a != b);//True
}
```

我们可以通过变量比较数据类型。当我们开始定义自己的类型时，这变得很重要。

```csharp
// 用于初始化
void Start ()
{
    int a = 7;
    string b = "hello";
    print (a.GetType() != b.GetType());//True
}
```

C# 中的内置类型有一个名为`GetType()`的函数，允许我们检查每个变量。在这种情况下，`int`不等于`string`，当游戏开始时 Console 会输出：

```csharp
// 用于初始化
void Start ()
{
    int a = 7;
    string b = "7";
    print (a.ToString() == b);//True
}
```

尽管我们有两个不同的类型，我们也可以通过数据类中的`ToString()`函数将`int`转换为`string`。

```csharp
// 用于初始化
void Start ()
{
    int a = 7;
    float b = 7.0f;
    print (a == b);//True
}
```

## 6.2.2 类型强制转换

我们可以在不转换的情况下比较`int`和`float`。这是因为 C# 在进行比较之前隐式地将`int`转换为`float`。然而，C# 并不知道它们是不同的类型。

```csharp
// 用于初始化
void Start ()
{
    int a = 7;
    float b = 7.9f;
    print (a == b);//False
    print ((int)b);//True
}
```

我们可以使用`(int)`对赋值为 7.9 的`float`进行强制转换，我们知道它大于 7。然而，当我们把`float` 7.9 转换为`int`时，我们丢失了小数点后的数字。

```csharp
// 用于初始化
void Start ()
{
    int a = 7;
    string b = "7";
    print (a == (int)b);//无法工作
}
```

没有内置方法允许我们将`string`类型更改为`int`或任何数字类型。因此，类型转换具有局限性。然而，不要让这阻碍了你。比较值从一开始就应该配合类型使用。还可以比较什么？

```csharp
GameObject a = GameObject.CreatePrimitive(PrimitiveType.Capsule);
GameObject b = GameObject.CreatePrimitive(PrimitiveType.Capsule);
print (a == b);//False;
```

正在比较什么？在这里，这些实际上是场景中不同的对象。尽管它们共享相同数量的属性，但它们并不是同一个。比较游戏对象实例的更清晰的方法是使用以下代码：

```csharp
GameObject a = GameObject.CreatePrimitive(PrimitiveType.Capsule);
GameObject b = GameObject.CreatePrimitive(PrimitiveType.Capsule);
print (a.GetInstanceID());
print (b.GetInstanceID());
print (a == b);
```

在这里我们对正在比较的内容更加具体了。如果场景中的每个对象都有唯一的实例，那么当我们需要检查场景中的对象是否匹配时，我们就能清楚地调试并看到正在比较什么。当我们比较场景中没有明确比较方法的对象时，通常有一个方法允许我们在对象之间做出更可读的区分。

```csharp
GameObject a = GameObject.CreatePrimitive(PrimitiveType.Capsule);
GameObject b = a;
print (a == b);//True
```

在这种情况下，它们是同一个对象，但行为是正确的。然而，再次我们应该这样做以确保我们正在方便地比较：

```csharp
void Start () {
    int a = GameObject.CreatePrimitive(PrimitiveType.Capsule);
    a.GetInstanceID();
    int b = a;
    print (a);
    print (b);
    print (a == b);//True
}
```

代码在 Console 面板中产生以下输出：

```
-3474
Unity.MonoBehaviour:print (Object)
TypeCasting:Start () (at Assets/TypeCasting.cs:10)
-3474
Unity.MonoBehaviour:print (Object)
TypeCasting:Start () (at Assets/TypeCasting.cs:11)
True
Unity.MonoBehaviour:print (Object)
TypeCasting:Start () (at Assets/TypeCasting.cs:12)
```

# 424 使用 Unity 3D 学习 C# 编程

```csharp
void Start (){
    GameObject a = GameObject.CreatePrimitive(PrimitiveType.Capsule);
    GameObject b = GameObject.CreatePrimitive(PrimitiveType.Capsule);
    print(a);
    print(b);
    print(a.GetType() == b.GetType());//True
}
```

有一个非常重要的区别。我们从两个`GameObject`类型的对象开始。这让我们比`int`类型拥有更多选项。`GameObject`包含许多函数，允许执行许多复杂的操作。可以检查`GameObject a`和`GameObject b`的类型。因此，`a.GetType()`和`b.GetType()`将返回相同的`GameObject`类型。这里的显著区别在于内存中的数据类型是有类型的，也就是说，每条数据在计算机内存中都有一个特定的形式或形状。

因此，`GameObject`有关联的类型；这也意味着我们可以创建自己的类型。
当我们编写每一个类时，我们都在创建新类型的数据。为了看到这一概念的运行情况，最好是编写几个简单的类进行测试。让我们先看看其他类型用途的。

```csharp
int c = 1;
Debug.Log(c.GetType());
```

上面的代码将以下输出发送到 Console 面板：

```
System.Int32
UnityEngine.Debug.Log(Object)
TypeCasting:Start() (at Assets/TypeCasting.cs:14
```

我们发现`c`是一个`System.Int32`，那么`a`和`b`是什么？

```
UnityEngine.GameObject
UnityEngine.Debug.Log(Object)
TypeCasting:Start() (at Assets/TypeCasting.cs:14
```

`GameObject a`是`UnityEngine.GameObject`，与`b`相同。因为它们是相同的数据类型，所以`a == b`的检查为真。我们应该研究其他几个类型。看看下面的片段：

```csharp
float c = 1.0f;
Debug.Log(c.GetType());
```

通过上面的代码，我们得到以下调试信息发送到 Console 面板：

```
System.Single
UnityEngine.Debug.Log(Object)
TypeCasting:Start() (at Assets/TypeCasting.cs:14
```

尽管我们使用的类型为`float`，但 C# 将其解释为`System.Single`。

```csharp
System.Single c = 1.0f;
Debug.Log(c.GetType());
```
