

## 12.7 案例研究：创建和使用接口

实现接口 `IPayable`。然后我们修改 `Employee` 类，使其也实现 `IPayable` 接口。

`Invoice` 和 `Employee` 类代表公司必须能够计算支付金额的对象。这两个类都实现了 `IPayable`，因此应用程序可以在 `Invoice` 对象和 `Employee` 对象上调用 `GetPaymentAmount` 方法。这实现了我们公司应付账应用程序所需的对 `Invoice` 和 `Employee` 的多态处理。

## 良好的编程实践 12.1

按照惯例，接口的名称以 `I` 开头（例如 `IPayable`）。这区分了接口和类，提高了代码的可读性。

## 良好的编程实践 12.2

在接口中声明方法时，选择一个能以通用的方式描述方法目的的名称，因为该方法可能由许多不相关的类实现。

## **包含接口的 UML 图**

图 12.10 中的 UML 类图显示了我们应付账应用程序中使用的接口和类层次结构。该层次结构从接口 `IPayable` 开始。UML 通过在名称上方使用尖括号括起来的 `«interface»` 字样来区分接口和类。UML 通过“实现”（realization）表示类与接口之间的关系。一个类被认为“实现”（«realize»）或执行一个接口。类图将实现建模为从实现类指向接口的带有空心箭头的虚线箭头。图 12.10 表明 `Invoice` 和 `Employee` 类分别实现（即执行）接口 `IPayable`。正如图 12.2 的类图所示，`Employee` 类以斜体显示，表示它是一个抽象类。具体的 `SalariedEmployee` 继承自 `Employee` 并继承了它对接口 `IPayable` 的基类实现。图 12.10 可以表示第 12.5 节的整个 `Employee` 层次结构——为了保持后续内容的简洁，我们没有包含 `HourlyEmployee`、`CommissionEmployee` 和 `BasePlusCommissionEmployee` 类。

![](img/57baed2319be0bb1b5f98674846f2711_535_0.png)

**图. 12.10** | IPayable 接口和类层次结构的 UML 类图。

### 12.7.2 声明接口 IPayable

接口 `IPayable` 的声明见图 12.11 的第 3 行。接口 `IPayable` 包含抽象方法 `GetPaymentAmount`（第 5 行）。该方法不能显式声明为 `public` 或 `abstract`。接口可以有任意数量的成员，方法可以有参数。

```cs
// 12.11: IPayable.cs
// IPayable interface declaration.
public interface IPayable
{
    decimal GetPaymentAmount(); // calculate payment; no implementation
}
```

图 12.11 | IPayable 接口声明。

### 12.7.3 创建类 Invoice

我们现在创建 `Invoice` 类（图 12.12）表示包含某类零件信息的简单发票。该类包含属性 `PartNumber`（第 7 行）、`PartDescription`（第 8 行）、`Quantity`（第 23–39 行）和 `PriceItem`（第 42–58 行），分别表示零件号、零件描述、订单零件数量和单价。`Invoice` 类还包含一个构造函数（第 13–20 行）以及一个 `ToString` 方法（第 61–63 行），该方法返回 `Invoice` 对象的字符串表示。属性 `Quantity` 和 `PriceItem` 确保了数量和单价仅被赋予非负值。

```cs
// 12.12: Invoice.cs
// Invoice class implements IPayable.
using System;
public class Invoice : IPayable
{
    public string PartNumber { get; }
    public string PartDescription { get; }
    private int quantity;
    private decimal priceItem;
    // four-parameter constructor
    public Invoice(string partNumber, string partDescription, int quantity,
        decimal priceItem)
    {
        PartNumber = partNumber;
        PartDescription = partDescription;
        Quantity = quantity; // validate quantity
        PriceItem = priceItem; // validate price per item
    }
```

图 12.12 | Invoice 类实现 IPayable。（部分 2.）

```cs
// property that gets and sets the quantity on the invoice
public int Quantity
{
    get
    {
        return quantity;
    }
    set
    {
        if (value < 0) // validation
            throw new ArgumentOutOfRangeException(nameof(value),
            $"{nameof(Quantity)} must be >= 0");
        quantity = value;
    }
}
// property that gets and sets the price per item
public decimal PriceItem
{
    get
    {
        return priceItem;
    }
    set
    {
        if (value < 0) // validation
            throw new ArgumentOutOfRangeException(nameof(value),
                $"{nameof(PriceItem)} must be >= 0");
        priceItem = value;
    }
}
// string representation of Invoice ToString() =>
public override string ToString() =>
    $"{PartNumber: {PartDescription}}\n" +
    $"{quantity: {Quantity}\n per item: {PriceItem:C}";
// method required to carry out contract with interface IPayable
public decimal GetPaymentAmount() => Quantity * PriceItem;
```

