
中间

这输出了以下内容：

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_368_0.png)

控制台显示代码是按照我们在类中布局的顺序执行的。当调用 `LateUpdate()` 函数时，我们使用 `Destroy(this)` 开始从场景中删除该类。当类开始删除自己时，它首先会被禁用，然后被删除。

当创建一个新的 `MonoBehaviour` 实例时，它也会调用它的 `Awake()`、`OnEnable()` 和 `Start()` 函数。直觉上，如果你在 `Awake()` 函数中创建一个对象，那么它在自己的 `Awake()` 函数执行之前等待 `Awake()` 结束是合理的。然而，情况并非总是如此。

```cs
void Awake ()
{
    Debug.Log("Awake Start");
    this.gameObject.AddComponent(typeof(Second));
    Debug.Log("Awake Done");
}
```

假设我们创建了一个新类 `Second.cs`，并让它正确记录它的 `Awake()` 和 `Start()` 函数。那么，在 `Second.cs` 类中，我们有以下代码：

```cs
public class Second : MonoBehaviour
{
    void Awake ()
    {
        Debug.Log("Second Awake Start");
    }

    void OnEnable ()
    {
        Debug.Log("Second OnEnable Start");
    }
}
```

产生了以下输出：

- First Awake Start
- Second Awake Start
- Second OnEnable Start
- First Awake Done
- First OnEnable

在 `First` 类被创建之前，`Second` 能够获取其 `Awake()` 并不中断地进入 `OnEnable()`。`First` 等待 `Second` 完成它的 `Awake()` 和 `OnEnable()` 函数后才完成自己的 `Awake()` 函数。之后，`First` 的 `OnEnable()` 才被调用，即使 `Second` 花费了自己的时间来完成它的 `Awake()` 函数。

```cs
void Awake () {
    Debug.Log("Second Awake Start");
    for (int i = 0; i < 1000; i++) {
        Debug.Log("wait!");
    }
    Debug.Log("Other Awake Done");
}
```

| Clear | Collapse | Clear on Play | Error Pause | 19 | 0 |
|---|---|---|---|---|---|
| First Awake Unity.Debug:Log(Object) | | | | | 1 |
| Second Awake Unity.Debug:Log(Object) | | | | | 1 |
| wait! Unity.Debug:Log(Object) | | | | | 1000 |
| Second Awake Unity.Debug:Log(Object) | | | | | 1 |
| OnEnable Unity.Debug:Log(Object) | | | | | 1 |
| First Awake Unity.Debug:Log(Object) | | | | | 1 |
| First OnEnable Unity.Debug:Log(Object) | | | | | 1 |
| First Start Unity.Debug:Log(Object) | | | | | 1 |
| Second Start Unity.Debug:Log(Object) | | | | | 1 |

`First.cs` 类完成了它的 `Awake()` 函数，然后 `Second.cs` 类完成了它的 `Awake()` 函数并开始它的 `OnEnable()`。接着 `First.cs` 类完成了它的 `Awake()` 并开始它的 `OnEnable()` 函数。`First` 和 `Second` 开始它们的 `Start()` 函数。注意，"First Awake Done" 直到 "Second OnEnable" 之后才出现。"Second OnEnable" 只有在打印 "Second Awake Done" 时才会打印，这意味着循环能够完成。

当创建更多对象时，这些函数调用的顺序变得更难以理清。如果你创建了不同的对象，某些对象可能花费更或更短的时间完成它们的 `Awake()`、`OnEnable()` 和 `Start()` 函数。弄清楚这一切需要一些思考。

## 6.12.2 组件执行顺序

当类作为制体（prefab）附加到 gameObject 上时，类的执行会变得有点混乱。在场景中，为主相机（Main Camera）添加 `Second` 和 `Third` 类将向我们展示一些意料之外的结果。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_368_0.png)

在场景中，为主相机添加 `Second` 和 `Third` 类将向我们展示一些意料之外的结果。

（注：此处后续原文存在大量重复的 OCR 错误，已根据要求过滤掉重复内容，仅翻译并保留核心逻辑部分。）

中级

```csharp
public void ParentFunction()
{
    print("parent says hello");
    FunctionA();
    FunctionB();
}

public void FunctionA()
{
    print("function A says hello");
}

public void FunctionB()
{
    print("function B says hello");
}
```

