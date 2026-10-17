
`Debug.Log(go.name);`

`static void NewTrick()` 是我们的扩展函数。为了扩展 `GameObject`，我们使用参数 `this GameObject go`，其中 `this` 通知 C# 我们正在编写扩展方法。在参数列表中，我们使用函数中的 `go` 作为 `go.name`。这个 `NewTrick()` 将 `GameObject` 的名称打印到控制台。

```csharp
public class Extensions : MonoBehaviour {

void Start () {

    GameObject.New

    // /gameObj M NewTrick

SimpleO

UpdateE

}

public delegate event;

// Update i

void Update() {

    if (Upda) {

        UpdateEvent();

    }

}

```

| `public static void NewTrick ( Vector3 pos )` |
| :--- |
| 来自 `Tricks.GameObjectExtensions` 的扩展方法 |

回到 `Start()` 函数，可以使用 `NewTrick()` 将相机或场景中任何具有 transform 的对象移动到场景中心。然而，这确实突出了 `Zero()` 可能应该出现在一个名为 `TransformExtensions` 的不同类中，还是不呢？函数可以重载，所以我们可以在该类中拥有多个 `Zero()` 扩展函数。

```csharp
public static class GameObjectExtensions

{
```

# 高级

```cs
public static void NewTrick (this GameObject go, Vector3 pos)

{

    go.transform.position = pos;

    Debug.Log(go.name);

}

public static void Zero (this Transform t)

{

    t.position = Vector3.zero;

}

public static void Zero (this GameObject go)

{

    go.transform.position = Vector3.zero;

}
```

我们有一个可以同时用于 `GameObject` 和 `Transform` 类型的 `Zero()` 函数。也许我们应该将 `GameObjectExtension` 重命名为类似于 `GameExtensions` 的名称。类和函数的命名是编写代码的重要部分。返回代码中重命名类或函数被称为重构。

在项目开始增长时，尽早了解一些需要避免的实践是有好处的。特别是对于 Unity 3D，当场景中的每个对象由较小的组件组合时，效果最好。这种特性通常被称为 Actor 模型（actor model）。

`MonoBehaviour` 的 `Start()` 和 `Update()` 循环有许多优点。然而它们伴随着微小的代价。一旦场景中填充了数百个对象，你的场景就没有需要单独启动 `Start()` 函数并更新其 `Update()` 的了。这可能会导致幻灯片现象和帧率损失。这种问题在高端 PC 上可能并不明显，但在性能较弱的小型移动设备上可能会产生毁灭性的影响。

## 7.16.3 继承自 Object

最后的手段，或者可能是轻量级 Unity 3D 游戏项目的第一步，是忘记所有的 `MonoBehaviour`。`Update()` 函数倾向于消耗你游戏大部分帧率。如果有一个非常繁忙的 `Update()` 函数，比有几百个简单的 `Update()` 函数调用要好得多。

在 PC 上，你永远无法避免幻灯片现象。只有当你使用移动设备时，你才会注意到帧率的明显下降。与桌面电脑相比，手机的处理器和内存限制很大。限制你的代码使用的资源和计算量非常重要，以确保在更有限的系统上运行时获得最佳性能。

为了保持函数简单且易于处理，确保单个 `Update()` 简短且快速至关重要。同时，确保基于对象而非 `MonoBehaviour` 的类在需要时仍然可以进行更新也是重要的。

## 7.16.4 OnUpdate

继续上一个练习，我们将通过事件添加一个系统来更新 `SimpleObject` 类。一旦我们在基于 `MonoBehaviour` 的类的 `Update()` 中添加了 `OnUpdate()` 函数，就能为这个轻量级类提供一个 `Update()`。

```cs
using UnityEngine;

using System.Collections;

using Tricks;

public class SimpleObject : Object

{

    GameObject gameObject;

}
```

```cs
public SimpleObject(GameObject go)

{

    this.gameObject = go;

    Debug.Log("im here: " + go.name);

}

public void OnUpdate ()

{

    gameObject.Zero();

}
```

首先，我们在 `SimpleObject` 中等待拥有 `Update()` 函数。这使用 `GameObject` 的方式与 `MonoBehaviour` 拥有 `GameObject` 的相同。我们正在使用新添加的 `.zero()` 扩展函数。
在 `Extensions` 类中，我们为简单对象添加以下代码：

```cs
public class Extensions : MonoBehaviour

{

    // 使用此进行初始化

    void Start ()

    {

        SimpleObject so = new SimpleObject(this.gameObject);

        UpdateEvent+= so.OnUpdate;

    }

    public delegate void UpdateHandler();

    public event UpdateHandler UpdateEvent;

    ///Update 每帧被调用一次

    void Update ()

    {

        if(UpdateEvent != null)

        {

            UpdateEvent();

        }

    }

}
```

我们创建了一个 `UpdateHandler()` 和一个 `UpdateEvent`，并为其分配了 `so.OnUpdate`。一旦分配完成，它每帧都会被 `Update()` 函数调用。游戏一运行，相机就会对齐到世界中心 `Vector3(0,0,0)` 并固定在在那里。

## 7.16. 我们学到了什么

