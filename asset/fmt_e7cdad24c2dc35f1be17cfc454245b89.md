
### 访问与可见性

全局变量以及所有方法都可以额外的访问修饰符进行扩展。这些修饰符决定了它们仅在类内部可见（因此也可以被使用），还是也可以被另一个类或实例访问。

- `public` 允许从任何地方访问。公共变量也会在 Unity 的 Inspector（检查器）面板中显示。
- `private` 将访问限制在你自己的类中。
- `protected` 将访问限制在你自己的类以及所有继承自它的类中。
- `internal` 将访问限制在你程序集（assembly）中的所有类中（对于 DLL 非常重要）。

如果你不指定这些关键字之一，C# 中的变量和方法将被自动视为 `private`。顺便说一下，类只能被授予 `public` 和 `internal`。如果缺少关键字，则被视为 `internal`。

```csharp
public class test {
    private int health;
    public bool isEqual(string stringA, string stringB) {
        //Code...
    }
}
```

### 静态类与类成员

在某些情况下，你需要独立于已创建实例运行的编程方法或变量，例如该类之前创建的所有实例的计数器。在这种情况下，当然，并不是每个实例都拥有自己的计数机制，其结果甚至可能不同。此类应用使用了所谓的静态方法/变量……或者称为通用类成员。（相比之下，传统的方法/变量被称为实例成员。）它们使用 `static` 关键字声明，并且不能通过实例访问，而是通过类名直接访问。Unity 在此处使用了它，例如在 `Mathf` 数类中。

```csharp
int myInteger = Mathf.RoundToInt(1.5f);
```

静态方法的声明如下所示：

```csharp
public static void SetLevelSettings(int levelIndex) {
    //Code...
}
```

`Math` 类更进了一步。这里整个类被声明为 `static`，因此编译器只允许类成员。“成员”是类中可以包含的所有“东西”的总术语，例如：方法、变量等。静态类则定义如下：

```csharp
public static class GameSettings {
    public static string playerName = "";
    public static void SetLevelSettings(int levelIndex) {
        //Code...
    }
}
```

### 参数修饰符 out / ref

通常，如上所述，传递给函数的变量是经过复制的。这意味着函数内部对值类型变量（或具有值类型语义的变量）的值更改不会影响从外部传递的变量。然而，在某些情况下，使用参数修饰符 `ref` 和 `out` 可能是理想的，它们通过引用将变量（无论是值类型还是引用类型）传递给方法，而不是通过复制内容。方法中的每个传参都必须与修饰符以及传递给方法的变量相标识。

```csharp
public bool isEqual(ref string myName, string colliderName) {
    bool result = false;
    if (stringA.ToLower() == stringB.ToLower()) {
        result = true; stringA = stringB;
    }
    return result;
}
```

使用 `ref` 修饰符调用方法：

```csharp
string myName = "Player";
string colliderName = "player";
equal = isEqual(ref myName, colliderName);
```

在上述情况下，`myName` 初始值为 "Player"，`colliderName` 值为 "player"。在调用方法后，两个变量的值都变成了 "player"。`out` 的用法与 `ref` 相同。这两个参数之间的区别如下：

- `ref` 请求一个已经初始化的变量。因此，被传递的变量在传递到方法之前必须已经有一个值。
- `out` 不需要初始化的变量。然而，必须在方法内部确保分配一个有效值。

一个巨大的优势是，你现在有了从一个方法返回多个值的选项。例如，Unity 的 `Physics` 类使用了 `out`。

```csharp
RaycastHit hit;
if (Physics.Raycast(transform, direction, out hit))
    float distance = hit.distance;
```

### 使用 params 数组

除了上述修饰符外，还有 `params` 修饰符。它简化了数组的传递，使得你不一定需要定义数组。你可以传递逗号分隔的变量列表。

```csharp
public int DamageAddition(params int[] damageValues) {
    int val = 0;
    foreach (int current in damageValues) {
        val += current;
    }
    return val;
}
```

```csharp
int sum;
int damage1 = 5;
int damage2 = 3;
sum = DamageAddition(damage1, damage2);
```

```csharp
int[] damageArray = new int[2];
damageArray[0] = 5;
damageArray[1] = 3;
sum = DamageAddition(damageArray);
```

### 属性与属性方法

