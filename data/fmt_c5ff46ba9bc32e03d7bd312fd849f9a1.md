
`print("im alive!");`

}

```

```csharp
// Example.cs

void Start()

.

print("");

Monster

 =box.AddComponent("Monster") as Monster)
```

```csharp
//GameObject = GameObject.CreatePrimitive((PrimitiveType:

box.AddComponent("Monster");

Monster m = box.GetComponent("Monster") 
```

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_325_0.png)

```csharp
//go.transform.position = new
```

```csharp
//go.transform.position = new
```

# 中级

我们还在通过其他一些方法来让移动行为更有趣，但在进入那一步之前，我们需要先学习一些技巧。

或者，我们可以通过以下符号同时赋值并获取 `Monster m` 变量：

```csharp
Monster m = box.AddComponent("Monster") as Monster;
```

这会自动将 `m` 赋值，因为它同时也被赋值给 `box` 组件。组件赋值和变量赋值是在一步内完成的。

## 6.5.4 我们学到了什么

这一章的内容相当很大。新的数组类型被用来存储许多游戏对象，它也可以很容易地用来存储一组数字，或者实际上是任何东西。我们学习了 `foreach` 循环，它在处理数组时非常有用。

在本章中，我们还进行了一些数学计算，并在 `Time` 类中发现了一个好用的计时器函数。之后，我们弄明白了如何通过代码挂载脚本组件，然后我们通过 `GetComponent()` 和类型转换来访问该组件，以确保它不是通用组件。

我们还有几个数据类型需要学习。既然我们正在处理这么多类型，我们将学习更多关于类型转换的内容。

## 6.6 枚举 (Enums)

如果我们有两个类，`Example.cs` 和 `Monster.cs`，那么 `Example.cs` 负责创建和分配对象，实际上是生成了一个 `Monster`。我们可以把之前写的 `Example.cs` 的旧版本改为 `Player.cs`，这将总共给我们三个对象。

```csharp
using UnityEngine;
using System.Collections;

public class Player : MonoBehaviour
{
    public float Speed = 0.1f;

    //Update 每帧调用一次
    void Update ()
    {
        gameObject.transform.position += Movement (Speed);

        Vector3 Movement (float dist)
        {
            Vector3 vec = Vector3.zero;
            if (Input.GetKey(KeyCode.A))
            {
                vec.x -= dist;
            }
            if (Input.GetKey(KeyCode.D))
            {
                vec.x += dist;
            }
            if (Input.GetKey(KeyCode.W))
            {
                vec.z += dist;
            }
            if (Input.GetKey(KeyCode.S))
            {
                vec.z -= dist;
            }
        }
    }
}
{
  vec.z -= dist;
}
```

因此，这就是我在本章中使用的 `Player.cs`；我们将用它来移动场景中的小盒子。我们将假装这个小盒子是一个看起来很酷的怪物猎人，配备了剑、散弹枪或双管散弹枪。

我们可能想将 `Example.cs` 重命名为 `MonsterSpawner.cs` 或 `MonsterGenerator.cs`，但我交由你决定。只需记住重命名类声明以与匹配。这将产生怪物来追逐玩家。挂载在 `MonsterSpawner` 创建的每个对象上的 `Monster.cs` 将会寻找玩家并追逐他。这就是计划。

注意：使用原元形状进行游戏原型设计是游戏开发的常规组成部分。这与所谓的“程序员艺术”（programmer art）有些关系。代码的更改往往意味着艺术的变化。要保持艺术和代码并行开发是很的。通常，代码中的一个微小变化意味着艺术上数天的修改。在不要求艺术家的情况下制作游戏原型要容易得多。大多数时候，程序员甚至不知道如何像艺术家一样行动。

### 6.6.1 使用枚举

关键字 "enum" 是 "enumeration"枚举）的缩写。程序员可能会说枚举是一个命名常量列表。这个意义可能看起来很晦涩。翻译过来，为了让我们的怪物拥有更好的行为函数集，我们将创建一个名为 `MonsterState` 的新类型。我们之前已经与 `PrimitiveType` 枚举交互过了。

```csharp
public enum PrimitiveType
{
  Sphere,
  Capsule,
  Cylinder,
  Cube,
  Plane
}
```

我们还看到枚举可以存储许多不同的名称。例如，`InputType` 枚举包含了你的鼠标、轨迹板或控制器的每个按键和输入的枚举。列出长串的“物品”列表有助于用比简单数字索引更有用的名称来命名每种可能性。记住，枚举不需要遵循任何特定模式。由你决定任何组织方式来保持枚举的整洁。在 `MoreLogic` 项目中，打开 Project 面板 Assets 列表中找到 `Example.cs`。

```csharp
public PrimitiveType primitiveType;
GameObject obj;

