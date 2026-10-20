

```java
        super( first, last, ssn ); // pass to Employee constructor
        setWeeklySalary( salary ); // validate and store salary
    } // end four-argument SalariedEmployee constructor

    // set salary
    public void setWeeklySalary( double salary )
    {
        if ( salary >= 0.0 )
            weeklySalary = salary;
        else
            throw new IllegalArgumentException(
                "Weekly salary must be >= 0.0" );
    } // end method setWeeklySalary

    // return salary
    public double getWeeklySalary()
    {
        return weeklySalary;
    } // end method getWeeklySalary

    // calculate earnings; implement interface Payable method that was
    // abstract in superclass Employee
    @Override
    public double getPaymentAmount()
    {
        return getWeeklySalary();
    } // end method getPaymentAmount

    // return String representation of SalariedEmployee object
    @Override
    public String toString()
    {
        return String.format( "salaried employee: %s\n%s: $%,.2f",
            super.toString(), "weekly salary", getWeeklySalary() );
    } // end method toString
} // end class SalariedEmployee
```

**Fig. 10.14** | 实现接口 Payable 方法 getPaymentAmount 的 SalariedEmployee 类。

## 10.7.6 使用接口 Payable 以多态方式处理发票和员工

PayableInterfaceTest（图 10.15）说明了接口 Payable 可用于在单个应用程序中以多态方式处理一组 Invoice 和 Employee。 第 9 行声明 payableObjects 并将其赋值为四个 Payable 变量的数组。 第 12–13 行将 Invoice 对象的引用赋给 payableObjects 的前两个元素。 第 14–17 行随后将 SalariedEmployee 对象的引用赋给 payableObjects 的其余两个元素。 这些赋值是允许的，因为 Invoice 是一个 Payable，SalariedEmployee 是一个 Employee 而 Employee 是一个 Payable。 第 23–29 行使用增强 for 语句以多态方式处理 payableObjects 中的每个 Payable 对象，打印对象作为 String，以及应付的付款金额。 第 27 行通过 Payable 接口引用调用方法 `toString`，即使 `toString` 未在接口 Payable 中声明——所有引用（包括接口类型）都引用扩展 Object 的对象，因此具有 `toString` 方法。 （方法 `toString` 也可在此隐式调用。）第 28 行调用 Payable 方法 `getPaymentAmount` 以获取 `payableObjects` 中每个对象的付款金额，而不考虑对象的实际类型。 输出显示第 27–28 行中的方法调用会调用相应类的 `toString` 和 `getPaymentAmount` 方法的实现。 例如，当 `currentPayable` 在 `for` 循环的第一次迭代中引用一个 Invoice 时，类 Invoice 的 `toString` 和 `getPaymentAmount` 执行。

```java
// Fig. 10.15: PayableInterfaceTest.java
// Tests interface Payable.

public class PayableInterfaceTest
{
   public static void main( String[] args )
   {
      // create four-element Payable array
      Payable[] payableObjects = new Payable[ 4 ];

      // populate array with objects that implement Payable
      payableObjects[ 0 ] = new Invoice( "01234", "seat", 2, 375.00 );
      payableObjects[ 1 ] = new Invoice( "56789", "tire", 4, 79.95 );
      payableObjects[ 2 ] =
         new SalariedEmployee( "John", "Smith", "111-11-1111", 800.00 );
      payableObjects[ 3 ] =
         new SalariedEmployee( "Lisa", "Barnes", "888-88-8888", 1200.00 );

      System.out.println(
         "Invoices and Employees processed polymorphically:\n" );

      // generically process each element in array payableObjects
      for ( Payable currentPayable : payableObjects )
      {
         // output currentPayable and its appropriate payment amount
         System.out.printf( "%s %n%s: $%,.2f\n\n",
            currentPayable.toString(),
            "payment due", currentPayable.getPaymentAmount() );
      } // end for
   } // end main
} // end class PayableInterfaceTest
```

```text
Invoices and Employees processed polymorphically:

invoice:
part number: 01234 (seat)
quantity: 2
price per item: $375.00
payment due: $750.00

invoice:
part number: 56789 (tire)
quantity: 4
price per item: $79.95
payment due: $319.80

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: $800.00
payment due: $800.00

salaried employee: Lisa Barnes
social security number: 888-88-8888
weekly salary: $1,200.00
payment due: $1,200.00
```

