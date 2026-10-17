
### 10.11 (Time2 类的扩展方法)
使用扩展方法为 `Time2` 类（图 10.5）提供一个增加一小时时间的方法。`Time2` 对象应始终保持一致状态，因此务必考虑到这一点并测试以下用例：
- a) 增加到下一分钟。
- b) 增加到下一个小时。
- c) 增加到下一天（例如从晚上 11:59:50 到凌晨 12:00:00）。

### 10.12 (增强 ComplexNumber 类)
增强 `ComplexNumber` 类（图 10.14），使用重载的 `++` 和 `--` 运算符，使其能够增加或减少复数的实部和虚部。测试你新的重载运算符。

### 10.13 (项目：用重载运算符替换 Rational 方法)
修改第 10 页上的 `Rational` 类（练习 10.8），声明重载运算符 `+`、`-` 和 `/`，以替换该类用于加法、减法、乘法和除法分数的方法。测试你新的重载运算符。

### 10.14 (项目：用重载运算符替换 HugeInteger 方法)
修改 `HugeInteger` 类（练习 10.9），声明重载运算符 `+`、`-`、`!=`、`=`、`<`、`>=` 和 `<=` 以替换该类的 `Add`、`Subtract`、`IsEqualTo`、`IsNotEqualTo`、`IsGreaterThan`、`IsLessThan`、`IsGreaterThanTo` 和 `IsLessThanEqualToTo` 方法。测试你新的重载运算符。如果你很有野心，为乘法 (`*`)、除法 (`/`) 和取余 (`%`) 提供重载运算符。

## 面向编程：继承

## 目标
在本章中你将：
- 理解继承如何促进软件的可重用。
- 创建一个继承基类属性和行为的派生类。
- 在派生类中重写基类方法。
- 使用访问修饰符 `protected` 让派生类方法访问基类成员。
- 使用 `base` 访问基类成员。
- 理解构造函数如何在继承体系中使用。
- 查看 `object` 类的方法概述，它是所有类的直接或间接基类。

![](img/57baed2319be0bb1b5f98674846f2711_475_0.png)

# 476 第 II 章 面向编程：继承

11.1 引言

11.2 基类与派生类

11.3 保护成员

11.4 基类与派生类之间的关系

11.4.1 创建和使用 Employee 类

11.4.2 在不使用继承的情况下创建 BasePlusEmployee 类

11.4.3 创建 CommissionEmployee 继承体系

11.4.4 使用 protected 实例变量进行 CommissionEmployeeBasePlusEmployee 继承

11.4.5 使用 private 实例变量进行 CommissionEmployeeBasePlusEmployee 继承体系

11.5 派生类中的构造函数

11.6 继承的软件工程

11.7 object 类

11.8 结语

总结 | 术语 | 自测复习题 | 自测复习题答案 | 练习题

![](img/57baed2319be0bb1b5f98674846f2711_476_0.png)

## 11.1 引言
本章继续对面向对象编程 (OOP) 的讨论，引入了其主要特征之一——继承。继承是一种软件复用的形式，通过吸收现有类的成员并用新的或修改的能力增强它们来创建一个新类。继承允许你通过重用经过验证的、高性能且经过调试的质量软件来节省开发时间。这也增加了系统被有效实现的概率。

新类所继承的现有类称为基类，而新类称为派生类。派生类通常会添加自己的字段、属性和方法。因此，它比其基类更具体，代表了一组更专门的对象。派生类表现出其基类的行为以及其特有的额外行为。

直接基类是派生类继承的类。类层次结构中的直接基类定义了类之间的继承关系。第 11.7 节列出了 `object`——这是一个 C# 关键字，是框架类库中 `System.Object` 的别名。每个直接或间接扩展（或继承）该对象。第 11.7 节列出了 object 类的方法，其他类都继承这些方法。在单继承中，一个类只被派生一次。C# 支持一个直接基类。在第 12 章中，我们将解释如何使用接口来实现多重继承的许多优势。

在单继承中，一个类只被派生一次。C# 支持一个直接基类。在第 12 章中，我们将解释如何使用接口来实现多重继承的许多优势。

## 11.2 基类与派生类
通常，一个类的对象是另一个类的对象。例如，在几何学中，矩形是四边形（如正方形、平行四形）。因此，`Rectangle` 类可以自 `Quadrilateral`。在这种背景下，`Quadrilateral` 是基类，`Rectangle` 是派生类。矩形是四边形的一种特定类型，但认为四边形是矩形是不正确的——四边形可以是平行四形或其他形状。图 11.1 列出了基类和派生类的示例——基类倾向于通用，而派生类倾向于具体。