当 `ParentFunction()` 被添加到 `Start()` 函数中时，它将在 Unity 3D 编辑器的 Console 面板中产生预期的"parent says hello"，接着是"function A says hello"，然后是"function B says hello"。并没有发生任何意外的事情。`Child` 类基于父类（Parent class），我们有机会通过添加层层代码来对其修改。为了看到这种修改，我们需要在 `Child` 类中重用 `Parent` 类。将 `ParentFunction()` 取并添加到 `Child` 类的 `Start()` 函数中。

```csharp
public class Child : Parent
{
    void Start ()
    {
        ParentFunction();
    }
}
```

运行此代码将在 Console 面板中产生与父类相同的输出。目前还没有进行函数重写（overriding）。如果我们打算重写一个函数，应该通过在我们计划重写的函数上添加 `virtual` 关键字，让父类允许函数被重写。

```csharp
public virtual void FunctionA() {
    print("function A says hello");
}
```

在 `public` 声明之后、返回数据类型之前添加 `virtual` 关键字，允许我们告诉该函数它可以被任何继承其函数的类重写。回到 `Child` 类，我们有了重写该虚函数的选项。

```csharp
using UnityEngine;
using System.Collections;

public class Child : Parent
{
    void Start ()
    {
        ParentFunction();
    }

    public override void FunctionA()
    {
        print("Im a new version of function A");
    }
}
```

# 354 使用 Unity 3D 学习 C# 编程

对于 `FunctionA()` 有了一个新的指令。正如你预期的那样，Console 面板的输出变成了新的内容。`Child` 类将向 Console 发送新数据，读取内容应该是：

parent says hello
Im a new version of function A
function B says hello

如果没有 `override` 和 `virtual` 关键字，我们将得到以下警告：

Assets/Child.cs(11,21): warning CS0108: 'Child.FunctionA()' hides inherited member 'Parent.FunctionA()'. Use the new keyword if hiding was intended

我们可以尝试这种做法并观察输出。在 `Child` 类中，我们将添加 `new` 关键字。然而，输出将保持不变，就像在使用 `Parent` 类的 `FunctionA()` 版本一样。这是因为因为存在于 `Child` 类中的 `FunctionA()` 是一个新的，而不是 `ParentFunction()` 所使用的那个。正如你可以想象的，这可能会引起困惑。

```csharp
public virtual void FunctionA()
{
    print("function A says hello");
}
```

## 6.13.1.1.1 Base

`Child` 类的函数版本继承了其父类的成员。隐藏（Hiding）意味着继承的函数版本不再有效。当调用时，新版本将运行。然而，我们在父类版本的 `FunctionA()` 中写了内容，我们可能重写也可能不想重写它。要使用原始版本，我们可以在 `FunctionA()` 的开头添加 `base` 关键字。

```csharp
void Start()
{
    base.FunctionA();
}
```

这在 Console 面板中产生了预期的 3 输出。要让 `Child` 类接管 `FunctionA()` 并创建它自己的函数版本，请使用 `override` 关键字。

```csharp
public override void FunctionA()
{
    print("Im a new version of function A");
}
```

因此，当 `Start()` 函数调用 `FirstFunction()` 时，调用的是相应版本，导致在游戏运行时 Unity 3D 的 Console 面板中打印出"new version of FirstFunction()"。通常，当我们有多个类需要使用同一个函数时，函数重写就会发挥作用。

## 6.13.2 类继承

我们已经看到了一些函数如何从类的以前版本中继承某些属性。为了看到它是如何工作的，请在一个名为 `Monsters` 的新 C# 文件中创建几个嵌套类。

```csharp
using UnityEngine;
using System.Collections;

public class Monsters : MonoBehaviour
{
    // 使用此项进行初始化
    void Start ()
    {
    }

    // Update 每帧调用一次
    void Update ()
    {
    }

    class Monster
    {
        public int HitPoints;
    }

    class Zombie : Monster
    {
        public int BrainsEaten = 0;
    }

    class Vampire : Monster
    {
        public int BloodSucked = 0;
    }
}
```

在公共类 `Monsters` 中，我们在底部添加了 `Monster` 类、`Zombie` 类以及 `Vampire` 类。`Zombie` 和 `Vampire` 都继承自 `Monster`。