假设你有一个 NPC 类，它有一个公共变量 `health`。你可以给该类的对象分配任何值，即使不允许对象具有负健康值。与其在处理该值的地方考虑这一点，不如从一开始就确保这种情况不会发生。为了实现这一点，在 C# 中有所谓的属性方法，它们可以在值传输时检查并更改该值。属性方法（简称为属性）由两个子方法组成：`get` 和 `set` 访问器。

- `get` 用于查询值。
- `set` 用于赋值。

实际变量（在我们案例中是 `health`）声明为 `private`，因此仅可以通过属性方法访问。这种过程也称为数据封装。使用这些访问器，NPC 类看起来如下：

```csharp
public class NPC {
    private int health;
    public int Health {
        get {
            return health;
        }
        set {
            health = value;
            if (health < 0)
                health = 0;
        }
    }
}
```

注意大小写：属性方法首字母大写且是 `public`。变量是小写且是 `private`。

```csharp
NPC npc = new NPC();
int h = 3;
npc.Health = 3; // 将私有变量 health 设置为 3
npc.Health -= 5; // 从当前值减去 5，所以 health 实际上为 -2
h = npc.Health; // Health 返回 0
```

## 继承

面向对象编程的一个重要特性是继承的可能性。这意味着程序员可以开发一个新类，它可以使用另一个类的所有方法、变量等作为基础，而无需重写代码。这个新类被称为派生类。它所继承的类被称为基类。如果一个类现在要继承另一个类，在类名后写一个冒号，然后是基类的名称。

```csharp
public class MyScriptName : MonoBehaviour {
    //Code
}
```

即使你可能自己并不经常使用继承，但这对作为 Unity 程序员的你来说非常重要的问题。Unity 中创建的类如果要作为组件使用，必须继承自 Unity 类 `MonoBehaviour`。这包含了类作为组件所需的所有内容。你可以在第 4 章“脚本编程”中找到更多信息。

### 基类与派生类

在 C# 中，如果一个类要继承另一个类，必须在类名后写一个冒号，然后是基类的名称。假设我们有一个类 `person`，它有一个公共变量 `name` 和私有变量 `points`。

```csharp
public class person {
    public string name = "";
    private int points = 0;
}
```

派生类 `NPC` 应该有一个额外的变量 `health`，那么它看起来如下：

```csharp
public class NPC : person {
    public int health;
}
```

现在你可以创建一个 `NPC` 类的对象，并使用这两个公共变量：

```csharp
NPC npc = new NPC();
npc.name = "Legolas";
```

```csharp
npc.health = 10;
```

### 继承与可见性

即使在上面的示例中 `NPC` 类继承了基类 `Person`，我之前解释的可见性规则仍然适用。你不能在派生类中访问基类的私有变量或私有方法。如果你仍然想允许访问，可以使用 `protected` 关键字代替 `private` 来定义这些成员。

```csharp
public class person {
    public string name = "";
    protected int points = 0;
}
```

这意味着变量 `points` 从外部来看仍然不可见，但在派生类 `NPC` 中可以访问。

```csharp
public class NPC : person {
    public int health;
    public void DoSomething() {
        points = 100;
    }
}
```

### 重写继承的方法

假设你有一个基础类 `person`，它除了各种变量和方法外，还有一个名为 `Shoot` 的方法。为了显示此功能，首先应该在控制台中输出一段短文本。你可以使用 `Debug.Log` 命令来实现。虽然 `Person` 类提供了标准文本 "Peng!"，但 `NPC` 类现在应该说一些不同的内容。为了实现这一点，C# 提供了覆盖方法的可能。要做到这一点，被重写的方法必须先在基类中被声明为可重写的。这是通过 `virtual` 关键字实现的。

```csharp
public class person {
    public virtual void Shoot() {
        Debug.Log("Peng!");
    }
}
```

派生类可以（但不必）重写此方法。这里的关键字是 `override`。

```csharp
public class NPC : person {
    public override void Shoot() {
        Debug.Log("Tie!");
    }
}
```

### 访问基类

如果你现在在派生类中重写了基类的方法，但现在想访问基类的方法，自然就产生了一个现在如何做的问题。这是通过 `base` 关键字实现的。你通过 `base` 访问基类的方法、变量等。

```csharp
public class NPC : person {
    public override void Shoot() {
        base.Shoot();
        Debug.Log("Tie!");
    }
}
```

### 密封类

另一种继承的方法是通过密封。这意味着防止类的继承能力。换句话说，如果你在类定义前面加上 `sealed` 关键字，没有其他类可以继承自它。

```csharp
public sealed class NPC : person { // code ... }
```