在脚本开始处理大量不同的变量后，垃圾回收（GC）开始成为一个影响游戏性能的问题。帧率的间歇性卡顿有时是内存中大量对象被清理的结果。
在 Unity 3D 的 C# 类中出现的其他有趣技巧是显示使用了多少内存。当你添加如 `using System;` 的指令时，你包含了大量需要访问的内存。在运行游戏时并不一定使用这些内存；但在你的代码编译时会使用。
为了方便使用，像下面这样简单的用例是有重要的：

```cs
using Vect3 = UnityEngine.Vector3;
```

这把 `Vector3` 简化为了 `Vect3`。这有助于减少命名空间冲突，并有助于在 MonoDevelop 的自动补全功能中选择名称。在情况下，弹出列表中 `Vector2` 始终在 `Vector3` 之上。过一段时间，如果你习惯了使用 `Vect3`，这种行为可以很容易替换。

# 高级

# 551

通常的做法是使用原始名称，以防需要库的其余部分。然而，了解这种技巧是可能的是有好的，以防你遇到奇怪的东西。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

## 析构函数 (destructors)

通常的做法是使用原始名称，以防需要库的其余部分。然而，了解这种技巧是可能的是有好的，以防你遇到奇怪的东西。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

## 7.17. 析构函数 (Destructors)

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

### 7.17.1 析构函数 (Basic Destructor)

Unity 3D 的开发者是坚定的。在 Unity 3D 中工作，对于 .NET 基础提供的完整功能集，对于哪些代码有效以及哪些不工作有着特定的限制。

```cs
using UnityEngine;

using System.Collections;

public class DestroyMe

{

    public string name;

    //构造函数

    public DestroyMe(string name)

    {

        this.name = name;

        Debug.Log(name + " says hello.");

    }

    ~DestroyMe()

    {

        Debug.Log(name + " says goodbye.");

    }

}
```

## 使用 Unity 3D 学习 C#

```cs
using UnityEngine;

using System.Collections;

public class Example : MonoBehaviour

{

    DestroyMe dm;

    // 使用此进行初始化

    void Start ()

    {

        dm = new DestroyMe("rob");

    }

    //Update 每帧被调用一次

    void Update ()

    {}

}
```

在挂载到相机上的 `Example.cs` 中，我们有一个将持有 `DestroyMe` 的变量。当我们创建一个新的 `DestroyMe` 并将其存储为 `dm` 时，我们给它一个名字，以便知道什么被清理了。

然而，我们可以通过简单的赋值来强制执行操作。

```cs
void Start ()

{

    dm = new DestroyMe("rob");

    dm = null;

}
```

当我们创建一个新的 `DestroyMe` 对象时，我们在控制台中看到 "rob says goodbye."。将变量 `dm` 设置为 `null` 会释放该类对 `DestroyMe` 对象的引用。一旦 C# 看到没有东西引用 `DestroyMe` 对象，它就会从内存中被清理。

通常情况下，C# 中的 GC 是自动运行的。对于结构体（struct）等对象，GC 应该执行得很快。只有当你需要处理大量的类对象时，我们才需要密切关注创建的对象数量。自动 GC 在随机间隔内进行。通常在 PC 上，GC 几乎没有影响。内存和 CPU 运行速度非常快，除非发生 GC 否则是察觉的。
GC 周期之间的间隔可能会根据创建对象的频率而变长或变短。这可能会导致每几秒出现一次帧率下降。建立某种方案来跟踪并销毁对象是非常重要的。

## 17.1.2 清理对象 (Clearing Out Objects)

在对象拥有一个引用后，它变得更容易处理。在 `DestroyMe` 类中，我们将添加一个新的 `OnUpdate ()`：

```cs
using UnityEngine;

using System.Collections;

public class DestroyMe

{

    public string name;

    //构造函数

    public DestroyMe(string name)

    {

        this.name = name;

        Debug.Log(name + " says hello.");

    }

    public void OnUpdate ()

```



# 高级

```csharp
{

  Debug.Log(name + " is updating.");

}

void DestroyMe() {

  Debug.Log(name + " says goodbye.");

}
```

然后，为了使用该函数，我们将创建一个委托和一个事件，在 `Example` 的 `Update()` 函数中进行更新。

```csharp
using UnityEngine;

using System.Collections;

public class Example : MonoBehaviour

{

  DestroyMe dm;

  int counter = 10;

  delegate void updateHandler();

  event updateHandler updateEvent;

  // 使用此进行初始化

  void Start ()

  {

    dm = new DestroyMe("rob");

    updateEvent += dm.OnUpdate;

  }

  // Update 每帧调用一次

  void Update ()

  {

    if (updateEvent != null)

    {

      updateEvent();

      counter--;

      if (counter <= 0)

      {

        dm = null;

      }

    }

  }

}
```

在这个类的版本中，我们想要通过事件将 `DestroyMe` 对象更新 10 次，然后将其移除。如果我们观察计数器减到 0 时发生了什么，我们像以前一样将 `dm` 设置为 `null`。然而，我们并没有收到析构函数被调用的消息，而且即使在 `dm` 被设置为 `null` 之后，`OnUpdate()` 函数每帧都会被调用。

```csharp
void Update ()

{

  if (updateEvent != null)

  {

    updateEvent();

    counter--;

    if (counter <= 0)

    {

      dm = null;

      updateEvent = null;

    }

  }

}
```
