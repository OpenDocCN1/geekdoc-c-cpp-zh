
将此推推到极端，`Object`（对象）引用可以用于指向任何对象，因为所有类最终都是 `Object` 类的后代。例如，`ArrayList` 使用了多态性，因为它被设计为持有 `Object` 引用。这就是为什么一个没有指定元素类型的 `ArrayList` 可以存储任何种类的对象。事实上，一个特定的 `ArrayList` 可以同时持有多个不同类型的对象，因为根据继承关系，它们都是 `Object` 对象。

引用变量 `creature` 可以是多态的，因为在任何时间点它都可以指向一个 `Animal` 对象、一个 `Mammal` 对象或一个 `Horse` 对象。假设这三个类都有一个名为 `move` 的方法，并且以不同的方式实现（因为子类重写了它所继承的定义）。下面的调用执行了 `move` 方法，但它调用的特定版本是在运行时确定的：

```java
creature.move();
```

当执行这行代码时，如果 `creature` 目前指向一个 `Animal` 对象，则调用 `Animal` 类的 `move` 方法。同样，如果 `creature` 目前指向一个 `Mammal` 对象，则调用 `Mammal` 版本的 `move` 方法。同样，如果它目前指向一个 `Horse` 对象。

当然，由于 `Animal` 和 `Mammal` 代表的是通用概念，它们可以被定义为抽象类。这种情况并不会消除拥有多态引用的能力。假设 `Mammal` 类中的 `move` 方法是抽象的，并在 `Horse`、`Dog`（狗）和 `Whale`（鲸）类（均派自 `Mammal`）中给唯一的定义。`Mammal` 引用变量可以指向从 `Horse`、`Dog` 和 `Whale` 类创建的任何对象，并用于执行其中任何一个对象的 `move` 方法。

让我们看看图 10.1 所示类层次结构。这些类代表了特定公司可能雇用的各种员工。让我们探讨一个使用该层次结构向他们支付工资的示例：一组各种类型的员工。

列表 10.1 中的 `Firm` 类包含一个主驱动程序，它创建了一个员工团队 `Staff` 并调用 `payday` 方法向他们支付工资。程序输出关于每个员工的信息以及他们各获得了多少工资（如果有的话）。

列表 10.2 中的 `Staff` 类维护了一个代表各种类型单个员工的对象数组。注意，该数组被声明为持有其他类，如 `Executive`（高管）和 `Employee`（员工）。它实际上由其他类创建的对象填充，这些类都是 `StaffMember` 类的后代，因此赋值是有效的。`stafflist` 数组填充了多态引用。

`Staff` 类的 `payday` 方法扫描员工列表，打印他们的信息并调用它们的 `pay` 方法来确定每位员工应该付付多少工资。`pay` 方法的调用是多态的，因为每个类都有它们自己的 `pay` 方法版本。

列表 10.3 显示的 `StaffMember` 类是抽象的。它不代表特定类型的员工，也不打算实例化。相反，它作为所有员工类的祖先，并包含所有员工的信息。每位员工都有姓名、地址和电话号码，因此存储这些值的变量在 `StaffMember` 类中被声明，并被所有后代继承。

![](img/7f8e069c1898b741edc17dfeed34b0c1_517_0.png)

视频笔记
探索 `Firm` 程序。

![](img/7f8e069c1898b741edc17dfeed34b0c1_518_0.png)

> 10.1 员工的类层次结构

`StaffMember` 类包含一个 `toString` 方法来返回由 `StaffMember` 类管理的信息。它还包含一个抽象方法 `pay`，该方法不接受参数并返回 `double` 类型的值。在通用的 `StaffMember` 级别，为此方法提供定义是不恰当的。

# 列表 10.1

```java
********************************************************************************
// Firm.java      作者: Lewis/Lotus
//
// 展示通过继承实现多态。
********************************************************************************
public class Firm {
    //-- 为公司创建一个员工团队并向他们支付工资。
    //--
    public static void main(String[] args) {
        Staff personnel = new Staff();
        personnel.payday();
    }
}
```

| 名称 | 地址 | 电话 | 安全号码 |
| :--- | :--- | :--- | :--- |
| Sam | 123 Main Line | 555-0469 | 123-45-6789 |
| Carla | 456 Off Line | 555-0101 | 987-45-4321 |
| Woody | 789 Off Rocker | 555-0000 | 010-20-340 |
| Diane | 678 Fifth Ave. | 555-0690 | 958-47-3625 |
| Norm | 987 Suds Blvd. | 555-8374 | |
| Cliff | 321 Duds Lane | 555-7282 | |

# 列表 10.2

```java
****************************************************
// Staff.java         作者: Lewis/Lotusus
// 代表特定业务的员工。
****************************************************
public class Staff {
    private StaffMember[] stafflist;
    // 构造函数：设置员工列表。
    public Staff () {
        staffList = new StaffMember[6];
        staffList[0] = new Executive("Sam", "123 Main Line", "555-0469", 123-45-6789);
        staffList[1] = new Employee("Carla", "456 Off Line", "555-0101", 987-45-4321);
        staffList[2] = new Employee("Woody", "789 Off Rocker", "555-0000", 010-20-340);
        staffList[3] = new Hourly("Diane", "678 Fifth Ave.", "555-0690", 958-47-3625);
        staffList[4] = new Volunteer("Norm", "987 Suds Blvd.", "555-8374");
        staffList[5] = new Volunteer("Cliff", "321 Duds Lane", "555-7282");
    }
    // 向所有员工支付工资。
    //---
    public void payday()
    {
        double amount;
        for (int count=0; count < staffList.length; count++) {
            System.out.println(staffList[count]);
        }
        amount = staffList[count].pay(); // 多态
        if (amount == 0.0) {
            System.out.println("Thanks!");
        } else {
            System.out.println("Paid: " + amount);
        }
        System.out.println("------------------------------------------------------------");
    }
}
```

