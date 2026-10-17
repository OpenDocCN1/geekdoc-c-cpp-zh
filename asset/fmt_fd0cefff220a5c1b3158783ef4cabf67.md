
## 6.21.3 类型别名 (Type Aliasing)

我们可以在`float`中使用上面的代码，但`float`是C#开始的命名约定。因此，我们将遵循约定，使用`float`而不是`System.Single`，尽管C#接受这两种者。`float`这个词来自C#早期的某人决定添加一个类型别名。我们可以通过`using`语句添加自己的类型别名。

```csharp
using UnityEngine;
using System.Collections;
using MyOwnIntType = System.Int16;
```

结合我们将在类顶部看到的指令，我们还可以添加另一个指令。通过添加`using MyOwnIntType`，我们可以将其赋值为`System.Int16`；这会将我们的标识符变为`System.Int16`。

```csharp
MyOwnIntType c = 1;
Debug.Log(c.GetType());
```

使用上面的片段会产生以下Console输出：

```
System.Int16
UnityEngine.Debug.Log(Object)
TypeCasting:Start () (at Assets/TypeCasting.cs:15)
```

这里`float`在Unity 3D的某个深处被赋值为了`System`。我们不太可能发现`float`的转换是`Single`，但知道该关键字是如何赋值的。事实是，`float`关键字虽然在编程中是多余的，但它只是给`System.Single`出的别名。同样，`int`或`double`以及我们常用的其他关键字也是为了简化代码的别名。其他系统已经对系统类型使用了别名，如`bigint`、`smallint`和`tinyint`，映射到存储整数值的不同字节。

现在我们知道了位类型是如何产生的，以及如何将一种类型转换为另一种类型，是时候用用这些知识了。

## 6.21.4 装箱与拆箱 (Boxing and Unboxing)

装箱是程序员当使用泛型容器来分配许多类型时使用的术语。当发现什么被“放入箱中”后，我们就可以决定下一步做什么。当数据从变量中取出时，一旦你知道它是什么以及要如何处理它，你就对其进行“拆箱”。

例如，我们可以获取场景中的所有对象并将它们放入数组`GameObject[] allObjects`中。这包括主摄像机和场景中的任何光照，以及怪物、玩家和环境对象。如果你查看列表寻找任何附有`Zombie()`的东西，你就可以获取带有`Zombie`组件的最近的`GameObject`并执行任何涉及该特定对象的的操作。从数组中拆箱一个`Zombie`允许你与其交互。

## 6.22 运算符重载 (Operator Overloading)

如果你想在将一个僵尸加到另一个僵尸时执行某些特定操作会发生什么？运算符，似乎C#中的任何东西都可以添加额外功能。在处理新类时，我们需要使用我们认为合适的方法管理数据。在大多数情况下，运算符重载应该被认为有点像巫术。

```csharp
class Zombie
{
    void Start ()
    {
        Zombie a = new Zombie();
        Zombie b = new Zombie();
        Zombie c = a + b;
    }
}
```

# 6.22.1 基础示例

```csharp
class Zombie
{
    public int damage = 10;
    public static Zombie operator + (Zombie a, Zombie b)
    {
        Zombie z = new Zombie();
        int powerUp = a.damage + b.damage;
        z.damage = powerUp;
        return z;
    }
    void Start ()
    {
        Zombie a = new Zombie();
        Zombie b = new Zombie();
        Debug.Log(a.damage);
        Debug.Log(b.damage);
        Zombie c = a + b;
        Debug.Log(c.damage);
    }
}
```

使用Unity 3D学习C#编程

如果我们的游戏中有一个作为标准物品的补给箱，我们可能希望有一个简单的方法将一个补给箱添加到另一个补给箱中。在我们的代码中，当我们添加一个包含少量数学计算的构造函数来根据补给箱中的物品自动计算重量时，这会变得非常有趣。在这里，我们将绷带和弹药的重量增加了补给箱的重量。在设置`Supplies`构造函数之后，我们将为`+`运算符添加一个行为。

```csharp
public static Supplies operator + (Supplies a, Supplies b)
{
    Supplies s = new Supplies(0);
    int sBandages = a.bandages + b.bandages;
    int sAmmun = a.ammunition + b.ammunition;
    float sWeight = a.weight + b.weight;
    s.bandages = sBandages;
    s.ammunition = sAmmun;
    s.weight = sWeight;
    return s;
}
```

