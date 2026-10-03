
# 8.11.5 多重属性

每个自定义属性都应该是相当特定的。特殊指令或你标记字段或函数的方式应该是具有特定的用途。如果你需要为类成员添加多个属性，你可以对其进行堆叠。

```cs
[AttributeUsage(AttributeTargets.All, AllowMultiple = true, Inherited = true)]
```

添加 `AllowMultiple = true` 告诉属性你可以在类成员上堆叠不同的属性。此外，我们可以为此属性添加 `Inherited = true`，这样任何继承该成员的类也将拥有相同的属性。

# 使用 Unity 3D 学习 C# 编程

```csharp
+ " attrib is a "
+ ma.Name);
}
if (attrib is MyOtherAttribute)
{
    MyOtherAttribute ma = attrib as
    MyOtherAttribute;
    Debug.Log("found "
    + info.ToString())
    + " attrib is a "
    + ma.OtherName);
}
```

为了让事情简单简单，我们可以检查属性的类型并在发现它们时对其进行类型转换。一旦完成类型转换，我们就可以提取预期的信息并使用它。在这个示例中，我们只是查看简单的案例来查找属性。一旦找到了属性，我们就既拥有属性中的信息，也拥有与之相关的类成员。

## 11.6.6 让属性投入工作

为了让属性变得有用，我们可以将其与某些类建立关联，这些类并不一定是基于具有活动 `Update()` 函数的 `MonoBehaviour`。`MonoBehaviour` 基类使得它们变得非常易于控制。通过一个不基于 `MonoBehaviour` 的简单类，我们可以得到如下代码：

```csharp
using UnityEngine;
using System.Collections;
public class BaseClass
{
    public string name;
    public BaseClass(string n)
    {
        this.name = n;
    }
    public void OnUpdate()
    {
        Debug.Log(name + " is updating...");
    }
}
```

这为我们提供了一个快速、轻量的起始类。在 `OnUpdate()` 函数上，我们将添加一个名为 "Update" 的属性。在这种情况下，我们将属性命名为 Update，我们将使用之前过的反射系统来查找它。在新的基类内部，我们在 `OnUpdate()` 函数上方添加了该属性。

```csharp
[MyAttribute("Update")]
public void OnUpdate()
{
    Debug.Log(name + " is updating...");
}
```

这段短片段显示了添加到函数中的 `MyAttribute`。现在是在场景中创建该类的几个实例的问题。这提供了一个简单的测试：如果场景中有许多不同的对象，它们可以在不同的函数上共享同一个属性。我们稍后将其添加到我们的示例中。

## 扩展

```csharp
void Start() {
    baseClasses = new BaseClass[10];
    for (int i = 0; i < 10; i++) {
        BaseClass bc = new BaseClass(i.ToString());
        baseClasses[i] = bc;
    }
}
```

这将创建若干 `BaseClass` 对象并将它们添加到数组中。这些对象也可以通过 `ArrayList` 并使用 `GameObject.FindObjectsOfType(typeof(object))` 来获取场景中的所有内容。之后，我们将能够筛选所有对象（包括 C# 类）并查找 `MyAttribute`。

接下来在 `SpecialAttributes.cs` 类中，我们也将实现一个 `Update()` 函数以及一个在 `Update()` 循环中更新的事件。

```csharp
public delegate void UpdateEventHandler();
public event UpdateEventHandler UpdateEvent;
void Update() {
    if (UpdateEvent != null) {
        UpdateEvent();
    }
}
```

这将创建一个处理器和一个事件，该事件会在每帧调用 `MonoBehaviour` 的 `Update()` 函数时触发。`BaseClass` 无法独立做到，因为它不是 `MonoBehaviour` 的子类。因此，我们将使用 `UpdateEvent` 来调用任何分配了 `MyAttribute("Update")` 的函数。

现在棘手的部分开始了。我们需要查看类中的所有函数，获取这些函数的属性，然后将函数添加到 `UpdateEvent` 中。首先，我们从每个对象开始。

```csharp
foreach(object o in baseClasses) {
    Type t = o.GetType();
    MethodInfo[] methods = t.GetMethods();
}
```

上面的代码做了两件事：它查看我们的对象数组，通过 `Type t = o.GetType()` 获取对象的类型，因此我们通过 `GetMethods()` 反射函数从 `t` 中获取方法。这变成了一个 `MethodInfo[]` 数组。一旦我们有了这个数组，就可以对每一个排序并查找属性。

```csharp
foreach(object o in baseClasses) {
    Type t = o.GetType();
    MethodInfo[] methods = t.GetMethods();
    foreach(MethodInfo method in methods) {
        object[] attributes = method.GetCustomAttributes(true);
    }
}
```

继续下去，我们将查看分配给 `object[] attributes` 变量的对象自定义属性。因此，在 `foreach method` 中，我们将遍历从 `t.GetMethods()` 获取的 `MethodInfo[]` 数组。对于每个方法，我们需要查找它的属性。因此，我们使用 `object[] attributes` 并将 `method.GetCustomAttributes(true)` 分配给 `object[]` 数组。提醒一下，`true` 用于告诉函数我们想要包含 `BaseClass` 可能继承的父类。

现在我们为每个方法都有了一个属性数组，我们需要查看每个属性。