图 12.12 | Invoice 类实现 IPayable（部分 2）

第 5 行表示 `Invoice` 类实现了 `IPayable`。与所有类一样，`Invoice` 类也继承自 `object` 类。一个类的所有对象都可以实现多个接口，在这种情况下，它们与每个实现的类型都具有 `is-a` 。

## 第 12 章 OOP：多态与接口

要实现多个接口，在类声明的冒号（`:`）后使用逗号分隔的接口名称列表，例如：

```cs
public class ClassName : BaseClassName, FirstInterface, SecondInterface
```

当一个类继承自基类并实现一个或多个接口时，类声明必须在任何接口之前列出基类名称。

> 软件工程观察 12.6 C 语言允许派生类继承多个类，但它允许一个类继承一个基类并实现任意数量的接口。

`Invoice` 类实现了第 66 行声明的 `IPayable` 接口中的方法。该方法将 `quantity` 和 `priceItem` 的值（通过相应的属性获取）相乘并返回结果。此方法了 `IPayable` 接口中方法的实现要求——我们与编译器履行了接口合约。

### 12.7.4 修改 Employee 类以实现 IPayable

我们现在修改 `Employee` 以实现 `IPayable` 接口。

修改 `Employee` 以实现 `IPayable` 接口（图 12.13）。类声明与图 12.4 相同，例外在于：

- 图 12.13 的第 27 行表示类实现了接口 `IPayable`。
- `GetPaymentAmount` 方法是在派生类上调用的。在执行时，当在派生对象上调用时会调用 `Employee` 的抽象方法。

```cs
// 12.13: Employee.cs
// Employee base class that implements IPayable
public abstract class Employee : IPayable
{
    public string FirstName { get; }
    public string LastName { get; }
    public string socialNumber;

    // three-parameter constructor
    public Employee(string firstName, string lastName,
        string socialNumber)
    {
        FirstName = firstName;
        LastName = lastName;
        this.socialNumber = socialNumber;
    }

    // string representation of Employee object
    public override string ToString() =>
        $"{LastName}\n" +
        $"social: {socialNumber}";

    // abstract method overridden by derived classes
    public abstract decimal Earnings();

    // implementing GetPaymentAmount here
    public virtual decimal GetPaymentAmount() => Earnings();
}
```

图 12.13 | Employee 基类实现 IPayable。（部分部分）

## Employee 的派生类与接口 IPayable

当一个类实现接口时，`is-a` 关系继承。`Employee` 类实现了 `IPayable`，因此我们可以说 `Employee` 是 `IPayable`，并且任何 `Employee` 对象也是 `IPayable`。如果我们用图 12.13 中的新 `Employee` 类更新第 12.5 节的层次结构，`SalariedEmployees`、`HourlyEmployees`、`CommissionEmployees` 和 `BasePlusEmployees` 都是 `IPayable` 对象。我们可以将 `SalariedEmployee` 派生类的引用赋值给基类接口，我们可以将 `SalariedEmployee` 对象（或任何 `Employee` 派生对象）赋值给 `IPayable` 变量。`Invoice` 实现 `IPayable`，因此 `Invoice` 也是 `IPayable` 对象，我们可以将 `Invoice` 对象的引用赋值给 `IPayable` 变量。

![](img/57baed2319be0bb1b5f98674846f2711_539_0.png)

> 软件工程观察 12.7 继承和接口在实现 `is-a` 关系上是。实现接口的类可以被认为是接口类型的对象。实现接口的类的派生类的对象也可以被认为是接口类型的对象。

![](img/57baed2319be0bb1b5f98674846f2711_539_1.png)

> 软件工程观察 12.8 基类与派生类之间、接口与实现接口的类之间的 `is-a` 关系在将对象传递给方法时成立。当方法接收基类或接口类型的参数时，它多态地处理接收到的对象。

### 12.7.5 使用接口 IPayable 多态地处理发票和员工

`PayableInterfaceTest`（图 12.14）说明了接口 `IPayable` 可用于在类中处理一组 `Invoice` 和 `Employee`。第 12–16 行创建了一个名为 `payableObjects` 的 `List<IPayable>`，并用四个对象初始化它——两个 `Invoice` 对象（第 13–14 行）和两个 `SalariedEmployee` 对象（第 15–16 行）。这些赋值是允许的，因为 `Invoice` 是 `IPayable`，`SalariedEmployee` 是 `IPayable`。