## 多态

面向对象的编程语言提供了另一种实用的技能，称为多态。你可以以相同的方式处理所有具有共同基类的对象/实例。以下方法触发了传递对象的 `Shoot` 函数。脚本并不关心该对象实际上是 `Person` 类型还是派生自 `Person` 的类（例如上一个示例中的 NPC）。

```csharp
void LetsShoot(Person person) {
    person.Shoot();
}
```

向 `LetsShoot` 传递各种对象：

```csharp
Person person = new Person();
NPC npc = new NPC();
LetsShoot(person);
LetsShoot(npc);
```

### 接口

C# 面向对象的另一个特性是接口。通过接口你可以定义不同类的共同特征，并借此再次对它们进行。这样你可以平等地对待不同的类，这在某些情况下非常有用。微软已经预定义了一些通用接口，这些对于某些功能也很重要，你也可以定义自己的接口。

#### 定义接口

要定义接口，使用 `interface` 关键字。按照惯例，接口名称始终以 `I` 开头，因此在上面的示例中它将是 `IShootable`。接口的其余部分类似于类，区别在于方法没有编写实现。

```csharp
public interface IShootable {
    void Shoot();
}
```

类和接口之间的重要区别涉及访问修饰符。在类中，所有没有访问修饰符的内容都是私有的，而接口被认为是内部的。毕竟，接口也用于描述类的外部影响。除了 `public` 之外，其他访问修饰符在接口中都是禁止的。

#### 实现接口

如果一个类要实现接口，其方法与继承类相同，即使用冒号。如果既继承一个类又实现一个（或多个）接口，这些将用逗号列在基类名称之后。`IShootable` 接口的实现如下：

```csharp
using UnityEngine;
using System;

public class Gun : MonoBehaviour, IShootable {
    private WeaponController weaponController;
    void Awake() {
        weaponController = gameObject.GetComponent<WeaponController>();
    }
    public void UseMe() {
        weaponController.Switch(this);
    }
    public void Shoot() {
        Debug.Log("Peng!");
    }
}
```

脚本的各个区域目前并不重要，将在其他章节中详细讨论。尽管如此，我想预测这里实际上发生了什么。当 `Awake` 方法被调用时，将搜索并为 `WeaponController` 脚本组件（其代码稍后处理）赋值。如果现在调用 `UseMe` 方法，`Gun` 自身的脚本实例将传递给 `WeaponController` 的 `Switch` 方法。最后，`Shoot` 方法仅向 Unity 控制台写入 "Peng" 用于演示。

#### MonoDevelop 支持

编程环境 MonoDevelop 帮助你实现接口。如果你在上面的示例中 `MonoBehaviour` 后面写了实现 `IShootable`，将指针移动到 `IShootable` 并点击右键。在出现的右菜单中，转到 Refactor / Implement implicit。然后所有的属性、方法等都会被自动添加到你的类中。你现在只需为它注入生命。当然，你现在可以删除默认插入的异常（错误消息）。

### 通过接口访问

要访问接口，你可以像使用变量类型一样使用接口。在接下来的脚本中，接口被用于 `Switch` 方法的参数定义，也用于公共变量的定义。这意味着只要一个类实现了 `IShootable` 接口并因此具有 `Shoot` 函数，任何类都可以传递给 `Switch`。

```csharp
using UnityEngine;
using System.Collections;

public class WeaponController : MonoBehaviour {
    public IShootable weapon;
    public void Switch(IShootable newWeapon) {
        weapon = newWeapon;
    }
    public void ShootCurrentWeapon() {
        weapon.Shoot();
    }
}
```

## 命名空间

如果我们在本书末尾开发这个演示游戏，你会发现在一个 Unity 项目中创建了许多类。此外，Unity 在后台编程时使用的框架也提供了许多类。为了不让你丢失视图并避免产生混乱，引入了所谓的命名空间。命名空间是一种组织结构，它将相关的类型（类等）结构化，并将它们分组为逻辑单元。你可以将其比为文件系统上的文件夹，其中包含各种文件。如果你现在想在 Unity 中使用某种类型，必须引用项目中的命名空间并集成到类中。通常情况下，Unity 会处理这一切。只有当你想要使用特殊类型时，才需要手动完成。

你可以在脚本文件的开头使用关键字 `using` 包含一个命名空间。接接的示例类包含了 `System.Collections.Generic` 命名空间，以便使用 `List` 类型。

```csharp
using System.Collections.Generic;
```