```csharp
foreach(object o in baseClasses)
{
    Type t = o.GetType();
    MethodInfo[] methods = t.GetMethods();
    foreach(MethodInfo method in methods)
    {
        object[] attributes = method.GetCustomAttributes(true);
        foreach(object attribute in attributes)
        {
            if (attribute is MyAttribute)
        }
    }
}
```

一旦我们有了属性，就应该检查它是否是我们预期的 `MyAttribute` 属性。如果是，我们就可以检查它是否是预期的 `MyAttribute` 属性。如果是，我们可以将方法分配到事件。这里是最终的算法：

```csharp
foreach(object o in baseClasses)
{
    Type t = o.GetType();
    MethodInfo[] methods = t.GetMethods();
    foreach(MethodInfo method in methods)
    {
        object[] attributes = method.GetCustomAttributes(true);
        foreach(object attribute in attributes)
    }
}
```

## 扩展

## 641

```csharp
{
  if (attribute is MyAttribute)
  {
    MyAttribute ma = attribute as MyAttribute;
    if (ma.Name == "Update")
    {
      EventInfo ei;
      typeof(SpecialAttributes).GetEvent("UpdateEvent");
      Type et = ei.EventHandlerType;
      Delegate d = Delegate.CreateDelegate(et, method);
      ei.AddEventHandler(this, d);
    }
  }
}
```

这需要几个步骤。首先我们从 `typeof(SpecialAttributes).GetEvent("UpdateEvent")` 获取 `EventInfo`。然后我们需要从它获取类型。这通过 `Type = ei.EventHandlerType` 完成，其中 `EventHandler` 是我们分配的 `EventHandler`。

每个正确类型的对象通过 `Delegate.CreateDelegate()` 创建一个新的委托。`CreateDelegate()` 函数接受三个参数：第一个是它正在创建一个委托，所以这种情况下是 `Type`；第二个是 `object`；最后是需要知道分配给事件的函数，即 `MethodInfo method`。

然后我们通过 `SpecialAttributes` 类 `ei` 将 `Delegate` `AddEventHandler()`。我们使用关键字将类作为 `object`。分配给对象的回调是 `Delegate d`。

现在运行时，对象被创建。在创建对象后，它们扫描带有属性的函数。如果属性名称是 "Update"，那么该函数将被分配到 `UpdateEvent`，该事件是在 `MonoBehaviour` 的 `Update()` 函数中被调用的。

# 8.11 属性标记

属性可以应用于类、函数和变量。我们还应该考虑对属性进行跟踪，限制属性的使用位置，以防止属性应用到我们不希望拥有特定属性的对象上。

在声明新的属性类时，我们得到几个可以使用的选项。

```csharp
[AttributeUsage(AttributeTargets.Method)]
public class MyOtherAttribute : Attribute
```

上述代码使得 `MyOtherAttribute` 仅适用于你的类函数。我们也可以使用按位运算符 `|` 添加额外的 `AttributeTargets` 以添加多个标记。此类标记在第 8.9 节中介绍过。

```csharp
[AttributeUsage(AttributeTargets.Method | AttributeTargets.Field)]
public class MyOtherAttribute : Attribute
{}
```

这会将选项改为同时包含函数和变量。正如我们在第 8.9.3 节中刚刚看到的按位运算符 `|`，我们知道 `AttributeTargets` 枚举是为了按位检查而设计的。

# 8.11 我们学到了什么

本章末尾的特殊会将每个类成员打印到 Console（控制台）面板。函数的输出描述了每个成员及其自定义属性。通过自定义属性，我们可以将其用于许多不同的任务。一个带有时间延迟的 `[UpdateAttribute(3.0f)]` 属性可以用来指示一个函数是否被添加到更新事件中，以及它应该如何被更新。

每个怪物都可以拥有具有不同时间值的 `UpdateAttribute`。速度更快、更聪明的怪物更新频率可以比更新之间有延迟的较慢怪物更高。如果你复活一个角色，可能需要将各种状态恢复为默认值。如果每个角色都有不同的统计数据，簿记工作可能会变得更加繁重。`[RestoreAttribute(restoredAmount)]` 会让簿记工作自动化。只需列出所有需要恢复的字段并恢复到指定的数量即可。使用自定义属性提供了一个易读的系统，可以将信息附加到函数或变量上。

# 8.12 架构与组织

因此，在本书书中我们专注于编写单个类或让类相互继承。学习语言的机制是可以的，但它对构建大型项目没有帮助。停顿并后退一步将帮助你所有的类相互匹配以构建整个项目。这需要完全不同的心态。

当你为游戏构建结构时，将 C# 文件按任务分离是非常重要的。当任务被分成不同的文件时，可以在更远的地方进行添加或合并。保持越多的分离，在工程师团队工作时需要合并的文件就越少。如果每个类的范围限制在几个相关任务上，也会减少需要查看修复 Bug 的数量。使用调试器时；如果文件不长且范围有限，你只需要在一个较小的文件中找到并修复问题即可。

当你独自工作时，很容易声称对代码库拥有所有权。当一切都尽在掌握，且你对它的运作有更好的了解时。涉及到团队工作时，每个人都需要专注于代码库中更专门化的部分。当你能够专注于特定任务时，你能够更好地链接你的范围并构建一个经过深思熟虑的类。