// 使用此进行初始化
void Start () {
  obj = GameObject.CreatePrimitive(primitiveType);
}
```

在 `Example.cs` 类的开头，我们有一个公共的 `Primitive` 类型 `primitiveType`。注意大小写的区别；第二个单词是小写，现在没有使用之前定义的 `PrimitiveType` 版本。

在编辑器中，你会看到一个包含不同 `PrimitiveTypes` 的新菜单。在 `Start()` 函数中，我们使用 `GameObject` 的 `CreatePrimitive` 成员函数来创建所选类型的新对象。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_328_0.png)

我们可以扩展此方法以更好地感受枚举的工作。

这项工作虽然可行，但它显得相当杂乱。如果我们向 `MonsterState` 中添加更多枚举（enums），将需要更多的 `if` 语句。然而，处理枚举有更简单的方法，所以是时候学习一个新花样了。

## 6.6.3 我们学到了什么

所以，枚举的创建是为了创建一个选项列表。通常情况下，枚举被限制在单个选项上，但情况并不总是如此。枚举能够包含多个选项，这一点在整个章节中都已讨论过。

使用枚举意味着根据选择采取行动。枚举实际上是基于数字的。你可以将枚举强制转换为 `int` 并获取一个可用的值。当进行此转换时，枚举中的第一个名称为 0，其他任何名称都是根据其在枚举列表中的位置的递增值。因此，根据以下代码，记录的值为 3，因为第一个状态是 0，而第四个状态是 3。

```csharp
public enum MonsterState
{
    standing,
    wandering,
    chasing,
    attacking
}

public MonsterState mState;

void Start ()
{
    mState = MonsterState.attacking;
    int number = (int)mState;
    Debug.Log(number);
}
```

还有其他操作枚举的方法，但为了理解它如何工作以及为什么有效，在进入那部分之前，我们需要涵盖其他几个主题。

## 6.7 switch

当我们同时处理多一个条件时，`switch` 语句就会经常派上用场。例如，我们可能会遇到一种面对长长的 `if-else` 语句链的情况。

```csharp
public int i;