这只是简单地将`a`和`b`的内容组合并相加，然后设置一个新的`Supplies`对象为组合后的值。最后，我们返回这个新对象。

```csharp
void Start ()
{
    Supplies supplyA = new Supplies(3);
    Supplies supplyB = new Supplies(9);
    Supplies combinedAB = supplyA + supplyB;
    Debug.Log(combinedAB.weight);
}
```

如果我们创建了两个`Supplies`对象的副本并将它们相加，我们将得到一个符合你预期的结果。你可能对任何其他数学运算符都有预期。以下代码产生了预期的结果：

```csharp
Supplies supplyA = new Supplies(3);
Supplies supplyB = new Supplies(9);
Supplies combinedAB = supplyA + supplyB;
Debug.Log(combinedAB.weight);
Supplies abc = supplyA + supplyB + combinedAB;
```

在都使用了运算符重载的情况下，`supplyA + supplyB`的最终重量为38.4单位。该重载应该是静态的（static），因为这是一个在类级作用范围内作用于`Supplies`对象的函数。我们需要更深入结构，以获得添加`绷带 C = bandageA + bandageB;`的能力，我们需要为该创建一个类和一个运算符重载。

## 6.2.2 重载 *

我们被限制为通过类来重载类。在上面的示例中，我们正在向补给中添加补给。我们可以用数字重载我们的`Supplies`运算符`*`。

```csharp
public static Supplies operator * (Supplies a, int b)
{
    Supplies s = new Supplies(0);
    int sBandages = a.bandages * b;
    int sAmmun = a.ammunition * b;
    float sWeight = a.weight * b;
    s.bandages = sBandages;
    s.ammunition = sAmmun;
    s.weight = sWeight;
    return s;
}
```

在上面的示例中，我们获取补给并将其乘以`int b`。为了使用新运算符，代码看起来应该像所示：

```csharp
Supplies sm = new Supplies(5);
Debug.Log(sm.weight);
sm = sm * 3;
Debug.Log(sm.weight);
```

在这种情况下，我们的`sm = sm * 3;`获取原始值并乘以3，然后接受新值作为自身。该日志将向控制面板发送8，然后是24。这意味着我们可以使用以下修改在控制面板中打印32：`sm = sm + sm * 3;`

除了之前使用`+`和`*`的示例外，我们还可以重载`true`和`false`关键字。对于像`>`和`<`的运算符，我们可以测试一个僵尸是否比另一个更危险。

## 6.2.3 重载 <

返回布尔值的运算符也可以被重载。`<`和`>`运算符可以被重载以返回`true`或`false`值。实现此点的代码片段如下：

```csharp
public static bool operator < (Zombie a, Zombie b)
{
    if (a.damage < b.damage)
        return true;
    } else {
        return false;
    }
}
```

在我们在使用之前，3D Unity会通过以下错误信息提醒我们忘记了某些东西：

`Assets/OperatorOverloading.cs (46,36): error CS0216: The operator 'OperatorOverloading.Zombie.operator < (OperatorOverloading.Zombie, OperatorOverloading.Zombie)' requires a matching operator '>' to also be defined`

为了符合要求，我们将添加小于`<`运算符重载的反向版本。通过使用它，我们在`Start ()`函数中使用以下语句比较两个僵尸：

```csharp
public static bool operator >(Zombie a, Zombie b)
{
    if (a.damage > b.damage)
    {
        return true;
    } else {
        return false;
    }
}
```

只需快速复制/粘贴并将`<`替换为大于`>`，就可以让我们使用小于和大于的重载。在我们的`Start ()`函数中，我们可以使用以下语句来检查我们的重载是否工作。

```csharp
Zombie a = new Zombie();
Zombie b = new Zombie();
a.damage = 9;
if (a.damage < b.damage) {
    Debug.Log("less damage");
}
```

除了前面的示例使用`+`和`*`外，我们还可以重载`true`和`false`关键字。对于像`>`和`<`的运算符，我们可以测试一个僵尸是否比另一个更危险。

