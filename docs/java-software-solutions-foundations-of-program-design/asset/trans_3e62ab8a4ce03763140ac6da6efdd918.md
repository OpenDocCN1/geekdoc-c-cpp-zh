

## 自测问题（答案见附录 N）

- SR 10.1 什么是多态？
- SR 10.2 为什么编译时绑定被认为比动态绑定更高效？

## 10.2 通过继承实现的多态

当我们使用特定类名声明一个引用变量时，它可以用来引用该类的任何对象。此外，它还可以引用通过继承与其声明类型相关的任何类的任何对象。例如，如果类 `Mammal` 是类 `Horse` 的父类，那么 `Mammal` 引用可以用来引用类 `Horse` 的任何对象。这种能力在以下代码段中展示：

```
Mammal pet;
Horse secretariat = new Horse();
pet = secretariat; // a valid assignment
```

反向操作，即将 `Mammal` 对象赋值给 `Horse` 引用，也是可行的，但需要显式转换。按此方向赋值通常用处不大，且更可能引发问题，因为尽管马具有哺乳动物的全部功能（因为马是一种哺乳动物），但反过来并不一定成立。

这种关系在整个类层次结构中有效。如果 `Mammal` 类派生自一个名为 `Animal` 的类，那么以下赋值也是有效的：

```
Animal creature = new Horse();
```

更进一步，`Object` 引用可以用来引用任何对象，因为最终所有类都是 `Object` 类的后代。例如，`ArrayList` 利用多态性，它被设计为保存 `Object` 引用。这就是为什么未指定元素类型的 `ArrayList` 可以用来存储任何种类的对象。实际上，一个特定的 `ArrayList` 可以在同一时间保存多种不同类型的对象，因为通过继承，它们都是 `Object` 对象。

引用变量 `creature` 可以是多态的，因为在任何时刻它都可以引用 `Animal` 对象、`Mammal` 对象或 `Horse` 对象。假设这三个类都有一个名为 `move` 的方法，并且以不同的方式实现（因为

关键概念
一个引用变量可以引用由继承相关的任何类创建的任何对象。

关键概念
对象的类型，而不是引用的类型，用于决定调用哪个版本的方法。

子类覆盖了它继承的定义）。下面的调用调用了 `move` 方法，但它调用的方法的特定版本是在运行时确定的：

```
creature.move();
```

当这行代码执行时，如果 `creature` 当前引用的是 `Animal` 对象，则会调用 `Animal` 类的 `move` 方法。同样，如果 `creature` 当前引用的是 `Mammal` 对象，则会调用 `Mammal` 版本的 `move`。如果它当前引用的是 `Horse` 对象，也是如此。

当然，由于 `Animal` 和 `Mammal` 表示一般概念，它们可以被定义为抽象类。这种情况并不会消除拥有多态引用的能力。假设 `Mammal` 类中的 `move` 方法是抽象的，并在 `Horse`、`Dog` 和 `Whale` 类（均派生自 `Mammal`）中给出了独特定义。`Mammal` 引用变量可以用来引用从 `Horse`、`Dog` 和 `Whale` 类中任何一个创建的任何对象，并且可以对它们中的任何一个执行 `move` 方法。

让我们看另一种情况。考虑图 10.1 中所示的类层次结构。其中的类代表某家公司可能雇佣的各种类型的员工。让我们探索一个使用该层次结构来支付一组不同类型员工工资的示例。

清单 10.1 中所示的 `Firm` 类包含一个 `main` 驱动程序，它创建一组员工（`Staff`）并调用 `payday` 方法来支付他们所有人的工资。程序输出包括每位员工的信息以及每位员工获得的工资金额（如果有的话）。

清单 10.2 中所示的 `Staff` 类维护一个对象数组，这些对象代表各种类型的员工个体。请注意，该数组被声明为保存 `StaffMember` 引用，但实际填充的是从其他几个类（如 `Executive` 和 `Employee`）创建的对象。这些类都是 `StaffMember` 类的后代，因此这些赋值是有效的。`staffList` 数组填充了多态引用。