## 10.2 通过继承实现多态

495

# 列表 10.3

```java
********************************************************************
// StaffMember.java      Author: Lewis/Loftus
// Represents a generic staff member.
********************************************************************
abstract public class StaffMember {
    protected String name;
    protected String address;
    protected String phone;
    ----------------------------------------------------
    // Constructor: Sets up this staff member using the specified
    // information.
    ----------------------------------------------------
    public StaffMember(String eName, String eAddress, String ePhone) {
        name = eName;
        address = eAddress;
        phone = ePhone;
    }
    ----------------------------------------------------
    // Returns a string including the basic employee information.
    ----------------------------------------------------
    public String toString() {
        String result = "Name: " + name + "\n";
        result += "Address: " + address + "\n";
        result += "Phone: " + phone;
        return result;
    }
    ----------------------------------------------------
    // Derived classes must define the pay method for each type of
    // employee.
    ----------------------------------------------------
    public abstract double pay();
}
```

然而，`StaffMember` 的每个子类都提供了自己特定的 `pay` 方法定义。通过在 `StaffMember` 中将 `pay` 定义为抽象，`Staff` 的 `payday` 方法就可以多态地支付每位员工工资。

这就是多态的精髓。每个类都最了解自己如何处理特定的行为，在本例中就是支付员工工资。然而，在某种意义上，它们都是同一种行为——员工获得工资。多态允许我们以一致但又独特的方式处理相似的对象。

列表 10.4 中的 `Volunteer` 类代表一个不因工作获得金钱报酬的人。我们只记录志愿者的基本信息，这些信息被传递给 `Volunteer` 的构造函数，构造函数通过 `super` 引用将其传递给 `StaffMember` 构造函数。`Volunteer` 的 `pay` 方法返回零工资值。如果 `pay` 没有

```java
********************************************************************************
// Volunteer.java               Author: Lewis/Loftus
// Represents a staff member that works as a volunteer.
********************************************************************************
public class Volunteer extends StaffMember
{
    //--------------------------------------------------------------------
    // Constructor: Sets up this volunteer using the specified
    // information.
    //--------------------------------------------------------------------
    public Volunteer (String eName, String eAddress, String ePhone)
    {
        super(eName, eAddress, ePhone);
    }
    //--------------------------------------------------------------------
    // Returns a zero pay value for this volunteer.
    //--------------------------------------------------------------------
    public double pay()
    {
        return 0.0;
    }
}
```

10.2 通过继承实现多态 497

被重写，否则 `Volunteer` 类将被视为抽象类且无法实例化。

请注意，当志愿者在 `Staff` 的 `payday` 方法中获得“工资”时，会打印一个简单的感谢表达式。在所有其他工资值大于零的情况下，会打印支付金额本身。

`Employee` 的 `toString` 方法被重写，以将 `Employee` 管理的额外信息连接到父类版本 `toString` 返回的信息中，该版本是通过 `super` 引用调用的。`Employee` 的 `pay` 方法简单返回该员工的工资率。

列表 10.6 所示的 `Executive` 类代表一个除了正常工资率外可能获得奖金的员工。`Executive` 类派自 `Employee`，因此同时继承了 `StaffMember` 和 `Employee`。`Executive` 的构造函数将所有信息传递给 `Employee` 构造函数，并将高管奖金设置为零。

使用 `awardBonus` 方法为高管发放奖金。该方法在 `Staff` 构造函数中被调用，用于员工数组中唯一的执行官。请注意，必须将通用的 `StaffMember` 引用强制转换为 `Executive` 引用才能调用 `awardBonus` 方法（该方法在 `StaffMember` 中不存在）。

`Executive` 类重写了 `pay` 方法，使其首先确定像任何员工一样的支付金额，然后加上奖金。使用 `super` 调用 `Employee` 类的 `pay` 方法以获取 `payRate` 变量，如果我们更改 `Employee` 对象的支付方式，该更改将自动反映在 `Executive` 中。奖金发放后，它会被重置为零。

列表 10.7 所示的 `Hourly` 类代表一个按小时计算工资率的员工。它记录当前薪资期间的工作小时数，这可以通过调用 `addHours` 方法进行修改。该方法从 `Staff` 的 `payday` 方法调用。`Hourly` 的 `pay` 方法根据工作小时数确定支付金额并将小时数重置为零。

# 列表 10.5

```java
************************************************************************************
// Employee.java               Author: Lewis/Loftus
//
// Represents a general paid employee.
************************************************************************************
public class Employee extends StaffMember
{
    protected String socialSecurityNumber;
    protected double payRate;
    // Constructor: Sets up this employee with the specified
    // information.
```
