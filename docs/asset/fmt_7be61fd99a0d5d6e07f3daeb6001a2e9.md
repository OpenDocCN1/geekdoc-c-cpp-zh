
`public Employee` (`String` `eName`, `String` `eAddress`, `String` `ePhone`,

`String` `socSecNumber`, `double` `rate`) {

`super(eName, eAddress, ePhone)`;

`socialSecurityNumber` = `socSecNumber`;

`payRate` = `rate`;

}

// Returns information about an employee as a string.

`public String` `toString()` {

`String` `result` = `super.toString()`;

`result` += `"\nSocial Security Number: "` + `socialSecurityNumber`;

`return result`;

}

// Returns the pay for this employee.

`public double` `pay()` {

`return payRate`;

}

}

# 10.2 通过继承实现多态

## 列表 10.6

```java
****************************************************
// Executive.java Author: Lewis/Loftus
// Represents an executive staff member, who can earn a bonus.
****************************************************
public class Executive extends Employee {
    private double bonus;
    //--------------------------------------------------------------------
    // Constructor: Sets up this executive with the specified
    // information.
    //--------------------------------------------------------------------
    public Executive(String eName, String eAddress, String ePhone,
                     String socSecNumber, double rate) {
        super(eName, eAddress, ePhone, socSecNumber, rate);
        bonus = 0; // bonus has yet to be awarded
    }
    //--------------------------------------------------------------------
    // Awards the specified bonus to this executive.
    //--------------------------------------------------------------------
    public void awardBonus(double execBonus) {
        bonus = execBonus;
    }
    //--------------------------------------------------------------------
    // Computes and returns the pay for an executive, which is the
// regular employee payment plus a one-time bonus.
    //--------------------------------------------------------------------
    public double pay() {
        double payment = super.pay() + bonus;
        bonus = 0;
        return payment;
    }
}
```

## 列表 10.7

```java
****************************************************
// Hourly.java
// Author: Lewis/Loftus
// Represents an employee that gets paid by the hour.
****************************************************
public class Hourly extends Employee
{
    private int hoursWorked;
    //--------------------------------------------------------------------
    // Constructor: Sets up this hourly employee using the specified
    // information.
    //--------------------------------------------------------------------
    public Hourly (String eName, String eAddress, String ePhone,
                 String socSecNumber, double rate) {
        super(eName, eAddress, ePhone, socSecNumber, rate);
        hoursWorked = 0;
    }
    //--------------------------------------------------------------------
    // Adds the specified number of hours to this employee's
    // accumulated hours.
    //--------------------------------------------------------------------
    public void addHours(int moreHours) {
        hoursWorked += moreHours;
    }
    //--------------------------------------------------------------------
    // Computes and returns the pay for this hourly employee.
    //--------------------------------------------------------------------
    public double pay() {
        double payment = payRate * hoursWorked;
        hoursWorked = 0;
        return payment;
    }
}
```

## 列表 10.7 继续

```java
//--- 返回关于此小时制员工的字符串信息。
//---
public String toString()
{
    String result = super.toString();
    result += "\nCurrent工作时长: " + hoursWorked;
    return result;
}
```

## 自测习题（答案见附录 N）

- SR 10.3 继承如何支持多态性？
- SR 10.4 假设 `MusicPlayer` 类是 `CDPlayer` 类的父类。以下语句序列合法吗？请解释。

`MusicPlayer` `mplayer` = `new MusicPlayer()`;
`CDPlayer` `cdplayer` = `new CDPlayer()`;
`mplayer` = `cdplayer`;
- SR 10.5 假设 `MusicPlayer` 类是 `CDPlayer` 类的父类。以下语句序列合法吗？请解释。

`MusicPlayer` `mplayer` = `new MusicPlayer()`;
`CDPlayer` `cdplayer` = `new CDPlayer()`;
`mplayer` = `cdplayer`;
- SR 10.6 方法重写与多态性之间是什么关系？
- SR 10.7 为什么 Firm 示例中的 `StaffMember` 类被声明为抽象类？
- SR 10.8 既然 `pay` 方法在 `StaffMember` 类中是抽象的且没有体，为什么要在 `StaffMember` 类中声明它？
- SR 10.9 在 `Staff` 类的 `payday` 方法中，下行代码调用了哪一个 `pay` 方法？

`amount` = `staffList[count].pay()`;

# 10.3 通过接口实现多态

> 核心概念
接口名称可以用于声明对象引用变量。

现在让我们检查如何使用接口来创建多态引用。正如我们多次看到的，类名可以被用于声明对象引用变量的类型。同样，接口名也可以被用作引用变量的类型。接口引用变量可以指向实现了该接口的任何类的任何对象。

假设我们如下所示声明一个接口 `Speaker`：

```java
public interface Speaker
{
    public void speak();
    public void announce (String str);
}
```

现在接口名 `Speaker` 可以用于声明一个对象引用变量：

`Speaker` `current`;

> 核心概念
接口引用可以指向任何实现了 `Speaker` 接口的任何类的任何对象。例如，如果我们定义一个类 `Philosopher` 使其实现 `Speaker` 接口，那么我们就可以如下将一个 `Philosopher` 对象赋值给 `Speaker` 引用变量：

```java
current = new Philosopher();
```

该赋值是有效的，因为 `Philosopher` 是一个 `Speaker`。从这种意义上说，类与其接口之间的关系等于子类与其父类之间的关系。这是一种“是”（is）的关系。这种关系形成了多态的基础。

