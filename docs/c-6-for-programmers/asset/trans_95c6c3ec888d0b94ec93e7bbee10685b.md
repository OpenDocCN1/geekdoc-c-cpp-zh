

使用派生类引用调用派生类对象的 BasePlusCommissionEmployee 的 ToString 和 Earnings 方法：

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: $5,000.00
commission rate: 0.04
base salary: $300.00
earnings: $500.00

使用基类引用调用派生类对象的 BasePlusCommissionEmployee 的 ToString 和 Earnings 方法：

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: $5,000.00
commission rate: 0.04
base salary: $300.00
earnings: $500.00

图 12.1 | 将基类和派生类引用分配给基类和派生类变量。（第 3 部分，共 3 部分。）

在图 12.1 中，第 11–12 行创建一个新的 CommissionEmployee 对象并将其引用分配给一个 CommissionEmployee 变量，第 15–16 行创建一个新的 BasePlusCommissionEmployee 对象并将其引用分配给一个 BasePlusCommissionEmployee 变量。这些赋值是自然的——CommissionEmployee 变量的主要目的是保存对 CommissionEmployee 对象的引用。第 23–24 行使用引用 commissionEmployee 调用方法 ToString 和 Earnings。由于 commissionEmployee 引用的是一个 CommissionEmployee 对象，因此会调用基类 CommissionEmployee 的方法版本。类似地，第 31–33 行使用引用 basePlusCommissionEmployee 在 BasePlusCommissionEmployee 对象上调用方法 ToString 和 Earnings。这会调用派生类 BasePlusCommissionEmployee 的方法版本。

第 37 行随后将对派生类对象 basePlusCommissionEmployee 的引用分配给基类 CommissionEmployee 变量，第 41–43 行使用该变量调用方法 ToString 和 Earnings。请注意，第 41 行中的调用 commissionEmployee2.ToString() 实际上调用的是派生类 BasePlusCommissionEmployee 的 ToString 方法。编译器允许这种“交叉”，因为派生类的对象是其基类的对象（反之则不成立）。当编译器遇到通过变量进行的虚方法调用时，编译器会检查变量的类类型以确定是否可以调用该方法。如果该类包含适当的方法声明（或继承了它），则调用可以编译。在执行时，变量所引用的对象的类型决定了实际使用的方法。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_368_0.png)

> > 软件工程观察 12.3
> >
> > 包含对派生类对象引用的基类变量在使用时调用虚方法，实际上会调用重写的派生类版本的方法。

## 12.4 抽象类和方法

当我们思考一个类类型时，我们假设应用程序会创建该类型对象。然而，在某些情况下，声明 *我们永远不打算实例化对象的类* 是有用的。这样的类称为 *抽象类*。由于它们仅用作继承层次结构中的基类，我们称之为 *抽象基类*。这些类 *不能* 用于实例化对象，因为，正如你很快就会看到的，抽象类是 *不完整* 的——派生类必须定义“缺失的部分”。第 12.5.1 节演示了抽象类。

### 抽象类的目的

抽象类的目的主要是提供一个适当的基类，供其他类继承，从而 *共享一个共同的设计*。例如，在图 11.3 的 Shape 层次结构中，派生类继承了作为 Shape 的含义——共同的属性如 `Location`、`Color` 和 `BorderThickness`，以及行为如 `Draw`、`Move`、`Resize` 和 `ChangeColor`。可以用来实例化对象的类称为 *具体类*。此类类提供了它们声明的 *每个* 方法的实现（某些实现可以继承）。例如，我们可以从抽象基类 `TwoDimensionalShape` 派生出具体类 `Circle`、`Square` 和 `Triangle`。类似地，我们可以从抽象基类 `ThreeDimensionalShape` 派生出具体类 `Sphere`、`Cube` 和 `Tetrahedron`。抽象类过于 *通用*，无法创建真实对象——它们仅指定派生类之间的共同点。我们需要在创建对象之前变得更 *具体*。例如，如果你向抽象类 `TwoDimensionalShape` 发送 `Draw` 消息，该类知道二维形状应该是可绘制的，但它 *不知道* 要绘制的 *具体* 形状是什么，因此无法实现真正的 `Draw` 方法。*具体类提供了* 实例化对象所需的具体细节。

