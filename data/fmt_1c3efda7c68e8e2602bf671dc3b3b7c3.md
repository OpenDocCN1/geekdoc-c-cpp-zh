
```
/*
#endregion
#region --- Output 3 ---
/*
Name: Darth Vader, Human: Midichlorians: 500000,
Forces: DarkSide, LightSide
Name: Darth Vader, Human: Midichlorians: 500000,
Forces: DarkSide
/*
#endregion
#region --- Output 4 ---
/*
Palatine 议员 [WhatAreYou] Darth Vader: 我是一个西斯。
Palatine 议员 [AreYouSith] Darth Vader: 我是一个西斯学徒，名字叫达斯·维德。
Palatine 议员 [WhatAreYou] Obi Wan Kenobi: 我是一个绝地武士。
Palatine 议员 [AreYouSith] Obi Wan Kenobi: 我不知道任何西斯。

Darth Vader [WhatAreYou] Palatine 议员: 我是一个西斯。
Darth Vader [AreYouSith] Palatine 议员: 我是一个西斯领主，我的学徒是达斯·维德。
Darth Vader [WhatAreYou] Obi Wan Kenobi: 我是一个绝地武士。
Darth Vader [AreYouSith] Obi Wan Kenobi: 我不知道任何西斯。

Obi Wan Kenobi [WhatAreYou] Darth Vader: 我既不是西斯也不是绝地。
Obi Wan Kenobi [AreYouSith] Darth Vader: 我不知道任何西斯。
/*
#endregion
```

# C# 入门

## 迷你用例：汽车租赁

在本项研究中，你将构建一个租赁汽车的门户，就像加油站和租车公司使用的那种一样。显然，你不会构建一个极其详尽且功能完备的系统，而是构建一个基础系统，用于满足租赁和还车的需求。

重要的是，此方案的设计初衷是为了说明面向对象编程（OOP）的某些方面，因此可能不是最优的。

## 强耦合 vs. 松耦合设计

强耦合的解决方案通常更难以更改，对类的更改通常会涉及到周围类和方法调用的更改。

此外，通过在可以使用接口的地方将类实例作为参数传递，从某种程度上也让自己陷入了困境。使用接口会使其变得简单得多，不仅可以传递接口的一部分，还可以完全传递其他实例。以数据层类的实例为例，通过使用接口，你可以轻松地将一个实现切换为另一个；例如从测试数据层切换到生产数据层。

在实现此用例时，你将使用继承来说明抽象类和成员如何在解决方案中使用以重用代码。你还将使用接口来实现类，使解决方案更易维护。通过使用接口，你将能够通过在类类实现 `IDataLayer` 和 `IBookingProcessor` 接口来切换业务层和数据层为其他实现，这被称为接口多态（Interface Polymorphism）。你还将通过不使用类定义参数和类型，而是使用类中实现的接口，使解决方案完全具有灵活性，这被称为接口注入（Interface Injection），是松耦合设计模式的一部分。假设你有一个名为 `IVehicle` 的接口，它定义了任何车辆（如汽车和摩托车）的特征和行为，你现在可以在方法定义中使用 `IVehicle` 接口作为参数，将汽车类或摩托车类的实例传递给方法，因为它们都实现了同一个接口。正如你可能在接口章节中学过的样，这是可行的。

## 汽车租赁规范

为了简单起见，系统计算的是同一天内的所有租赁，不支持半天或按小时租赁。当汽车租赁时间超过一天时，时长应通过从还车日期减去租赁日期来计算。

### 规范

汽车分为若干类别，从开始定义了三个：

- 轿车（Sedan）、组合（Combi）和面包车（Van）。以后可能会添加更多类别。

每次租赁必须通过唯一的预订单号识别。每次租赁定义为每个订单租赁一辆汽车，每个订单只能有一个客户。

类应该放在不同的程序集中以便重用；共有三个程序集，拥有各自的文件夹结构：

- Car Rental（汽车租赁）：Windows Forms 应用程序
- Business Layer（业务层）：存放处理所有业务逻辑的订单处理器
- Data Layer（数据层）：存放实体类和数据层类

在处理预订单时，应用程序将调用 `BookingProcessor` 类实例的相应方法，该类接收 `CollectionDataLayer` 类实例以便与数据源通信，在这种情况下，数据源是存储在集合中的伪数据。`CollectionDataLayer` 类是在实现并使用真实数据源时会被替换的类；从 `BookingProcessor` 类到数据源的所有方法调用都是在该类的实例上进行的。代表数据源的伪数据和集合存储在一个名为 `TestData` 的类中；在现实场景中，这很可能会使用 Entity Framework 实体与数据库通信。

### 价格

汽车类别决定了如何计算价格，所有计算都考虑了两种类型：每日费用和公里费用。