| 基类 | 派生类 |
| --- | --- |
| Student | 研究生、本科生 |
| Shape | 圆形、三角形、矩形 |
| Loan | 汽车贷款、房屋改善贷款、抵押贷款 |
| Employee | 教职员工、员工、小时薪工人、佣金员工 |
| SpaceObject | 星星、月球、行星、宇宙飞碟 |
| BankAccount | 支票账户、储蓄账户 |

> **图 11.1** | 继承示例。

由于每个派生类都是其基类的对象，且一个基类可以有多个派生类，因此基类所代表的对象集通常比任何一个派生类所代表的对象集大。例如，基类 `Vehicle` 代表所有车辆——汽车、卡车、自行车等。相比之下，派生类 `car` 代表车辆的一个更更具体的子集。

继承关系形成了层次结构（图 11.2 和 11.3）。基类与其派生类存在于层次关系中。当类参与继承时，它们与其他类产生“关联”。一个类要么成为基类（向其他类提供成员），要么成为派生类（从另一个类继承其成员）。

让我们开发一个示例类层次结构，也称为继承体系（图 11.2）。11.2 中的 UML 类图展示了一个大学社区，它有许多类型的成员，包括员工、学生和校友。员工由教职员工或工作人员组成。教职员工分为行政人员（如院长和系主任）或教师。

## 478 第二章 对象面向编程：继承

类。例如，学生可以是研究生也可以是本科生。本科生可以是大一、大二、大三或大四学生。

![](img/57baed2319be0bb1b5f98674846f2711_478_0.png)

图 11.2 | 大学社区成员（CommunityMembers）的继承层级 UML 类图。

层级图中每个带有空心三角形箭头的行都表示“是一个”（is-a）的关系。顺着箭头方向，我们可以说：“员工（Employee）是一个社区成员”，“”，“教师（Teacher）是一个教职人员（Faculty member）”。CommunityMember 是 Employee 和学生（Student）的直接基类，而校友（Alumnus）是图中所有其他类的间接基类。从底部开始，你可以顺着箭头并将“是一个”关系应用到最顶部的基类。例如，管理员（Administrator）是教职人员，是员工，也是社区成员。

现在考虑图 11.3 中的形状（Shape）层级，它始于基类 Shape。该类由派生类二维形状（TwoDimensionalShape）和三维形状（ThreeDimensionalShape）扩展——Shape 要么是二维形状要么三维形状。该层级的第三层包含特定的二维形状和三维形状。我们可以从底部到该层级最顶部的基类遵循箭头识别“是一个”的关系。例如，三角形（Triangle）是二维形状也是三维形状，而球体（Sphere）是三维形状也是形状。该层级可能包含许多其他类。例如，椭圆（ellipses）和四边形（trapezoids）也是二维形状。

![](img/57baed2319be0bb1b5f98674846f2711_478_1.png)

图 11.3 | 显示形状（Shapes）继承层级的 UML 类图。

## 11.3 protected
并不是所有的类关系都是继承关系。在第 10 章中，我们讨论了“有一个”（has-a）的关系，即类拥有指向其他类的引用的成员。这种关系通过现有类的组合来创建类。例如，给定 Employee、出生日期（BirthDate）和电话（Telephone）类，说“员工是一个出生日期”或“员工是一个电话电话号码”是不恰当的。然而，员工有一个出生日期，员工有一个电话号码。

可以测试基类对象和派生类对象——它们的共同点体现在基类的成员中。扩展公共基类的类对象可以被视为该基类的对象——此类对象与基类有“是”的关系。例如，基类对象不能被视为其派生类对象的对象。例如，所有汽车都是车辆，但并不是所有车辆都是汽车（其他车辆可以是卡车、飞机、自行车等）。本章和第 12 章考虑了“是”的关系的示例。

派生类可以自定义它从基类中继承的方法。在这种情况下，派生类可以重写（重定义）基类方法并带有适当实现，正如我们在章节代码示例中经常看到的那样。

第 10 章讨论了公共（public）和私有（private）访问。只要应用程序拥有该类或其某个派生类的引用，该类的公共成员就是可访问的。类的私有成员仅在类内部可访问。基类的私有成员会被其派生类继承，但不能被派生类的方法和属性直接访问。在本节中，我们引入了访问修饰符（access modifier）。使用 protected 访问提供了公共和私有之间的中间访问级别。基类的 protected 成员可以被基类的成员和其派生类的成员访问，但不能被该类的客户端访问。

所有非基类成员在成为派生类的成员时都会保留它们各自的访问修饰符——基类的公共成员变为派生类的公共成员，基类的保护 成员变为派生类的保护 成员。

