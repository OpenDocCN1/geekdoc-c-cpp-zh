
将 socialSecurityNumber、grossSales 和 commissionRate 设为私有属性（第6–10行），并提供公共方法 setFirstName、getFirstName、setLastName、getLastName、setSocialSecurityNumber、getSocialSecurityNumber、setGrossSales、getGrossSales、setCommissionRate、getCommissionRate、earnings 和 toString 来操作这些值。方法 earnings（第93–96行）和 toString（第99–107行）使用类的 get 方法获取其实例变量的值。如果我们决定更改实例变量名，earnings 和 toString 的声明不需要修改——只有直接操作实例变量的 get 和 set 方法的方法体需要更改。这些更改仅发生在超类内部——无需对子类进行修改。将此类更改的影响局部化是一种良好的软件工程实践。

```
// Fig. 9.10: CommissionEmployee.java
// CommissionEmployee class uses methods to manipulate its
// private instance variables.
public class CommissionEmployee
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
```

图9.10 | CommissionEmployee 类使用方法来操作其私有实例变量。（第1部分，共3部分）

```
39     lastName = last; // should validate
40   } // end method setLastName
41
42   // return last name
43   public String getLastName()
44   {
45       return lastName;
46   } // end method getLastName
47
48   // set social security number
49   public void setSocialSecurityNumber( String ssn )
50   {
51       socialSecurityNumber = ssn; // should validate
52   } // end method setSocialSecurityNumber
53
54   // return social security number
55   public String getSocialSecurityNumber()
56   {
57       return socialSecurityNumber;
58   } // end method getSocialSecurityNumber
59
60   // set gross sales amount
61   public void setGrossSales( double sales )
62   {
63       if ( sales >= 0.0 )
64           grossSales = sales;
65       else
66           throw new IllegalArgumentException(
67               "Gross sales must be >= 0.0" );
68   } // end method setGrossSales
69
70   // return gross sales amount
71   public double getGrossSales()
72   {
73       return grossSales;
74   } // end method getGrossSales
75
76   // set commission rate
77   public void setCommissionRate( double rate )
78   {
79       if ( rate > 0.0 && rate < 1.0 )
80           commissionRate = rate;
81       else
82           throw new IllegalArgumentException(
83               "Commission rate must be > 0.0 and < 1.0" );
84   } // end method setCommissionRate
85
86   // return commission rate
87   public double getCommissionRate()
88   {
89       return commissionRate;
90   } // end method getCommissionRate
```

图9.10 | CommissionEmployee 类使用方法来操作其私有实例变量。（第2部分，共3部分）

```
91
92   // calculate earnings
93   public double earnings()
94   {
95     return getCommissionRate() * getGrossSales();
96   } // end method earnings
97
98   // return String representation of CommissionEmployee object
99   @Override // indicates that this method overrides a superclass method
100  public String toString()
101  {
102    return String.format( "%s: %s %s\n%s: %s\n%s: %.2f\n%s: %.2F",
103      "commission employee", getFirstName(), getLastName(),
104      "social security number", getSocialSecurityNumber(),
105      "gross sales", getGrossSales(),
106      "commission rate", getCommissionRate() );
107  } // end method toString
108 } // end class CommissionEmployee
```

图9.10 | CommissionEmployee 类使用方法来操作其私有实例变量。（第3部分，共3部分）

子类 BasePlusCommissionEmployee（图9.11）继承了 CommissionEmployee 的非私有方法，并可以通过这些方法访问超类的私有成员。类 BasePlusCommissionEmployee 有几处变化，使其不同于图9.9。方法 earnings（第35–39行）和 toString（第42–47行）各自调用方法 getBaseSalary 来获取基本工资值，而不是直接访问 baseSalary。如果我们决定重命名实例变量 baseSalary，只需要修改 setBaseSalary 和 getBaseSalary 方法的方法体。

```
// Fig. 9.11: BasePlusCommissionEmployee.java
// BasePlusCommissionEmployee class inherits from CommissionEmployee
// and accesses the superclass’s private data via inherited
// public methods.

public class BasePlusCommissionEmployee extends CommissionEmployee
{
  private double baseSalary; // base salary per week

  // six-argument constructor
  public BasePlusCommissionEmployee( String first, String last,
    String ssn, double sales, double rate, double salary )
  {
    super( first, last, ssn, sales, rate );
    setBaseSalary( salary ); // validate and store base salary
  } // end six-argument BasePlusCommissionEmployee constructor
```

图9.11 | BasePlusCommissionEmployee 类继承自 CommissionEmployee，并通过继承的公共方法访问超类的私有数据。（第1部分，共2部分）

```
18  // set base salary
19  public void setBaseSalary( double salary )
20  {
21      if ( salary >= 0.0 )
22          baseSalary = salary;
23      else
24          throw new IllegalArgumentException(
25              "Base salary must be >= 0.0" );
26  } // end method setBaseSalary
27
28  // return base salary
29  public double getBaseSalary()
30  {
31      return baseSalary;
32  } // end method getBaseSalary
33
34  // calculate earnings
35  @Override // indicates that this method overrides a superclass method
36  public double earnings()
37  {
38      return getBaseSalary() + super.earnings();
39  } // end method earnings
40
41  // return String representation of BasePlusCommissionEmployee
42  @Override // indicates that this method overrides a superclass method
43  public String toString()
44  {
45      return String.format( "%s %s\n%s: %.2f", "base-salaried",
46          super.toString(), "base salary", getBaseSalary() );
47  } // end method toString
48 } // end class BasePlusCommissionEmployee
```

图9.11 | BasePlusCommissionEmployee 类继承自 CommissionEmployee，并通过继承的公共方法访问超类的私有数据。（第2部分，共2部分）

## BasePlusCommissionEmployee 类的 earnings 方法

earnings 方法（第35–39行）重写了类 CommissionEmployee 的 earnings 方法（图9.10，第93–96行），用于计算领取基本工资的佣金员工的收入。新版本通过 super.earnings()（第34行）调用 CommissionEmployee 的 earnings 方法，仅获取基于佣金的那部分收入，然后加上基本工资以计算总收入。注意从子类调用被重写的超类方法所使用的语法——在超类方法名之前放置关键字 super 和点（.）分隔符。这种方法调用是一种良好的软件工程实践——如果一个方法执行了另一个方法所需的全部或部分操作，就应调用该方法而不是重复其代码。通过让 BasePlusCommissionEmployee 的 earnings 方法调用 CommissionEmployee 的 earnings 方法来计算 BasePlusCommissionEmployee 对象的部分收入，我们避免了重复代码并减少了代码维护问题。如果不使用“super.”，则 BasePlusCommissionEmployee 的 earnings 方法将调用自身而不是超类版本。这将导致我们在第18章中研究的一种称为无限递归的现象，最终会导致方法调用栈溢出——这是一个致命的运行时错误。