**Fig. 10.15** | 以多态方式处理 Invoice 和 Employee 的 Payable 接口测试程序。

## 10.7.7 Java API 的常见接口

在本节中，我们概述了 Java API 中找到的几个常见接口。 接口的强大功能和灵活性在整个 Java API 中被频繁使用。 这些接口以与您创建的接口（例如第 10.7.2 节中的接口 Payable）相同的方式实现和使用。 Java API 的接口使您能够在 Java 提供的框架中使用自己的类，例如比较您自己的类型的对象并创建可以与同一程序中的其他任务并发执行的任务。 图 10.16 概述了我们在 *Java How to Program, Ninth Edition* 中使用的 Java API 的一些更受欢迎的接口。

| 接口 | 描述 |
| --- | --- |
| Comparable | Java 包含几个比较运算符（例如 <、<=、>、>=、==、!=），允许您比较原始值。 然而，这些运算符 *不能* 用于比较对象。 接口 Comparable 用于允许实现该接口的类的对象相互比较。 接口 Comparable 通常用于对集合中的对象进行排序，例如数组。 我们在第 20 章《通用集合》和第 21 章《通用类和方法》中使用 Comparable。 |
| Serializable | 一个用于标识其对象可以写入（即序列化）或从某种类型的存储（例如磁盘上的文件、数据库字段）读取（即反序列化）或跨网络传输的类的接口。 我们在第 17 章《文件、流和对象序列化》以及第 27 章《网络》中使用 Serializable。 |
| Runnable | 由任何希望该类的对象能够使用称为多线程的技术并行执行而实现的类实现（在第 26 章《多线程》中讨论）。 该接口包含一个方法 run，描述对象执行时的行为。 |
| GUI 事件监听器接口 | 您每天都会使用图形用户界面（GUI）。 在网络浏览器中，您可能会输入要访问的网站的地址，或者您可能会单击按钮返回到上一个站点。 浏览器响应您的交互并执行所需任务。 您的交互称为事件，浏览器用于响应事件的代码称为事件处理程序。 在第 14 章《GUI 组件：第一部分》和第 25 章《GUI 组件：第二部分》中，您将学习如何构建 GUI 和事件处理程序以响应用户交互。 事件处理程序在实现适当的事件监听器接口的类中声明。 每个事件监听器接口指定一个或多个必须实现的方法以响应用户交互。 |
| SwingConstants | 包含一组用于在屏幕上定位 GUI 元素而在 GUI 编程中使用的常量。 我们在第 14 章和第 25 章中探讨 GUI 编程。 |

**Fig. 10.16** | Java API 的常见接口。

## 10.8 （可选）GUI 和图形案例研究：使用多态进行绘图

您可能已经注意到在 GUI 和图形案例研究练习 8.1 中创建的绘图程序（并在 GUI 和图形案例研究练习 9.1 中修改）中，形状类有很多相似之处。 使用继承，我们可以从所有三个类中“提取”公共特征并将它们放在单个形状超类中。 然后，使用超类类型的变量，我们可以以多态方式操作形状对象。 删除冗余代码将导致更小、更灵活、更易于维护的程序。

### GUI 和图形案例研究练习

10.1 修改 GUI 和图形案例研究练习 8.1 和练习 9.1 的 MyLine、MyOval 和 MyRectangle 类以创建图 10.17 中的类层次结构。 MyShape 层次结构的类应该是“智能”形状类，知道如何绘制自己（如果提供 Graphics 对象告诉它们在哪里绘制）。 一旦程序从此层次结构创建对象，它就可以将其余生命周期作为 MyShape 以多态方式操作它。

在您的解决方案中，图 10.17 中的类 MyShape 必须是抽象的。 由于 MyShape 代表一般形状，因此在不知道它确切是什么形状的情况下无法实现 draw 方法。 层次结构中形状的坐标和颜色表示应声明为类 MyShape 的私有成员。 除了公共数据外，类 MyShape 还应声明以下方法：

- a) 一个无参数构造函数，将形状的所有坐标设置为 0 并将颜色设置为 Color.BLACK。
- b) 一个构造函数，将坐标和颜色初始化为所提供参数的值。
- c) 用于各个坐标和颜色的设置方法，允许程序员独立为层次结构中的形状设置任何数据项。
- d) 用于各个坐标和颜色的获取方法，允许程序员独立检索层次结构中形状的任何数据项。

