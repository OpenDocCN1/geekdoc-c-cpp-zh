
**图 11-2** 使用图 11-1 中的类声明 `Employee` 对象的程序

![](img/a793a0aa5ac4813ed7fc54d92636efcd_485_0.png)

**图 11-3** 图 11-2 中程序的输出

图 11-1 中的 `Employee` 类在构造时将 `Employee` 的小时工资设置为 `10.00`，但该类还包含一个 `setHourlyWage()` 方法，应用程序以后可以使用它可以更改初始的 `hourlyWage` 值。编写 `Employee` 类构造函数的另一种更优方法如图 11-4 所示。在构造函数的这个版本中，一个值为 `10.00` 的命名常量被传递给 `setHourlyWage()`。使用这种技术有几个优点：

- 构造函数中不再需要 `calculateWeeklyPay()` 语句，因为构造函数调用了 `setHourlyWage()`，而后者调用了 `calculateWeeklyPay()`。
- 未来，如果需要对小时工资实施限制，则需要在一处修改代码。例如，如果修改 `setHourlyWage()` 以不允许过高或过低的费率，代码将在 `setHourlyWage()` 方法中更改，而不需要在构造函数中修改。这减少了所需的工作量并减少了错误的可能性。

```java
public Employee()
  Declarations
    num DEFAULT_WAGE = 10.00
  setHourlyWage(DEFAULT_WAGE)
return
```

**图 11-4** `Employee` 类构造函数的另一种版本

### 理解构造函数

当然，在初始化时需要不同的 `hourlyWage` 要求，在构造后设置值时也需要，因此构造函数中编写的代码语句与 `setHourlyWage()` 方法中的语句不同。

### 非默认构造函数

你可以编写非默认构造函数，即接受参数的构造函数。当你创建一个构造函数时，无论是默认还是非默认，自动提供的构造函数将不再可访问。

例如，与其强制每个 `Employee` 都用相同的初始值进行构造，你可能选择通过向构造函数传递一个数值来创建具有唯一 `hourlyWage` 的 `Employee` 对象。图 11-5 显示了 `Employee` 构造函数如何接收参数。使用此构造函数时，使用类似于以下任一的声明传递参数：

- `Employee(8.81)`
- `Employee partTimeWorker(valueEnteredByUser)`

当调用构造函数时，构造函数调用中的数值被传递给 `Employee()`，其中参数 `rate` 接收参数的值。该值在构造函数内部赋值给 `hourlyWage`。

```java
public Employee(num rate)
    hourlyWage = rate
    calculateWeeklyPay()
    return
```

图 11-5 `Employee` 构造函数接受该参数

如果你按照图 11-5 所示创建一个带有构造函数的 `Employee` 类，并且它是类中唯一的构造函数，那么你创建的每个 `Employee` 对象都必须在它的声明中使用数值参数。换句话说，该类的此新版本包含单个非默认构造函数，以下声明有效：

`Employee partTimeWorker`

## 方法和构造函数的重载

在第 9 章中，你学习了如何通过编写多个具有同名但不同参数列表的方法版本来重载构造函数。同样地，你也可以重载实例方法和构造函数。例如，图 11-6 显示了包含两个构造函数的 `Employee` 类版本。记住，方法的签名是它的名称和参数类型列表。图 11-6 中的构造函数具有不同的签名——一个版本不需要参数，另一个版本需要一个数值参数。换句话说，该类的版本包含了默认构造函数和非默认构造函数。

```java
class Employee
    Declarations
    private string lastName
    private num hourlyWage
    private num weeklyPay
    public Employee()
        hourlyWage = 10.00
        calculateWeeklyPay()
    return
    public Employee(num rate)
        hourlyWage = rate
        calculateWeeklyPay()
    return
    public void setName(string name)
        lastName = name
    return
    public void setHourlyWage(num wage)
        hourlyWage = wage
        calculateWeeklyPay()
    return
    public string getLastName()
        return lastName
    public num getHourlyWage()
        return hourlyWage()
    public num getWeeklyPay()
        return weeklyPay
    private void calculateWeeklyPay()
        Declarations
        num WORK_WEEK_HOURS = 40
        weeklyPay = hourlyWage * WORK_WEEK_HOURS
    return
endClass
```

