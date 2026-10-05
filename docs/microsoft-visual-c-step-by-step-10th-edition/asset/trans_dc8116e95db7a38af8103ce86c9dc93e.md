

所有的结构实际上继承自一个名为 `System.ValueType` 的抽象类。（第 13 节探讨了抽象类。）这只是 Microsoft .NET 库定义基于栈的值类型的通用行为的一种实现细节；你不太可能在自己的应用程序中直接使用 `ValueType`。

## 重新回顾 System.Object 类

`System.Object` 类是所有类的根类。所有类都隐式派自 `System.Object`。因此，C# 编译器会将 `Mammal` 类静重写为如下代码（如果你真的想，也可以显式地编写）：

点击查看代码图像

```
class Mammal : System.Object
{
  ...
}
```

`System.Object` 类中的任何方法都会通过继承链传递给派生 `Mammal` 的类，例如 `Horse` 和 `Whale`。在实践中，这意味着你定义的所有类都继承了 `System.Object` 类的所有特性。这包括如 `ToString` 方法（在第 2 节“使用变量、运算符和表达式”中讨论过），该方法用于将对象转换为字符串以便显示。

## 调用基类构造函数

除了继承的方法外，派生类还自动包含基类的所有字段。这些字段通常在创建对象时需要初始化。你通常在构造函数中执行此类初始化。记住，所有类都至少有一个构造函数。（如果你不提供，编译器会为你生成一个默认构造函数。）

在派生类的构造函数中，作为初始化的一部分调用其基类的构造函数是一个良好的习惯，这使得基类构造函数能够执行它所需的任何额外初始化。在定义继承类的构造函数时，你可以指定 `base` 关键字来调用基类构造函数，如下例所示：

点击查看代码图像

```
class Mammal // 基类
{
    public Mammal(string name) // 基类的构造函数
    {
        ...
    }
    ...
}
class Horse : Mammal // 派生类
{
    public Horse(string name)
        : base(name) // 调用 Mammal(name)
    {
        ...
    }
    ...
}
```

如果你没有在派生类构造函数中显式调用基类构造函数，编译器会尝试在执行派生类构造函数代码之前，静默插入对基类默认构造函数的调用。回到之前的示例，编译器将将其重写为：

点击查看代码图像

```
class Horse : Mammal
{
    public Horse(string name)
    {
        ...
    }
    }
```

如下：

点击查看代码图像

```
class Horse : Mammal
{
    public Horse(string name)
        : base()
    {
        ...
    }
}
```

如果 `Mammal` 有一个公共的默认构造函数，这种方法就能有效。然而，并非所有类都有公共的默认构造函数。例如，记住，只有在你没有编写任何非默认构造函数时，编译器才会生成默认构造函数。在这种情况下，忘记调用正确的基类构造函数会导致编译错误。

## 类的赋值

书中的之前的示例展示了如何使用类来声明变量，以及如何使用 `new` 关键字创建对象。示例还展示了 C# 的类型检查规则如何防止你将一种类型的对象赋值给声明为不同类型的变量。例如，根据此处显示的 `Mammal`、`Horse` 和 `Whale` 类的定义，跟在这些定义后的代码是非法的：

点击查看代码图像

```
class Mammal
{
    ...
}

class Horse : Mammal
{
    ...
}

class Whale : Mammal
{
    ...
}

Horse myHorse = new Horse(...);
Whale myWhale = myHorse; //  - 类型不同
```

然而，只要使用的类型是继承层次结构中更高层的类，就可以通过不同类型的变量引用该对象。因此，以下语句是合法的：

点击查看代码图像

```
Horse myHorse = new Horse(...);
Mammal myMammal = myHorse; // 合法，Mammal 是 Horse 的基类
```

如果你从逻辑上考虑这个问题，那么所有的马都是哺乳动物，因此你可以安全地将一个 `Horse` 类型的对象赋值给 `Mammal` 类型的变量。继承层次结构意味着你可以将 `Horse` 对象简单地看作一种特殊的 `Mammal` 对象；它拥有 `Mammal` 对象拥有的所有内容，加上你为 `Horse` 类添加的任何方法和字段所定义的额外部分。你也可以让 `Mammal` 变量引用一个 `Whale` 对象。

然而，有一个显著的限制：当使用 `Mammal` 变量引用 `Horse` 或 `Whale` 对象时，你只能访问由 `Mammal` 类定义的方法和字段。`Horse` 或 `Whale` 类定义的任何额外方法通过 `Mammal` 类都是不可见的。

点击查看代码图像

```
Horse myHorse = new Horse(...);
Mammal myMammal = myHorse;
myMammal.Breath(); // OK - Breathe 是 Mammal 类的一部分
myMammal.Trot(); // 错误 - Trot 不是 Mammal 的部分
```

> 前面的讨论解释了为什么你可以将几乎任何内容赋值给对象变量。记住 `object` 是 `System.Object` 的别名，所有类都直接或间接地继承自 `System.Object`。

请注意，相反的情况并不成立。你不能无保留地将一个 `Mammal` 对象赋值给 `Horse` 变量：

点击查看代码图像

```
Mammal myMammal = new Mammal(...);
Horse myHorse = myMammal; // 错误
```

这看起来像是一个奇怪的限制，但记住并不是所有的 `Mammal` 对象都是 `Horse`。你可以使用 `as` 运算符或通过强制转换将 `Mammal` 对象赋值给 `Horse`。（第 7 节“创建和管理类”讨论了 `is` 和 `as` 运算符。）

下面的代码示例使用 `as` 运算符检查 `Mammal` 是否为 `Horse`，如果是，则对 `Horse` 的赋值成功：

点击查看代码图像

```
Mammal myMammal = new Horse(...);
Horse myHorse = myMammal as Horse; // OK - Horse

Mammal myMammal = new Whale(...);
Horse myHorse = myMammal as Horse; // 返回 null - Whale
```

## 声明新方法

计算机编程领域最困难的任务之一是为标识符思考独特有意义的名称。如果你正在为一个类定义方法，且该类是继承层次结构的一部分，早晚你会尝试重用一个已经被某个类占用的名称。如果基类和派生类恰好声明了两个签名相同的方法，当你编译应用程序时将收到一个警告。

> 注意
> 方法签名指的是方法的名称及其参数的类型数量，但不包括其返回类型。两个名称相同且带有相同参数列表的方法具有相同的签名，即使它们返回不同的类型。

派生类中的方法会掩盖（或隐藏）基类中具有相同签名的方法。例如，如果你编译以下代码，编译器会生成一条警告信息，通知你 `Horse.Talk` 隐藏了继承的方法 `Mammal.Talk`：

点击查看代码图像

```
class Mammal
{
  ...
  public void Talk() // 假设所有哺乳动物都会说话
  {
    ...
  }
}
```

```
class Horse : Mammal
{
  public void Talk() // 马说话的方式与其他哺乳动物不同！
  {
    ...
  }
}
```

尽管你的代码可以编译并运行，但你应该认真对待这个警告。如果另一个类派自 `Horse` 并调用 `Talk` 方法，它可能期望调用 `Mammal` 类中实现的方法。然而，`Horse` 中的 `Talk` 方法隐藏了 `Mammal` 类中的 `Talk` 方法，取而调用的是 `Horse.Talk` 方法。

大多数情况下，这种巧合最好是混乱的根源，你应该考虑重命名方法以避免冲突。然而，如果你确定想要让这两个方法具有相同的签名以隐藏 `Mammal.Talk` 方法，你可以通过 `new` 关键字来消除警告，如下：

