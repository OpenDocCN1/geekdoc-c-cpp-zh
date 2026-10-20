

## 软件工程观察 9.3

使用继承时，层次结构中所有类的公共实例变量和方法都在超类中声明。当对超类中的这些公共特性进行更改时——子类就会继承这些更改。如果没有继承，就需要在包含所讨论代码副本的所有源代码文件中进行更改。

## 9.4.3 创建 CommissionEmployee-BasePlusCommissionEmployee 继承层次结构

现在我们重新声明类 BasePlusCommissionEmployee（图 9.8）以扩展类 CommissionEmployee（图 9.4）。BasePlusCommissionEmployee 对象是一个 CommissionEmployee，因为继承传递了类 CommissionEmployee 的能力。类 BasePlusCommissionEmployee 还具有实例变量 baseSalary（图 9.8，第 6 行）。关键字 extends（第 4 行）表示继承。BasePlusCommissionEmployee 继承了 CommissionEmployee 的实例变量和方法，但只有超类的 public 和 protected 成员可以在子类中直接访问。CommissionEmployee 构造函数未被继承。因此，公共 BasePlusCommissionEmployee 服务包括其构造函数（第 9–16 行）、从 CommissionEmployee 继承的公共方法，以及方法 setBaseSalary（第 19–26 行）、getBaseSalary（第 29–32 行）、earnings（第 35–40 行）和 toString（第 43–53 行）。方法 earnings 和 toString 覆盖了类 CommissionEmployee 中的对应方法，因为其超类版本无法正确计算 BasePlusCommissionEmployee 的收入或返回合适的 String 表示。

```
// Fig. 9.8: BasePlusCommissionEmployee.java
// private superclass members cannot be accessed in a subclass.
public class BasePlusCommissionEmployee extends CommissionEmployee
{
    private double baseSalary; // base salary per week

    // six-argument constructor
    public BasePlusCommissionEmployee( String first, String last,
        String ssn, double sales, double rate, double salary )
    {
        // explicit call to superclass CommissionEmployee constructor
        super( first, last, ssn, sales, rate );

        setBaseSalary( salary ); // validate and store base salary
    } // end six-argument BasePlusCommissionEmployee constructor

    // set base salary
    public void setBaseSalary( double salary )
    {
        if ( salary >= 0.0 )
            baseSalary = salary;
        else
            throw new IllegalArgumentException(
                "Base salary must be >= 0.0" );
    } // end method setBaseSalary
```

```
// return base salary
public double getBaseSalary()
{
    return baseSalary;
} // end method getBaseSalary

// calculate earnings
@Override // indicates that this method overrides a superclass method
public double earnings()
{
    // not allowed: commissionRate and grossSales private in superclass
    return baseSalary + ( commissionRate * grossSales );
} // end method earnings

// return String representation of BasePlusCommissionEmployee
@Override // indicates that this method overrides a superclass method
public String toString()
{
    // not allowed: attempts to access private superclass members
    return String.format(
        "%s: %s %s\n%s: %s\n%s: %.2f\n%s: %.2f\n%s: %.2f",
        "base-salaried commission employee", firstName, lastName,
        "social security number", socialSecurityNumber,
        "gross sales", grossSales, "commission rate", commissionRate,
        "base salary", baseSalary );
} // end method toString
} // end class BasePlusCommissionEmployee
```

BasePlusCommissionEmployee.java:39: commissionRate has private access in CommissionEmployee
    return baseSalary + ( commissionRate * grossSales );
                    ^
BasePlusCommissionEmployee.java:39: grossSales has private access in CommissionEmployee
    return baseSalary + ( commissionRate * grossSales );
                                      ^
BasePlusCommissionEmployee.java:49: firstName has private access in CommissionEmployee
    "base-salaried commission employee", firstName, lastName,
                                         ^
BasePlusCommissionEmployee.java:49: lastName has private access in CommissionEmployee
    "base-salaried commission employee", firstName, lastName,
                                                    ^
BasePlusCommissionEmployee.java:50: socialSecurityNumber has private access in CommissionEmployee
    "social security number", socialSecurityNumber,
                              ^
BasePlusCommissionEmployee.java:51: grossSales has private access in CommissionEmployee
    "gross sales", grossSales, "commission rate", commissionRate,
                  ^

Fig. 9.8 | private superclass members cannot be accessed in a subclass. (Part 2 of 3.)

BasePlusCommissionEmployee.java:51: commissionRate has private access in CommissionEmployee
"gross sales", grossSales, "commission rate", commissionRate,
^
7 errors

Fig. 9.8 | private superclass members cannot be accessed in a subclass. (Part 3 of 3.)

## 子类构造函数必须调用其超类的构造函数

每个子类构造函数必须隐式或显式调用其超类构造函数，以初始化从超类继承的实例变量。BasePlusCommissionEmployee 的六参数构造函数（第 9–16 行）中的第 13 行显式调用了类 CommissionEmployee 的五参数构造函数（在图 9.4 的第 13–22 行声明），以初始化 BasePlusCommissionEmployee 对象的超类部分（即变量 firstName、lastName、socialSecurityNumber、grossSales 和 commissionRate）。我们通过使用超类构造函数调用语法来实现这一点——关键字 super，后跟包含超类构造函数参数的括号。参数 first、last、ssn、sales 和 rate 分别用于初始化超类成员 firstName、lastName、socialSecurityNumber、grossSales 和 commissionRate。如果 BasePlusCommissionEmployee 的构造函数没有显式调用超类的构造函数，Java 将尝试调用超类的无参数或默认构造函数。类 CommissionEmployee 没有这样的构造函数，因此编译器会发出错误。图 9.8 第 13 行中的显式超类构造函数调用必须是子类构造函数体中的第一条语句。当超类包含无参数构造函数时，可以使用 super() 显式调用该构造函数，但这种情况很少见。

## BasePlusCommissionEmployee 方法 Earnings

编译器对第 39 行生成错误，因为超类 CommissionEmployee 的实例变量 commissionRate 和 grossSales 是 private——子类 BasePlusCommissionEmployee 的方法不允许访问超类 CommissionEmployee 的私有实例变量。我们在图 9.8 中使用红色文本标出了错误的<|message|>。编译器还在 BasePlusCommissionEmployee 的 toString 方法的第 49–51 行发出额外错误，原因相同。BasePlusCommissionEmployee 中的错误本可以通过使用从类 CommissionEmployee 继承的 get 方法来避免。例如，第 39 行本可以使用 getCommissionRate 和 getGrossSales 分别访问 CommissionEmployee 的私有实例变量 commissionRate 和 grossSales。第 49–51 行也可以使用适当的 get 方法来检索超类实例变量的值。

## 9.4.4 使用 protected 实例变量的 CommissionEmployee-BasePlusCommissionEmployee 继承层次结构

为了使类 BasePlusCommissionEmployee 能够直接访问超类实例变量 firstName、lastName、socialSecurityNumber、grossSales 和 commissionRate，我们可以在超类中将这些成员声明为 protected。正如我们在第 9.3 节中所讨论的，超类的 protected 成员可被该超类的所有子类访问。在新的 CommissionEmployee 类中，我们仅修改了图 9.4 的第 6–10 行，以使用 protected 访问修饰符声明实例变量，如下所示：