![](img/a793a0aa5ac4813ed7fc54d92636efcd_487_0.png)

**图 11-6** 具有载构造函数的 `Employee` 类

当你使用 11-6 所示的类时，可以执行如下语句：

`Employee deliveryPerson`
`Employee myButler(25.85)`

### 理解构造函数

当你使用第一个语句声明 `Employee` 时，会自动设置 `10.00` 的工资，因为该语句使用了无参数构造函数。当你使用第二个语句声明 `Employee` 时，`hourlyWage` 被设置为传递的值。类中的任何方法或构造函数都可以重载，只要每个版本都有唯一的签名。例如，你可以像图 11-7 所示为 `Employee` 类添加第三个构造函数。此版本可以与其他两个版本共存，因为其参数列表与现有版本都不同。通过此版本，你可以指定 `Employee` 的小时率以及名称。如果应用程序执行类似下面的语句，则将执行此双参数版本：

`Employee myid(22.50, "Parker")`

```java
public Employee(num rate, string name)
lastName = name
hourlyWage = rate
calculateWeeklyPay()
```

图 11-7 第三个 `Employee` 类构造函数

你可能会创建一个具有多个构造版本的 `Employee` 类，为客户端程序提供灵活性。例如，特定的客户端程序可能使用一个版本，而另一个客户端可能使用另一个。

观看视频 `Constructors`。

## 两个真相和一个谎言

### 理解构造函数

+ 1. 构造函数是建立对象的方法。
2. 默认构造函数被定义为自动创建的构造函数。
3. 根据编程语言，默认构造函数可能会为对象的数据字段提供初始值。

所有默认构造函数都是自动创建的。
类的默认构造函数是默认构造函数。
谎言是 #2。默认构造函数不接受参数。

### 理解析构函数

析构函数包含了类实例在销毁时所需的操作。通常情况下，类实例会在对象超出作用域时销毁。与构造函数一样，如果你没有为类显式创建析构函数，系统会自动提供一个。

声明析构函数最常见的方法是显式使用由波浪号（~）和类名组成的标识符。你不能为析构函数提供参数；它必须有一个空的参数列表。因此，析构函数不能重载；一个类最多只有一个析构函数。与构造函数一样，析构函数没有返回值。

> 创建和命名析构函数的规则在不同的编程语言中不同。例如，在 Visual Basic 类中，析构函数被称为 `Finalize`。

图 11-8 显示了一个 `Employee` 类，它只包含一个字段 (`idNumber`)、一个构造函数和一个阴影析构函数。虽然构造函数或析构函数输出任何内容并不常见，但这种设计让你在创建和销毁对象时看到这些消息。当你执行图 11-9 中的程序时，你实例化两个 `Employee` 对象，每个对象都有自己的 `idNumber` 值。当程序结束时，两个 `Employee` 对象超出了作用域，每个对象的析构函数会被自动调用。图 11-10 显示：

```java
class Employee
    Declarations
    private string idNumber
    public Employee(string empID)
        idNumber = empID
        output "Employee " + idNumber + " is created"
        return
    public ~Employee()
        output "Employee " + idNumber + " is destroyed"
        return
endClass
```

图 11-8 带有析构函数的 `Employee` 类

```java
start
  Declarations
    EmployeeWorker("101")
    Employee anotherWorker("202")
stop
```

**图 11-9** 声明两个 `Employee` 对象的程序

![](img/a793a0aa5ac4813ed7fc54d92636efcd_490_0.png)

**图 11-10** 图 11-9 中程序的输出