`Staff` 类的 `payday` 方法扫描员工列表，打印他们的信息并调用他们的 `pay` 方法，以确定每位员工应获得多少工资。`pay` 方法的调用是多态的，因为每个类都有自己的 `pay` 方法版本。

清单 10.3 中所示的 `StaffMember` 类是抽象的。它不代表特定类型的员工，也不打算被实例化。相反，它充当所有员工类的祖先，并包含适用于所有员工的信息。每位员工都有姓名、地址和电话号码，因此用于存储这些值的变量在 `StaffMember` 类中声明，并由所有后代继承。

视频注释
探索 Firm 程序。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_518_0.png)

`StaffMember` 类包含一个 `toString` 方法，用于返回 `StaffMember` 类管理的信息。它还包含一个名为 `pay` 的抽象方法，该方法不带参数并返回 `double` 类型的值。在通用的 `StaffMember` 级别，给这个方法提供定义是不合适的。

## 清单 10.1

```
//************************************************************************
// Firm.java          Author: Lewis/Loftus
//
// Demonstrates polymorphism via inheritance.
//************************************************************************

public class Firm
{
    //-------------------------------------------------------------
    // Creates a staff of employees for a firm and pays them.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        Staff personnel = new Staff();

        personnel.payday();
    }
}
```

### 输出

Name: Sam
Address: 123 Main Line
Phone: 555-0469
Social Security Number: 123-45-6789
Paid: 2923.07
--------------------------------------------------
Name: Carla
Address: 456 Off Line
Phone: 555-0101
Social Security Number: 987-65-4321
Paid: 1246.15
--------------------------------------------------
Name: Woody
Address: 789 Off Rocker
Phone: 555-0000
Social Security Number: 010-20-3040
Paid: 1169.23
--------------------------------------------------
Name: Diane
Address: 678 Fifth Ave.
Phone: 555-0690
Social Security Number: 958-47-3625
Current hours: 40
Paid: 422.0
----------------------------------------
Name: Norm
Address: 987 Suds Blvd.
Phone: 555-8374
Thanks!
----------------------------------------
Name: Cliff
Address: 321 Duds Lane
Phone: 555-7282
Thanks!
----------------------------------------

## 清单 10.1（续）

```
Social Security Number: 958-47-3625
Current hours: 40
Paid: 422.0
----------------------------------------
Name: Norm
Address: 987 Suds Blvd.
Phone: 555-8374
Thanks!
----------------------------------------
Name: Cliff
Address: 321 Duds Lane
Phone: 555-7282
Thanks!
----------------------------------------
```

## 清单 10.2

```
//****************************************************************
// Staff.java      Author: Lewis/Loftus
//
// Represents the personnel staff of a particular business.
//****************************************************************

public class Staff
{
    private StaffMember[] staffList;

    //-------------------------------------------------------------
    // Constructor: Sets up the list of staff members.
    //-------------------------------------------------------------
    public Staff ()
    {
        staffList = new StaffMember[6];

        staffList[0] = new Executive ("Sam", "123 Main Line",
            "555-0469", "123-45-6789", 2423.07);
```

## 清单 10.2（续）

```
staffList[1] = new Employee ("Carla", "456 Off Line", "555-0101", "987-65-4321", 1246.15);
staffList[2] = new Employee ("Woody", "789 Off Rocker", "555-0000", "010-20-3040", 1169.23);

staffList[3] = new Hourly ("Diane", "678 Fifth Ave.", "555-0690", "958-47-3625", 10.55);

staffList[4] = new Volunteer ("Norm", "987 Suds Blvd.", "555-8374");
staffList[5] = new Volunteer ("Cliff", "321 Duds Lane", "555-7282");

((Executive)staffList[0]).awardBonus (500.00);

((Hourly)staffList[3]).addHours (40);
}

//--------------------------------------------------
// Pays all staff members.
//--------------------------------------------------
public void payday ()
{
    double amount;

    for (int count=0; count < staffList.length; count++)
    {
        System.out.println (staffList[count]);

        amount = staffList[count].pay(); // polymorphic

        if (amount == 0.0)
            System.out.println ("Thanks!");
        else
            System.out.println ("Paid: " + amount);

        System.out.println ("--------------------------------");
    }
}
```