### 仅使用抽象基类类型的客户端代码

并非所有继承层次结构都包含抽象类。然而，你经常会编写仅使用 *抽象基类类型* 的客户端代码，以减少客户端代码对一系列特定派生类类型的依赖。例如，你可以编写一个参数为抽象基类类型的方法。调用时，此类方法可以传递 *任何* 直接或间接扩展作为参数类型指定的抽象基类的具体类的对象。

### 层次结构中抽象基类类型的多级

抽象类有时构成层次结构的多个级别。例如，图 11.3 的 Shape 层次结构以 *抽象* 类 `Shape` 开始。在层次结构的下一级有两个更 *抽象* 的类，`TwoDimensionalShape` 和 `ThreeDimensionalShape`。层次结构的下一级声明了 `TwoDimensionalShapes` 的 *具体* 类（`Circle`、`Square` 和 `Triangle`）以及 `ThreeDimensionalShapes` 的 *具体* 类（`Sphere`、`Cube` 和 `Tetrahedron`）。

### 创建抽象类

你通过使用关键字 `abstract` 声明类使其成为抽象类。抽象类通常包含一个或多个抽象方法。抽象方法是在其声明中使用关键字 `abstract` 的方法，如

```java
public abstract void Draw(); // abstract method
```

抽象方法隐式为虚方法且不提供实现。包含抽象方法的类必须声明为抽象类，即使它包含一些具体（非抽象）方法。抽象基类的每个具体派生类还必须提供基类抽象方法的具体实现。我们在图 12.4 中展示了一个具有抽象方法的抽象类的示例。

### 抽象属性

属性也可以声明为抽象或虚，然后在派生类中使用 `override` 关键字重写，就像方法一样。这允许抽象基类指定其派生类的公共属性。抽象类属性的形式为：

```csharp
public abstract PropertyType MyProperty { get; set; }
```

get 和 set 关键字后的分号表示我们为这些访问器 *不提供* 实现。抽象属性省略了 get 访问器和/或 set 访问器的实现。具体派生类 *必须* 为抽象属性声明的每个访问器提供实现。当同时指定 get 和 set 访问器时，每个具体派生类都必须实现两者。如果省略了一个访问器，则派生类 *不允许* 实现该访问器。否则会导致编译错误。

### 构造函数和 static 方法不能为抽象或虚

构造函数和 static 方法不能声明为抽象或虚。构造函数不会被继承，因此这样的构造函数永远无法实现。类似地，派生类不能重写 static 方法，因此这样的 static 方法永远无法实现。

**软件工程观察 12.4**

*抽象类声明了继承它的各种类在类层次结构中直接或间接继承的共同属性和行为。抽象类通常包含一个或多个抽象方法或属性，具体派生类必须重写它们。抽象类的实例变量、具体方法和具体属性受正常的继承规则约束。*

**常见编程错误 12.1**

*尝试实例化抽象类的对象是编译错误。*

**常见编程错误 12.2**

*如果派生类也未声明为抽象，则未能在派生类中实现基类的抽象方法和属性是编译错误。*

### 声明抽象基类类型的变量

虽然我们不能实例化抽象基类的对象，但你很快就会看到，我们 *可以* 使用抽象基类来声明变量，这些变量可以保存对 *从这些抽象类派生的任何具体类* 对象的引用。应用程序通常使用此类变量以多态方式操作派生类对象。此外，你可以使用抽象基类名来调用这些抽象基类中声明的 static 方法。

### 多态性和设备驱动程序

多态性对于实现所谓的 *分层软件系统* 特别有效。在操作系统中，例如，每种不同类型的物理设备可能与其它设备完全不同。即使如此，通用命令也可以读取或写入数据