派生类可以使用其名称引用继承自基类的公共和保护 成员。当派生类重写基类版本时，可以通过在基类方法名前之前加上关键字和成员访问符（`base.`）从派生类访问该方法。我们将在 11.4 节中讨论访问基类的重写方法。

| 软件工程观察 11.1 |
| :--- |
| 派生类的属性和方法不能直接访问基类的私有成员。派生类只能通过基类提供的非私有方法和属性来更改私有基类字段的状态。 |

| 软件工程观察 11.2 |
| :--- |
| 在基类中声明变量有助于你测试、调试和修改系统。如果派生类可以访问其基类的私有字段，继承自该类的类就可以访问这些本应为私有的字段，信息隐藏的益处就会丢失。 |

## 11.4 基类与派生类之间的关系
在本节中，我们使用一个包含公司薪资应用中各种员工类型的继承层级，来讨论基类与派生类之间的关系。在这家公司中：
- 佣金员工（commission employees）——将由基类对象表示——获得其销售额的百分比，
- 基本工资加佣金员工（base-salary commission employees）——将由派生类对象表示——获得基本工资加其销售额的百分比。

我们将对这些员工类型之间关系的讨论分为五个进化的示例，这些示例经过精心设计，用于教授继承实现良好的软件工程的关键能力：
- 1. 第一个示例代表 `CommissionEmployee` 类，它直接继承自 `object`。
- 2. 第二个示例声明了 `BaseCommissionEmployee` 类，它直接继承自 `object`。
- 3. 第三个示例声明了 `BasePlusCommissionEmployee` 类，它直接继承自 `object`。
- 4. 第四个示例显示了 `BasePlusCommissionEmployee` 继承自 `CommissionEmployee`。
- 5. 第五个示例通过将变量设为私有演示了最佳实践。

在前四个示例中，我们在多个应该使用属性的情况下直接访问变量。在第五个示例中，我们将利用为止介绍的软件工程技术创建易于维护、修改和调试的类。

### 11.4.1 创建和使用 CommissionEmployee
我们从 `CommissionEmployee`（图 11.4）开始。第 5 行冒号（`:`）后面的类名 `object` 标识了 `CommissionEmployee` 扩展（即继承自）`object` 类（System.Object 的别名）。使用继承从现有类创建类。每个类（`object` 除外）都扩展一个现有类。`CommissionEmployee` 类扩展自 `object`，object 方法没有字段（第 11.7 节总结了对象的方法）。每个类直接或间接继承自 `object`。如果一个类没有指定继承自另一个类，它将隐式继承自 `object`。由于这个原因，你通常不在代码中包含 "object"——我们在示例中包含了它；但在书中不再包含。

```csharp
// Fig. CommissionEmployee.cs
// CommissionEmployee 代表一个佣金员工。
using System;
public class CommissionEmployee : object {
    public string FirstName { get; }
    public string LastName { get; }
    public string SocialSecurityNumber { get; }
    private decimal grossSales;// 每周销售额
    private decimal commissionRate;//佣金百分比

    // 无参数构造函数
    public CommissionEmployee(string firstName, string lastName,
        string socialSecurityNumber, decimal grossSales,
        decimal commissionRate) {
        // 此处隐式调用 object 构造函数
        FirstName = firstName;
        LastName = lastName;
        SocialSecurityNumber = socialSecurityNumber;
        GrossSales = grossSales; // 验证销售额
        commissionRate = commissionRate; // 验证佣金
    }

    // 用于获取和设置佣金员工销售额的属性
    public decimal GrossSales {
        get {
            return grossSales;
        }
        set {
            if (value < 0) // 验证
                throw new ArgumentOutOfRangeException(nameof(value),
                    value, $"${nameof(GrossSales)} 必须 >= 0");
```

图 11.4 CommissionEmployee 类代表一个佣金员工。（第一部分，共 2 部分）

# 482 第二章 面向对象编程：继承

```csharp
grossSales = value;
}
// 获取和设置员工佣金率的属性
public decimal CommissionRate
{
    get
        return commissionRate;
    set
    {
        if (value <= 0 || value >= 1) // 校验
            throw new ArgumentOutOfRangeException(nameof(value), value, $"{nameof(CommissionRate)} 必须大于 0 且 1");
        commissionRate = value;
    }
}
```

// 计算员工薪金

public decimal Earnings() => commissionRate * grossSales;

// 返回 CommissionEmployee 对象的字符串表示

public override string ToString()

{

    return $"employee: {FirstName} {LastName}\n" +

           $"{SocialSecurityNumber}\n" +

           $"gross sales: {grossSales}\n" +

           $"commission rate: {commissionRate:F2};";

}
