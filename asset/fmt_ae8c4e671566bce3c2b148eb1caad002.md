
如果 `pay` 未被重写，`Volunteer` 类将被视为抽象类且无法实例化。

请注意，当志愿者在 `Staff` 的 `payday` 方法中被“支付”时，会打印一条简单的感谢信息。在所有其他情况下，当薪酬值大于零时，则打印付款本身。

`Listing 10.5` 中展示的 `Employee` 类代表按特定费率每个工资期领取报酬的员工。薪酬率以及员工的社保号码，连同其他基本信息一起传递给 `Employee` 构造函数。基本信息通过 `super` 引用传递给 `StaffMember` 的构造函数。

`Employee` 的 `toString` 方法被重写，以将 `Employee` 管理的额外信息与父类版本的 `toString` 返回的信息拼接起来，后者通过 `super` 引用调用。`Employee` 的 `pay` 方法仅返回该员工的薪酬率。

`Listing 10.6` 中展示的 `Executive` 类代表除正常薪酬率外还可能获得奖金的员工。`Executive` 类派生自 `Employee`，因此继承自 `StaffMember` 和 `Employee`。`Executive` 的构造函数将其信息传递给 `Employee` 构造函数，并将高管奖金设为零。

通过 `awardBonus` 方法向高管授予奖金。该方法在 `Staff` 构造函数中对 `staffList` 数组中唯一的执行官调用。请注意，必须将通用的 `StaffMember` 引用强制转换为 `Executive` 引用才能调用 `awardBonus` 方法（`StaffMember` 不存在该方法）。

`Executive` 类重写了 `pay` 方法，使其首先按普通员工的方式确定付款，然后加上奖金。`Employee` 类的 `pay` 方法通过 `super` 调用以获得正常付款金额。这种技术比仅使用 `payRate` 变量更好，因为如果我们选择更改 `Employee` 对象的支付方式，更改将自动反映在 `Executive` 中。奖金发放后会被重置为零。

`Listing 10.7` 中展示的 `Hourly` 类代表按小时计酬的员工。它跟踪当前工资期内工作的小时数，可通过 `addHours` 方法的调用进行修改。该方法由 `Staff` 的 `payday` 方法调用。`Hourly` 的 `pay` 方法根据工作小时数确定付款，然后将小时数重置为零。

### LISTING 10.5

```java
//******************************
// Employee.java      Author: Lewis/Loftus
// Represents a general paid employee.
//******************************
public class Employee extends StaffMember
{
    protected String socialSecurityNumber;
    protected double payRate;
    //-------------------------------------------------------------
    // Constructor: Sets up this employee with the specified information.
    //-------------------------------------------------------------
    public Employee (String eName, String eAddress, String ePhone,
                     String socSecNumber, double rate)
    {
        super (eName, eAddress, ePhone);
        socialSecurityNumber = socSecNumber;
        payRate = rate;
    }
    //-------------------------------------------------------------
    // Returns information about an employee as a string.
    //-------------------------------------------------------------
    public String toString()
    {
        String result = super.toString();
        result += "\nSocial Security Number: " + socialSecurityNumber;
        return result;
    }
    //-------------------------------------------------------------
    // Returns the pay rate for this employee.
    //-------------------------------------------------------------
    public double pay()
    {
        return payRate;
    }
}
```

### LISTING 10.6

```java
//************************************************************************
// Executive.java      Author: Lewis/Loftus
//
// Represents an executive staff member, who can earn a bonus.
//************************************************************************
public class Executive extends Employee
{
    private double bonus;
    //-------------------------------------------------------------
    // Constructor: Sets up this executive with the specified
    // information.
    //-------------------------------------------------------------
    public Executive (String eName, String eAddress, String ePhone,
                      String socSecNumber, double rate)
    {
        super (eName, eAddress, ePhone, socSecNumber, rate);
        bonus = 0;  // bonus has yet to be awarded
    }
    //-------------------------------------------------------------
    // Awards the specified bonus to this executive.
    //-------------------------------------------------------------
    public void awardBonus (double execBonus)
    {
        bonus = execBonus;
    }
    //-------------------------------------------------------------
    // Computes and returns the pay for an executive, which is the
    // regular employee payment plus a one-time bonus.
    //-------------------------------------------------------------
    public double pay()
    {
        double payment = super.pay() + bonus;
        bonus = 0;
        return payment;
    }
}
```

### LISTING 10.7

```java
//***************************************************************************
// Hourly.java      Author: Lewis/Loftus
//
// Represents an employee that gets paid by the hour.
//***************************************************************************
public class Hourly extends Employee
{
    private int hoursWorked;
    //-------------------------------------------------------------
    // Constructor: Sets up this hourly employee using the specified
    // information.
    //-------------------------------------------------------------
    public Hourly (String eName, String eAddress, String ePhone,
                   String socSecNumber, double rate)
    {
        super (eName, eAddress, ePhone, socSecNumber, rate);
        hoursWorked = 0;
    }
    //-------------------------------------------------------------
    // Adds the specified number of hours to this employee's
    // accumulated hours.
    //-------------------------------------------------------------
    public void addHours (int moreHours)
    {
        hoursWorked += moreHours;
    }
    //-------------------------------------------------------------
    // Computes and returns the pay for this hourly employee.
    //-------------------------------------------------------------
    public double pay()
    {
        double payment = payRate * hoursWorked;
        hoursWorked = 0;
        return payment;
    }
}
```