- 轿车：价格 = 每日费用 * 天数
- 组合车：价格 = 每日费用 * 天数 + 日费 * 行驶公里数。日费初始为 1.5，但可能会更改。
- 面包车：价格 = 每日费用 * 天数 + 日费 * 行驶公里数。日费初始为 2.0，距离费初始为 2.5，但可能会更改。

# C# 入门

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_409_0.png)

## 三程序集

解决方案将包含三个程序集：用于 Windows Forms 应用程序的 **Car Rental**，用于业务规则的业务层 **Business Layer**，以及一个与数据源通信的 **Data Layer**。

为了访问 **Business Layer** 和 **Data Layer** 程序集中的类，你需要在应用程序程序集中对它们添加引用。

## 应用程序结构

应用程序在这种情况下使用名为 **Car Rental** 的 Windows Forms 应用程序项目创建。除了默认的项目内容（如表单）外，你还将添加一个名为 **Classes** 的文件夹，并在其中添加所有处理 GUI 所需的类；你将需要创建一个类作为组合框（combo box）项显示数据的模型，以及另一个类作为列表视图（list view）显示数据的模型。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_410_0.png)
![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_410_1.png)
![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_410_2.png)

## 应用程序 GUI

应用程序 GUI 包含一个带有标签页控件的表单，该控件有四个标签页：租车（Rent Vehicle）、还车（Return Booking）、订单（Bookings）和添加数据（Add Data）。

租车标签页包含一个显示可租车辆的列表视图控件、一个包含客户列表的组合框，以及一个租车按钮，该按钮将使用另外两个控件的信息为客户租车。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_410_3.png)

还车标签页包含一个显示可还租车辆的列表视图控件、一个用于指定还车时车辆里程设置的文本框，以及一个还车按钮，该按钮将使用其他控件的数据来还车并计算租用费用。

# C# 初学者教程

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_411_0.png)

订单标签页使用列表视图控件提供系统中已创建所有订单的历史概述。已租出的车辆在“已还（Returned）”列中没有指定日期。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_411_1.png)

添加数据标签页可以使用文本框和组合框来指定或选择数据，从而添加新的车辆和客户。

# C# 初学者教程

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_412_0.png)

## 业务层结构

**业务层（Business Layer）**应该使用**类库（Class Library）**项目创建，而不是**类库（Portal）**项目，因为后者包含了一些你不希望项目中需要的限制。该程序集只有一个名为 **BookingProcessor** 的类，它实现了一个名为 **IBookingProcessor** 的接口，该接口又继承了名为 **IRentalBase** 的接口。

添加两个名为 **Classes** 和 **Interfaces** 的文件夹，并将 **BookingProcessor** 类放在 Classes 文件夹中，将 **IBookingProcessor** 接口放在 Interfaces 文件夹中。**IRentalBase** 接口属于**数据层（Data Layer）**，这意味着你需要在**业务层**程序集中对**数据层**程序集的引用。

**IRentalBase** 接口定义了 **BookingProcessor** 和 **CollectionDataLayer** 类中实现的大部分方法；这两个类都实现了相同的方法，因为应用程序后台代码中的 **BookingProcessor** 类实例将使用 **CollectionDataLayer** 实例并调用其方法来访问数据源；方法具有相同的名称、返回数据类型和参数，可以易于跟踪从业务层到数据层的程序流，同时也实现了 **IRentalBase** 接口的复用。

# C# 初学者教程

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_413_0.png)

## 数据层结构

数据层程序集应该使用类库（Class Library）项目创建，而不是类库（Portal）项目，因为后者包含了一些你不希望项目中需要的限制。此程序集必须包含大多数类，因为它存放了所有的实体类和自定义异常类，以及 `IDataLayer` 接口的任何实现（例如 `CollectionDataLayer` 类）。

`CollectionDataLayer` 类的实例将被注入（发送）到 `BookingProcessor` 类的实例中；来自汽车租车应用程序对数据源的所有调用将通过 `BookingProcessor` 实例进行，以便在从 `BookingProcessor` 实例的方法内部调用数据层之前强制执行任何业务规则。

需要许多文件夹来保持结构的的整洁和易于导航。Data Layers 文件夹将存放 `IDataLayer` 接口的任何实现（例如 `CollectionDataLayer` 类）。Data Source 文件夹将有一个名为 `TestData` 的类，它将作为此应用程序实现中使用的测试数据的数据源。Entities 文件夹将存放所有特定数据的类，这些类可以用于数据库表建模，例如 `Customer`、`Booking` 和 `Vehicle`。Enums 文件夹将包含一个 .cs 文件，存放应用程序所需的所有枚举。Exceptions 文件夹将存放所有自定义的异常（如 `CustomerException`），而 Interfaces 文件夹将存放程序集中使用的所有接口。

# C# 初学者教程