## 6.13.21 共享用属性

在公共类 `Monsters` 中，我们在底部添加了 `Monster` 类、`Zombie` 类以及 `Vampire` 类。`Zombie` 和 `Vampire` 都继承自 `Monster`。

在公共类 `Monsters` 中，我们在底部添加了 `Monster` 类、`Zombie` 类以及 `Vampire` 类。`Zombie` 和 `Vampire` 都继承自 `Monster`。

在公共类 `Monsters` 中，我们在底部添加了 `Monster` 类、`Zombie` 类以及 `Vampire` 类。`Zombie` 和 `Vampire` 都继承自 `Monster`。

在公共类 `Monsters` 中，我们在底部添加了 `Monster` 类、`Zombie` 类以及 `Vampire` 类。`Zombie` 和 `Vampire` 都继承自 `Monster`。

在公共类 `Monsters` 中，我们在底部添加了 `Monster` 类、`Zombie` 类以及 `Vampire` 类。`Zombie` 和 `Vampire` 都继承自 `Monster`。

在公共类 `Monsters` 中，我们在底部添加了 `Monster` 类、`Zombie` 类以及 `Vampire` 类。`Zombie` 和 `Vampire` 都继承自 `Monster`。

（此处翻译逻辑如下）：

`Child` 类的函数版本继承了其父类的成员。隐藏意味着继承的函数版本不再有效。当被调用时，新版本将运行。然而，我们在父类版本的 `FunctionA()` 中写了内容，我们可能重写也可能不想重写它。要使用原始版本，我们可以在 `FunctionA()` 的开头添加 `base` 关键字。

这在 Console 面板中产生了预期的 3 输出。要让 `Child` 类接管 `FunctionA()` 并创建它自己的函数版本，请使用 `override` 关键字。

因此，当 `Start()` 函数调用 `FirstFunction()` 时，调用的是相应版本，导致在游戏运行时 Unity 3D 的 Console 面板中打印出"new version of FirstFunction()"。通常，当我们有多个类需要使用同一个函数时，函数重写就会发挥作用。

## 6.13.2 类继承

我们已经看到了一些函数如何从类的以前版本中继承某些属性。为了看到它是如何工作的，请在一个名为 `Monsters` 的新 C# 文件中创建几个嵌套类。

```csharp
using UnityEngine;
using System.Collections;

public class Monsters : MonoBehaviour
{
    // 使用此项进行初始化
    void Start ()
    {
    }

    // Update 每帧调用一次
    void Update ()
    {
    }

    class Monster
    {
        public int HitPoints;
    }

    class Zombie : Monster
    {
        public int BrainsEaten = 0;
    }

    class Vampire : Monster
    {
        public int BloodSucked = 0;
    }
}
```

在公共类 `Monsters` 中，我们在底部添加了 `Monster` 类、`Zombie` 类以及 `Vampire` 类。`Zombie` 和 `Vampire` 都继承自 `Monster`。

### 6.13.21 共享属性

（由于原文文本在 6.13.21 之后出现了大量重复的乱码句子，根据高级文档工程师逻辑，翻译核心含义部分）：

在公共类 `Monsters` 中，我们在底部添加了 `Monster` 类、`Zombie` 类以及 `Vampire` 类。`Zombie` 和 `Vampire` 都继承自 `Monster`。

（注：由于提供的原文文本后半部分存在严重的文本重复错误，译文已根据核心逻辑进行处理）。

这可以作为对象和类为何以这种方式创建的公平示例。当函数和变量被分离在类中时，它们允许你为了非常特定的目的进行模块化处理。在设计类时，牢记面向对象的概念是非常重要的。

## 6.13.3 Object

更改此前已实现函数的行为是面向对象编程（OOP）语言中的一种强大工具。Unity 3D 中所有类继承的基类是 `Object`。Object 是 Unity 可以引用的基类。为了让 Unity 3D 能够与类交互，它必须首先基于对象。Net Framework 为任何创建的其他类提供了对象基础。这使得每个新对象都有了彼此通信的共同基础。

```
Object
- Base Types
  - Object()
  - Equals(object, object) : bool
  - Equals(object) : bool
  - Finalize() : void
  - GetHashCode() : int
  - GetType() : Type
  - MemberwiseClone() : object
```