### 清单 10.7 续

```java
//-------------------------------------------------------------------
// Returns information about this hourly employee as a string.
//-------------------------------------------------------------------
public String toString()
{
    String result = super.toString();
    result += "\nCurrent hours: " + hoursWorked;
    return result;
}
}
```

### 自我复习题（答案见附录 N）

SR 10.3 继承如何支持多态？

SR 10.4 假设类 `MusicPlayer` 是类 `CDPlayer` 的父类。以下语句序列是否合法？请解释。

```java
MusicPlayer mplayer = new MusicPlayer();
CDPlayer cdplayer = new CDPlayer();
mplayer = cdplayer;
```

SR 10.5 假设类 `MusicPlayer` 是类 `CDPlayer` 的父类。以下语句序列是否合法？请解释。

```java
MusicPlayer mplayer = new MusicPlayer();
CDPlayer cdplayer = new CDPlayer();
cdplayer = mplayer;
```

SR 10.6 重写与多态有何关系？

SR 10.7 为什么 Firm 示例中的 `StaffMember` 类被声明为抽象类？

SR 10.8 既然 `pay` 方法是抽象方法，并且在该层级没有方法体，为什么还要在 `StaffMember` 类中声明它？

SR 10.9 在 `Staff` 类的 `payday` 方法中，以下代码行会调用哪个 `pay` 方法？

```java
amount = staffList[count].pay();
```

## 10.3 通过接口实现多态

> 关键概念
> 接口名可用于声明对象引用变量。

现在让我们探讨如何使用接口创建多态引用。正如我们多次看到的，类名可以用来声明对象引用变量的类型。类似地，接口名也可以用作引用变量的类型。接口引用变量可以引用任何实现了该接口的类的任何对象。

假设我们声明一个名为 `Speaker` 的接口，如下所示：

```java
public interface Speaker
{
    public void speak();
    public void announce (String str);
}
```

现在可以使用接口名 `Speaker` 来声明对象引用变量：

```java
Speaker current;
```

> 关键概念
> 接口引用可以引用任何实现了该接口的类的任何对象。

引用变量 `current` 可以用于引用任何实现了 `Speaker` 接口的类的任何对象。例如，如果我们定义一个名为 `Philosopher` 的类，使其实现 `Speaker` 接口，那么我们可以将 `Philosopher` 对象赋值给 `Speaker` 引用，如下所示：

```java
current = new Philosopher();
```

这个赋值是合法的，因为 `Philosopher` 是一种 `Speaker`。在这个意义上，类与其接口之间的关系与子类和父类之间的关系相同。这是一种“是一个”关系。而这个关系构成了多态的基础。

接口引用的灵活性使我们能够创建多态引用。正如我们在本章前面看到的，利用继承，我们可以创建一个多态引用，只要一组对象通过继承相关联，它就可以引用其中任意一个对象。利用接口，我们可以在实现同一接口的对象之间创建类似的多态引用。

例如，如果我们创建一个名为 `Dog` 的类，它也实现了 `Speaker` 接口，那么它也可以被赋值给 `Speaker` 引用变量。实际上，同一个引用变量可以在某一时刻引用 `Philosopher` 对象，随后再引用 `Dog` 对象。以下代码行说明了这一点：

```java
Speaker guest;
guest = new Philosopher();
guest.speak();
guest = new Dog();
guest.speak();
```

在这段代码中，第一次调用 `speak` 方法时，它调用的是 `Philosopher` 类中定义的 `speak` 方法。第二次调用时，它调用的是 `Dog` 类的 `speak` 方法。与通过继承实现的多态引用一样，决定调用哪个方法的不是引用的类型，而是引用在调用时刻所指向的对象的类型。

注意，当我们使用接口引用变量时，只能调用接口中定义的方法，即使它所引用的对象还有其他可以响应的方法。例如，假设 `Philosopher` 类还定义了一个名为 `pontificate` 的公共方法。以下代码的第二行会产生编译错误，即使该对象实际上可以响应 `pontificate` 方法：

```java
Speaker special = new Philosopher();
special.pontificate();  // generates a compiler error
```

问题在于编译器只能确定该对象是一个 `Speaker`，因此只能保证该对象能够响应 `speak` 和 `announce` 方法。由于引用变量 `special` 可能引用 `Dog` 对象（而 `Dog` 对象不能 `pontificate`），所以它不允许该调用。如果我们知道在特定情况下这种调用是合法的，我们可以将该对象强制转换为适当的引用，以便编译器接受它，如下所示：

```java
((Philosopher)special).pontificate();
```