图 11-9 中的程序显式调用了 `Employee` 类的析构函数，但从输出中可以看到析构函数执行了两次。你通常不会显式地调用它，尽管在某些语言中可以这样做。有趣的是，你从图 11-10 的输出中可以看到最后创建的对象是第一个销毁的对象；无论程序实例化了多少对象或对象是否同时超出作用域，这种关系都成立。

> 当类实例不再被任何代码使用时，它就符合销毁条件——也就是说当它超出作用域时。在许多语言中，对象析构函数的实际执行可能发生在对象符合销毁条件后的任何时间。

现在，你几乎没有理由创建一个析构函数来演示它是如何被自动调用的。以后，当你编写处理文件、数据库或大量计算机内存的复杂程序时，你可能希望在对象超出作用域时执行特定的清理或关闭任务。你会在析构函数放置适当的指令。

# 两个真话一个假言

理解析构函数

- 与构造函数不同，如果你想为类创建一个析构函数，必须显式创建。
- 你不能为析构函数提供参数；它必须有一个空的参数列表。
- 析构函数不能重载；一个类最多只有一个析构函数。

> 错误的陈述是 #1。与构造函数一样，你不需要显式地创建一个，它是自动创建的。

### 理解组合

类可以包含另一个类的对象作为数据字段。例如，你可能会创建一个名为 `Date` 的类，其中包含月、日、年，并在 `Employee` 类中添加两个 `Date` 字段来存储员工的出生日期和入职日期。你可能会创建一个名为 `Department` 的类来代表公司中的每个部门，并创建 `Department` 类来包含一个主管（主管是一个 `Employee`）。图 11-11 包含了这些关系的图。当一个类包含另一个类的对象时，这种关系被称为整体-部分关系或组合。这种创建的关系也被称为“拥有”（has-a）关系，因为一个类“拥有”另一个类的实例。

![](img/a793a0aa5ac4813ed7fc54d92636efcd_491_0.png)

图 11-11 典型关系图

### 理解继承

当类实例不再被任何代码使用时，它就符合销毁条件——也就是说当它超出作用域时。在许多语言中，对象析构函数的实际执行可能发生在对象符合销毁条件后的任何时间。

现在，你几乎没有理由创建一个析构函数来演示它是如何被自动调用的。以后，当你编写处理文件、数据库或大量计算机内存的复杂程序时，你可能希望在对象超出作用域时执行特定的清理或关闭任务。你会在析构函数放置适当的指令。

# 两个真话一个假言

理解组合

- 1. 类可以包含另一个类的对象作为数据字段。
- 2. 当你使用对象作为字段时就会发生组合。
- 3. 组合被称为“是”（is-a）关系，因为一个类“是另一个类的实例”。

> 错误的陈述是 #3。组合被称为“拥有”（has-a）关系。

### 理解继承

理解类有助于你组织对象。继承帮助你更精确地组织它们。当你使用继承一术语时，可能会想到遗传继承。你可能会根据继承的属性来选择植物和动物。

### 理解继承

`Employee`
- `empNum` : `string`
- `weeklySalary` : `num`

```
+setEmpNum(number : string) : void
+getEmpNum() : string
+setWeeklySalary(salary : num) : void
+getWeeklySalary() : num
```

![](img/a793a0aa5ac4813ed7fc54d92636efcd_494_0.png)

`CommissionEmployee`
- `commissionRate` : `num`

```
+setCommissionRate(rate : num) : void
+getCommissionRate() : num
```

图 11-13 `CommissionEmployee` 继承自 `Employee`

![](img/a793a0aa5ac4813ed7fc54d92636efcd_494_1.png)

记住，类图中的加号表示公共访问，减号表示私有访问。图 11-13 以及本章中的其他几图都是 UML 图的示例。第 13 章将更详细地描述 UML。

```java
class CommissionEmployee inheritsFrom Employee
Declarations
  private num commissionRate
public void setCommissionRate(num rate)
  commissionRate = rate
  return
public num getCommissionRate()
  return commissionRate
endClass
```