接口引用的灵活性允许我们创建多态引用。正如我们在本章之前看到的，通过继承，我们可以创建一个多态引用，只要这些对象具有继承关系，就可以指向对象集合中的任何一个。使用接口，我们可以在实现相同接口的对象之间创建类似的多态引用。例如，如果我们创建一个也实现 `Speaker` 接口的类 `Dog`，它也可以被赋值给 `Speaker` 变量。事实上，同一个引用变量在某一个时刻可以指向一个 `Philosopher` 对象，稍后指向一个 `Dog` 对象。以下代码说明了这一点：

```java
Speaker guest;
guest = new Philosopher();
guest.speak();
guest = new Dog();
guest.speak();
```

在这段代码中，第一次调用 `speak` 方法时，它调用了在 `Philosopher` 类中定义的 `speak` 方法。第二次调用时，它调用了 `Dog` 类的 `speak` 方法。与通过继承实现多态引用一样，决定调用哪个方法的不是引用的类型，而是基于调用时引用所指向的对象的类型。请注意，当使用接口引用时，我们只能调用接口中定义的方法，即使对象实际上响应了其他方法。例如，假设 `Philosopher` 类还定义了一个公共方法 `pontificate`。即使对象对 `pontificate` 有响应，以下代码的第二行也会产生编译错误：

```java
Speaker special = new Philosopher();
special.pontificate(); // 产生编译错误
```

问题在于，编译器只能断定该对象是一个 `Speaker`，因此只能保证该对象可以响应 `speak` 和 `announce`。如果我们知道在特定情况下可以将该对象强制转换（cast）为适当的引用，以便编译器接受它，如下所示：

```java
((Philosopher)special).pontificate();
```

与基于继承的多态引用一样，接口名可以被作方法参数的类型。在这些情况下，实现接口的任何类的对象都可以传递给方法。以下方法接受一个 `Speaker` 对象作为参数：

```java
public void sayIt (Speaker current)
{
    current.speak();
}
```

> 核心概念
方法的参数可以是多态的，这使得方法对其参数具有灵活的控制。将多态引用作为方法的正式参数是一种技术。它允许方法控制传递给它的参数类型，同时赋予了接受各种类型参数的灵活性。

## 自测习题（答案见附录 N）

- SR 10.10 如何使用接口完成多态性？

# 10.4 排序

让我们检查一个适合多态解决方案的问题。排序是按照定义良好的顺序安排项目列表的过程。例如，你可能希望对姓名列表按字母顺序排序，或者将调查结果列表按降序排列。多年来，人们已经开发并批判了许多排序算法。排序被认为是计算机科学中的一个经典领域。

本节将检查两种排序算法：选择排序和插入排序。我们不会深入探讨排序算法的细节，而是介绍该主题并建立一些基本概念。

## 选择排序

排序算法通过接继将特定值放在其最终位置来对列表。换句话说，对于列表中的每个位置，算法都会选择该位置的值并将其放置。让我们考虑将数值列表升序排列的问题。选择排序的通用策略是：扫描整个列表找到最小值，将其与列表的第一个元素交换。扫描剩余列表（除去第一个元素）找到最小值，将其与列表的第二个元素交换。扫描剩余列表（除去前两个元素）找到最小值，将其与列表的第三个元素交换。重复此过程直到最后一个位置（该位置将包含最大值）。当过程完成后，列表就被排序了。图 10.2 展示了选择排序的使用。

![](img/7f8e069c1898b741edc1dfeed34b0c1_532_0.png)

图 10.2 选择排序处理

# 第10章 多态

让我们来看一个例子。列表10.8 中的程序使用选择排序对 `Contact` 对象列表进行升序排序。

列表10.9 显示了 `Sorting` 类。它包含了静态排序算法。`PhoneList` 程序使用了 `selectionSort` 方法。另一个方法将在本节中讨论。

`selectionSort` 方法接受 `Comparable` 对象数组进行排序。回想 `Comparable` 是一个仅包含一个方法 `compare` 的接口，该方法旨在返回一个整数，如果执行对象小于、等于或大于所比较的对象，则分别返回小于、等于或大于零。

任何实现 `Comparable` 接口的类都必须定义 `compare` 方法。因此，任何对象都可以与另一个对象进行比较以确定它们的相对顺序。

`selectionSort` 方法是多态的。它完全没有引用 `Contact` 对象，却被用于对 `Contact` 对象数组进行排序。只要对象是 `Comparable`，`selectionSort` 方法就可以排序任何对象数组。

每个 `Contact` 对象代表一个有姓和电话号码的人。列表10.10 显示了 `Contact` 类。

`Contact` 类实现了 `Comparable` 接口，因此提供了 `compareTo` 方法的定义。在这种情况下，联系人按姓排序；如果两个联系人的姓相同，则使用名字。

## 10.4 排序

字体 代码列表 10.8

```java
********************************************************************
// PhoneList.java Author: Lewis/Loftus
// 测试排序算法的驱动程序。
********************************************************************
public class PhoneList {
    // 创建 Contact 对象的数组，对其进行排序，然后打印出来。
    //
    public static void main(String[] args) {
        Contact[] friends = new Contact[8];
        friends[0] = new Contact("John", "Smith", "610-555-7384");
        friends[1] = new Contact("Sarah", "Barnes", "215-555-3827");
        friends[2] = new Contact("Mark", "Riley", "733-555-2969");
        friends[3] = new Contact("Laura", "Getz", "663-555-3984");
        friends[4] = new Contact("Larry", "Smith", "464-555-3489");
        friends[5] = new Contact("Frank", "Phelps", "322-555-2284");
```