```csharp
public static bool operator == (Zombie a, Zombie b)
{
    return a.damage == b.damage;
}
public static bool operator != (Zombie a, Zombie b)
{
    return a.damage != b.damage;
}
```

在我们的代码中，我们可以使用以下语句来检查我们的重载是否工作：

```csharp
Zombie a = new Zombie();
Zombie b = new Zombie();
a.damage = 9;
if (a.damage == b.damage) {
    Debug.Log("equal damage");
}
if (a.damage != b.damage) {
    Debug.Log("not equal damage");
}
```

## 6.2.4 总结

在这一节中我们学习了运算符重载。

- 运算符重载允许为类自定义运算符。
- 运算符重载是静态的。
- 运算符重载可以返回布尔值（比较重载）。
- 运算符重载可以用于简化代码（例如添加补给箱）。

一旦到位，你可以尝试创建另一个类来继承它。以下类尝试继承自该密封类（sealed class）：

```csharp
using UnityEngine;
using System.Collections;
public class InheritFromSealed : FinalizedObject
{
    //使用此方法进行初始化
    void Start ()
{}
    // Update 每帧被调用一次
    void Update ()
{}
}
```

当然，这会在会在Unity的控制台（Console）面板中产生以下错误：

`Assets/InheritFromSealed.cs(4,14): error CS0509: 'InheritFromSealed': cannot derive from sealed type 'FinalizedObject'`

从类中移除`sealed`关键字并允许更多类继承自它是轻而易举的，但这会提示你正在进行一项并非意图的更改。这种行为旨在限制对某个类进行特定操作的篡改程度。通常情况下，使用`sealed`编写的类用于非常基础且广泛使用的函数；它们不应该要求任何其他类继承自。

关键点在于，一个广泛使用的类应该是稳定且保持不变的。可靠性是防止过多Bug渗透代码的关键。`sealed`等所有不同的访问修饰符都旨在防止意外行为。当然，这并不意味着它可以完全防止所有Bug。

## 6.2.3 抽象（Abstract）

关于类如何继承父类，`abstract`关键字另一个巧妙的关键字。`abstract`关键字用于告诉继承类有一个它们需要实现的函数。如果你需要实现一个标记为`abstract`的函数，Unity 3D将提醒你并抛出错误。

### 6.2.3.1 基础示例

为了告诉另一个程序员或你自己实现一个特定的函数，使用了`abstract`关键字。设置一个继承关系的类有助于你规划类以及这些类预期的使用方式。

```csharp
using UnityEngine;
using System.Collections;
public class Abstraction : MonoBehaviour
{
    abstract class BaseClass
    {
        public int Counter;
        public abstract void ImportantFunction();
    }
    class ChildClass : BaseClass
    {
        public override void ImportantFunction()
```

### 中级

```csharp
{
  Counter++;
  Debug.Log(Counter);
}
void Start() { 
  ChildClass c = new ChildClass();
  c.ImportantFunction();
  c.ImportantFunction();
  c.ImportantFunction();
  c.ImportantFunction();
}
```

该示例在基于`MonoBehaviour`的`Abstraction.cs`类中了两个嵌套类。第一个类被称为`BaseClass`。它提供了两个内容：一个用于计数的`int`和一个抽象函数。`int`名为`counter`，函数被命名为`ImportantFunction()`。包含抽象函数的类也必须声明为`abstract`。

```csharp
abstract class BaseClass
{
  public int counter;
  public abstract void ImportantFunction();
}
```

`abstract`关键字标识出该函数是一个存根（stub）。它告诉程序员，从`BaseClass`继承中有一个重要的函数，他或她需要实现它。具体的实现由子类的作者来决定。

例如，如果我们正在制作怪物，我们会有一个怪物基类和某种`attackHuman()`（攻击人类），这是所有怪物都需要执行的动作。吸血鬼、恶魔和狼人都都需要执行某些`attackHuman(Human)`。该函数在每个怪物之间有何不同。它如何在怪物上实现，以及由谁来编写该函数。

当函数前面带有`abstract`关键字时，该函数不能有函数体。它看起来可能如下：

```csharp
abstract class BaseClass
{
  public int Counter;
  public abstract void ImportantFunction()
  {
    //不允许有代码
  }
}
```