void Start ()
{
    if(i == 0)
    {
        Debug.Log("i is zero");
    }
    else if(i == 1)
    {
        Debug.Log("i is one");
    }
    else if(i == 2)
    {
        Debug.Log("i is two");
    }
    else if(i == 3)
```

### 中间级

# 311

```csharp
{
  Debug.Log("i is three");
  else if(i == 4)
{
    Debug.Log("i is four");
  }
  else
{
    Debug.Log("i is greater than 4");
  }
}
```

这段代码块应该让你感到有些别扭。事实上，有一个名为 `switch` 语句的系统，它是为了缓解这种长 `if-else` 语句链的别扭感。`switch` 以关键字 `switch` 开始，后面跟着一个参数 `()`，该参数控制由一对大括号封装的代码块。

```csharp
void Update ()
{
  switch (someVariable)
  {
  }
}
```

`switch` 语句的内容使用关键字 `case`。每个 `case` 都由一个匹配 `switch` 参数中参数的预期选项来完成。

### 6.7.1 基础示例

`switch` 可以用于任意数量的类型。简单的 `switch` 语句可以像下面使用 `int` 的代码，类似于 `if-else` 链。可以在附加到 Main Camera 上的 `SwitchStatement` 项目中找到。

```csharp
using UnityEngine;
using System.Collections;

public class Example : MonoBehaviour {
  public int i = 1;

  void Start () {
    switch (i)
    {
      case 0:
        Debug.Log("i is zero");
        break;
      case 1:
        Debug.Log("i is one");
        break;
      case 2:
        Debug.Log("i is two");
        break;
    }
  }
}
```

这是一个带有 `case` 的基础 `switch`。`case` 后面跟着 1 或 2，并以冒号结尾。在另一个 `case` 出现之前，有两个语句，最后一个语句是 `break;`，它结束了 `case` 语句。

# 使用 Unity 3D 学习 C# 编程

第一个 `case 1:` 被执行是因为 `i = 1;`；或者用通俗的话说`i` 满足了执行 `case` 之后代码的条件。语句后面的 `break;` 让计算机跳出 `switch` 语句并停止 `switch` 语句内部的任何进一步执行。

```csharp
int i = 1;
switch (i)
{
    case 1: print("got one"); break;
    case 2: print("got two"); break;
}
```

当你处理短 `case` 时，移除多余的空间并使用更多的代码要容易得多。每个 `case` 被称为一个标签（label）；我们可以在 `switch` 语句之外使用标签，但我们将在 6.7.5 节中了解更多信息。

`switch` 语句是管理一组情况的好得多方法。第一次看 `switch` 语句时，可能会有一点困惑。这里发生了几件事。`switch` 的一般情况基本上是获取一个变量，可以是任何类型。代码选择 `case` 语句开始执行。主要条件是所有的 `case` 都使用 `switch()` 函数中使用的类型。例如，如果 `switch` 使用了 "mState" 枚举，你可以使用一个检查 "ent" 的 `case`。

在查看编写该代码的代码块时，`switch` 的优势可能显而易见。`switch` 有用的重要原因是可以穿过许多不同的语句，每个参数的内容都需要进行计算。

当你处理短 `case` 时，移除多余的空间并使用更多的代码要容易得多。每个 `case` 被称为一个标签；我们可以在 `switch` 语句之外使用标签，但我们将在 6.7.5 节中了解更多信息。

`switch` 语句是管理一组情况的好得多方法。第一次看 `switch` 语句时，可能会有一点困惑。这里发生了几件事。`switch` 的一般情况基本上是获取一个变量，可以是任何类型。代码选择 `case` 语句开始执行。主要条件是所有的 `case` 都使用 `switch()` 函数中使用的类型。例如，如果 `switch` 使用了 "mState" 枚举，你可以使用一个检查 "ent" 的 `case`。

`switch` 语句是管理一组情况的好得多方法。第一次看 `switch` 语句时，可能会有一点困惑。这里发生了几件事。`switch` 的一般情况基本上是获取一个变量，可以是任何类型。代码选择 `case` 语句开始执行。主要条件是所有的 `case` 都使用 `switch()` 函数中使用的类型。例如，如果 `switch` 使用了 "mState" 枚举，你可以使用一个检查 "ent" 的 `case`。

6.7.2 Default:

如果 `switch` 中有一个没有被包含的 `case` 怎么办？处理任何数字。这就是 `default:` 发挥用场的地方。

```csharp
int i = 3;
switch (i)
{
    case 0:
        Debug.Log("i is zero");
        break;
    case 1:
        Debug.Log("i is one");
        break;
    case 2:
        Debug.Log("i is two");
        break;
    default:
        Debug.Log("other number");
        break;
}
```

加上 `default` 后，任何未处理的情况都可以被处理。如果没有添加 `default`，任何未处理的将被将被忽略。`default` 是一个可选条件。

当然，`switch` 语句与枚举配合似乎非常合适。枚举外观的一个略有不同的变化是我们需要使用点运算符将输入值与枚举之一进行比较。

```csharp
public enum MyCases
{
    first,
    second,
    third,
    fourth,
    fifth,
    sixth,
    seventh
}

public MyCases cases;

void Update ()
{
    switch (cases)
    {
        case MyCases.first:
            Debug.Log("first case");
            break;
        case MyCases.second:
            Debug.Log("second case");
            break;
        case MyCases.third:
            Debug.Log("third case");
            break;
        case MyCases.fourth:
            Debug.Log("fourth case");
            break;
        case MyCases.fifth:
            Debug.Log("fifth case");
            break;
        case MyCases.sixth:
            Debug.Log("sixth case");
            break;
        case MyCases.seventh:
            Debug.Log("seventh case");
            break;
    }
}
```

我们有一个复杂的 `case` 数组，每个 `case` 都根据 `MyCases` 的枚举值顺序排列。在 Unity3D 编辑器内部，当分配给 GameObject 时，C# 类会在 Inspector 面板中提供一个下拉列表。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_335_0.png)

# 中级
