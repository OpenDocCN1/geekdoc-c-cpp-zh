

并非每个类关系都是继承关系。在第 8 章中，我们讨论了 has-a 关系，其中类拥有对其他类对象的引用作为成员。这种关系通过现有类的组合创建类。例如，给定类 Employee、BirthDate 和 TelephoneNumber，说一个 Employee 是一个 BirthDate 或一个 Employee 是一个 TelephoneNumber 是不合适的。然而，一个 Employee 有一个 BirthDate，并且一个 Employee 有一个 TelephoneNumber。

可以对超类对象和子类对象进行类似的处理——它们的共同点在超类的成员中表达。扩展同一超类的所有类的对象都可以被视为该超类的对象——此类对象与超类具有 is-a 关系。在本章后面以及第 10 章中，我们将考虑许多利用 is-a 关系的例子。

子类可以自定义从其超类继承的方法。为此，子类会覆盖（重新定义）超类方法并提供适当的实现，正如我们在本章的代码示例中经常看到的那样。

## 9.3 protected 成员

第 8 章讨论了访问修饰符 public 和 private。一个类的 public 成员只要程序拥有该类或其子类的对象的引用，就可以在任何地方访问。一个类的 private 成员只能在类本身内部访问。在本节中，我们介绍访问修饰符 protected。使用 protected 访问提供了介于 public 和 private 之间的中间访问级别。超类的 protected 成员可以被该超类的成员、其子类的成员以及同一包中的其他类的成员访问——protected 成员也具有包访问权限。

所有 public 和 protected 超类成员在成为子类成员时仍保留其原始访问修饰符——超类的 public 成员成为子类的 public 成员，超类的 protected 成员成为子类的 protected 成员。超类的 private 成员在类本身之外不可访问。相反，它们在其子类中被隐藏，只能通过从超类继承的 public 或 protected 方法访问。

子类方法可以通过简单地使用成员名称来引用从超类继承的 public 和 protected 成员。当子类方法覆盖继承的超类方法时，可以通过在超类方法名前加上关键字 super 和点（.）分隔符从子类访问超类方法。我们将在第 9.4 节讨论访问超类的被覆盖成员。

> 软件工程观察 9.1
> 子类的 方法不能直接访问其超类的 private 成员。子类只能通过超类中提供的非 private 方法并被子类继承来更改 private 超类实例变量的状态。

> 软件工程观察 9.2
> 声明 private 实例变量有助于您测试、调试和正确修改系统。如果子类可以访问其超类的 private 实例变量，则继承自该子类的类也可以访问这些实例变量。这将传播本应为 private 的实例变量的访问权限，信息隐藏的好处将丧失。

## 9.4 超类与子类之间的关系

我们现在使用公司工资应用程序中员工类型的继承层次结构来讨论超类与其子类之间的关系。在这家公司中，佣金员工（将由超类的对象表示）按其销售额的百分比获得报酬，而底薪加佣金员工（将由子类的对象表示）获得底薪加上其销售额的百分比。

我们将这些类之间关系的讨论分为五个示例。第一个声明类 CommissionEmployee，它直接继承自类 Object 并声明为 private 的实例变量 first name、last name、社会安全号码、佣金率和毛销售额。

第二个示例声明类 BasePlusCommissionEmployee，它也直接继承自类 Object 并声明为 private 的实例变量 first name、last name、社会安全号码、佣金率、毛销售额和基本工资。我们通过编写类所需代码的每一行来创建这个类——我们很快就会看到，通过继承自类 CommissionEmployee 来创建它要高效得多。

第三个示例声明一个新的 BasePlusCommissionEmployee 类，该类扩展类 CommissionEmployee（即 BasePlusCommissionEmployee 是一个 CommissionEmployee，同时还具有基本工资）。这种软件重用使我们在开发新子类时可以编写更少的代码。在此示例中，类 BasePlusCommissionEmployee 尝试访问类 CommissionEmployee 的 private 成员——这会导致编译错误，因为子类无法访问超类的 private 实例变量。

第四个示例表明，如果 CommissionEmployee 的实例变量声明为 protected，则 BasePlusCommissionEmployee 子类可以直接访问该数据。两个 BasePlusCommissionEmployee 类包含相同的功能，但我们展示了继承版本更容易创建和管理。

在讨论使用 protected 实例变量的便利性之后，我们创建第五个示例，将 CommissionEmployee 实例变量重新设置为 private 以强制执行良好的软件工程。然后我们展示 BasePlusCommissionEmployee 子类如何使用 CommissionEmployee 的 public 方法以受控的方式操作从 CommissionEmployee 继承的 private 实例变量。

### 9.4.1 创建和使用 CommissionEmployee 类

我们首先声明类 CommissionEmployee（图 9.4）。第 4 行开始类声明并指出类 CommissionEmployee extends（即继承自）类 Object（来自包 java.lang）。这导致类 CommissionEmployee 继承类 Object 的方法——类 Object 没有任何字段。如果您没有显式指定新类扩展哪个类，则该类隐式扩展 Object。因此，您通常不会在代码中包含“extends Object”——我们仅在此示例中出于演示目的这样做。

### 类 CommissionEmployee 的方法和实例变量概述

类 CommissionEmployee 的 public 服务包括构造函数（第 13–22 行）以及方法 earnings（第 93–96 行）和 toString（第 99–107 行）。第 25–90 行声明了类实例变量（在第 6–10 行声明）的 public get 和 set 方法 firstName、lastName、socialSecurityNumber、grossSales 和 commissionRate。类将实例变量声明为 private，因此其他类的对象不能直接访问

这些变量。将实例变量声明为 private 并提供 get 和 set 方法来操作和验证它们有助于强制执行良好的软件工程。例如，方法 setGrossSales 和 setCommissionRate 在将值赋给实例变量 grossSales 和 commissionRate 之前会验证其参数。在真实的、业务关键的应用程序中，我们也会在类的其他 set 方法中执行验证。

// Fig. 9.4: CommissionEmployee.java
// CommissionEmployee class represents an employee paid a
// percentage of gross sales.
public class CommissionEmployee extends Object
{
    private String firstName;
    private String lastName;
    private String socialSecurityNumber;
    private double grossSales; // gross weekly sales
    private double commissionRate; // commission percentage

    // five-argument constructor
    public CommissionEmployee( String first, String last, String ssn,
        double sales, double rate )
    {
        // implicit call to Object constructor occurs here
        firstName = first;
        lastName = last;
        socialSecurityNumber = ssn;
        setGrossSales( sales ); // validate and store gross sales
        setCommissionRate( rate ); // validate and store commission rate
    } // end five-argument CommissionEmployee constructor

    // set first name
    public void setFirstName( String first )
    {
        firstName = first; // should validate
    } // end method setFirstName

    // return first name
    public String getFirstName()
    {
        return firstName;
    } // end method getFirstName

    // set last name
    public void setLastName( String last )
    {
        lastName = last; // should validate
    } // end method setLastName

    // return last name
    public String getLastName()
    {
```

Fig. 9.4 | CommissionEmployee class represents an employee paid a percentage of gross sales. (Part 1 of 3.)