下面的图片显示了实现数据层类时涉及的接口，在此例中，`CollectionDataLayer` 类将用于获取和操作由 `TestData` 类中的集合集合表示的数据源中的数据。请注意，`BookingProcessor` 类实现的 `IRentalBase` 接口在这里是作为 `IDataLayer` 和 `IRentalBase` 接口之间接口继承的一部分被实现的。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_414_0.png)

下面的图片说明了应用程序所需的自定义异常以及它们对 `KeyNotFoundException` 类的继承。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_414_1.png)
![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_414_2.png)

# C# 初学者教程

下面的图片说明了车辆的实现以及实现特定车辆（如 `Car` 类）时使用的接口和继承。请注意，`Car` 类继承了一个中间类 `Vehicle`，这是为了确保某些方法的默认实现是可用的，它还开放了 `IVehicle` 接口作为数据类型，供未来可能添加的所有类型的特定车辆类使用。它还通过在方法中使用接口进行接口注入，而不是使用特定的车辆类作为参数，使得实现更具灵活性。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_415_0.png)

下面的图片插图了剩余实体类 `Customer`、`Booking` 和 `Vehicle` 的实现。虽然严格来说没有必要使用接口来实现这些类，但为了一致性，这里是做了，并且万一将来必须实现实体的子类别，你可能希望对什么是客户有更专门的定义，并复用 `ICustomer` 接口将客户的默认特性和行为实现到专门的类中，确保它们是客户。实现类似结果的另一种方法当然是使用继承和重写方法。

# C# 入门

| ICustomer |
| :--- |
| 接口 (Interface) |
| 属性 (Properties) |
| 名字 (FirstName) |
| ID (Id) |
| 姓 (LastName) |
| 社会安全号 (SocialSecurityNumber) |

| IBooking |
| :--- |
| 接口 (Interface) |
| 属性 (Properties) |
| 费用 (Cost) |
| 客户ID (CustomerId) |
| ID (Id) |
| 已租用 (Rented) |
| 已还 (Returned) |

| IVehicleType |
| :--- |
| 接口 (Interface) |
| 属性 (Properties) |
| 每日基础价 (BasePricePerDay) |
| 每公里基础价 (BasePricePerKm) |
| ID (Id) |
| 公里费 (KmTariff) |
| 名称 (Name) |

| ICustomer |
| :--- |
| 类 (Class) |

| IBooking |
| :--- |
| 类 (Class) |

| IVehicleType |
| :--- |
| 类 (Class) |

### Customer 接口和类

此类将代表客户的特征，这意味着它只包含属性。在所有情况下，属性都是公开的，以便在任何地方访问；数据类型也不应该是秘密，除了 `Id` 属性外，所有属性都应该使用 `string` 数据类型声明。

1. 在 Data Layer 项目的 Interfaces 文件夹中添加一个 `ICustomer` 接口并将其设置为公共。

```csharp
public interface ICustomer
{
```

2. 在接口中定义所有属性，记住在接口中不需要指定访问修饰符。

```csharp
string LastName { get; set; }
```

3. 在 Data Layer 项目的 Entities 文件夹中添加一个公共类 `Customer` 并在类中实现接口。

```csharp
public class Customer : ICustomer
{
```

4. 添加属性最快的方法是从接口中复制它们并为它们添加 `public` 访问修饰符。

```csharp
public string LastName { get; set; }
```

`ICustomer` 接口的完整代码：

```csharp
public interface ICustomer {
  int Id { get; set; }
  string SocialSecurityNumber { get; set; }
  string FirstName { get; set; }
  string LastName { get; set; }
}
```

`Customer` 类的完整代码：

```csharp
public class Customer {
  public int Id { get; set; }
  public string SocialSecurityNumber { get; set; }
  public string FirstName { get; set; }
  public string LastName { get; set; }
}
```

### Booking 接口和类

此类将代表预订的特征，因此只包含属性。在这种情况下，所有属性都是公开的以便在任何地方访问；数据类型也不应该是秘密，所有 `Id` 属性应该使用 `int` 数据类型声明，`Rented` 和 `Returned` 属性应该使用 `DateTime` 数据类型声明，而金额小数部分的费用属性应该使用 `double` 数据类型声明。

1. 在 Data Layer 项目的 Interfaces 文件夹中添加一个名为 `IBooking` 的接口并将其设置为公共。

```csharp
public interface IBooking
{}
```

2. 在接口中定义所有属性，记住在接口中不需要指定任何访问修饰符。

```csharp
double Cost { get; set; }
```

3. 在 Data Layer 项目的 Entities 文件夹中添加一个公共类 `Booking` 并在类中实现接口。

```csharp
public class Booking : IBooking
{}
```

4. 添加属性最快的方法是从接口中复制它们并粘贴到类中，并为它们添加 `public` 访问修饰符。

```csharp
public double Cost { get; set; }
```

`IBooking` 接口的完整代码：
