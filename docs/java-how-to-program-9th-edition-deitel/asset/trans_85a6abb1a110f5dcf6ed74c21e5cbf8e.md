

## 10.5 案例研究：使用多态的工资系统 411

```
14 setGrossSales( sales );
15 setCommissionRate( rate );
16 } // end five-argument CommissionEmployee constructor

// set commission rate
public void setCommissionRate( double rate )
{
if ( rate > 0.0 && rate < 1.0 )
commissionRate = rate;
else
throw new IllegalArgumentException(
"Commission rate must be > 0.0 and < 1.0" );
} // end method setCommissionRate

// return commission rate
public double getCommissionRate()
{
return commissionRate;
} // end method getCommissionRate

// set gross sales amount
public void setGrossSales( double sales )
{
if ( sales >= 0.0 )
grossSales = sales;
else
throw new IllegalArgumentException(
"Gross sales must be >= 0.0" );
} // end method setGrossSales

// return gross sales amount
public double getGrossSales()
{
return grossSales;
} // end method getGrossSales

// calculate earnings; override abstract method earnings in Employee
@Override
public double earnings()
{
return getCommissionRate() * getGrossSales();
} // end method earnings

// return String representation of CommissionEmployee object
@Override
public String toString()
{
return String.format( "%s: %s%n%s: $%,.2f%n%s: %.2f",
"commission employee", super.toString(),
"gross sales", getGrossSales(),
"commission rate", getCommissionRate() );
} // end method toString
} // end class CommissionEmployee
```

## 10.5.5 间接具体子类 BasePlusCommissionEmployee

类 BasePlusCommissionEmployee（图 10.8）扩展类 CommissionEmployee（第 4 行），因此是类 Employee 的间接子类。类 BasePlusCommissionEmployee 有一个构造函数（第 9–14 行），它接受名字、姓氏、社会安全号码、销售额、佣金率和基本工资作为参数。然后它将除基本工资外的所有参数传递给 CommissionEmployee 构造函数（第 12 行）以初始化继承的成员。BasePlusCommissionEmployee 还包含一个 set 方法（第 17–24 行）用于为实例变量 baseSalary 分配新值，以及一个 get 方法（第 27–30 行）用于返回 baseSalary 的值。方法 earnings（第 33–37 行）计算 BasePlusCommissionEmployee 的收入。第 36 行在 earnings 方法中调用超类 CommissionEmployee 的 earnings 方法来计算员工收入中基于佣金的部分——这又是代码重用的一个很好的例子。BasePlusCommissionEmployee 的 toString 方法（第 40–46 行）创建 BasePlusCommissionEmployee 的字符串表示，其中包含 "base-salaried"，随后是调用超类 CommissionEmployee 的 toString 方法得到字符串（另一个代码重用的例子），然后是基本工资。结果是一个以 "base-salaried commission employee" 开头的字符串，后跟 BasePlusCommissionEmployee 的其余信息。回想一下，CommissionEmployee 的 toString 通过调用其超类（即 Employee）的 toString 方法获得员工的名字、姓氏和社会安全号码——又是代码重用的一个例子。BasePlusCommissionEmployee 的 toString 启动了一条跨越 Employee 层次结构所有三个层级的调用链。

```
// Fig. 10.8: BasePlusCommissionEmployee.java
// BasePlusCommissionEmployee class extends CommissionEmployee.
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
26    // return base salary
27    public double getBaseSalary()
28    {
29        return baseSalary;
30    } // end method getBaseSalary
31
32    // calculate earnings; override method earnings in CommissionEmployee
33    @Override
34    public double earnings()
35    {
36        return getBaseSalary() + super.earnings();
37    } // end method earnings
38
39    // return String representation of BasePlusCommissionEmployee object
40    @Override
41    public String toString()
42    {
43        return String.format( "%s %s; %s: $%,.2f",
44            "base-salaried", super.toString(),
45            "base salary", getBaseSalary() );
46    } // end method toString
47 } // end class BasePlusCommissionEmployee
```

图 10.8 | BasePlusCommissionEmployee 类扩展 CommissionEmployee。（第 2 部分，共 2 部分。）

## 10.5.6 多态处理、运算符 instanceof 和向下转型

为了测试我们的 Employee 层次结构，图 10.9 中的应用程序创建了四个具体类 SalariedEmployee、HourlyEmployee、CommissionEmployee 和 BasePlusCommissionEmployee 的对象。该程序通过各自对象类型的变量以非多态方式操作这些对象，然后通过 Employee 变量数组以多态方式使用。在多态处理对象时，程序将每个 BasePlusCommissionEmployee 的基本工资提高 10%——这需要确定对象的执行时类型。最后，程序以多态方式确定并输出 Employee 数组中每个对象的类型。第 9–18 行创建四个具体 Employee 子类的对象。第 22–30 行以非多态方式输出这些对象的字符串表示和收入。每个对象的 toString 方法在对象作为字符串使用 %s 格式说明符输出时由 printf 隐式调用。

```
1  // Fig. 10.9: PayrollSystemTest.java
2  // Employee hierarchy test program.
3
4  public class PayrollSystemTest
5  {
6      public static void main( String[] args )
7      {
8          // create subclass objects
9          SalariedEmployee salariedEmployee =
10             new SalariedEmployee( "John", "Smith", "111-11-1111", 800.00 );
```

```
11  HourlyEmployee hourlyEmployee =
12      new HourlyEmployee( "Karen", "Price", "222-22-2222", 16.75, 40 );
13  CommissionEmployee commissionEmployee =
14      new CommissionEmployee(
15      "Sue", "Jones", "333-33-3333", 10000, .06 );
16  BasePlusCommissionEmployee basePlusCommissionEmployee =
17      new BasePlusCommissionEmployee(
18      "Bob", "Lewis", "444-44-4444", 5000, .04, 300 );
19
20  System.out.println( "Employees processed individually:\n" );
21
22  System.out.printf( "%s\n%: $%,.2f\n\n",
23      salariedEmployee, "earned", salariedEmployee.earnings() );
24  System.out.printf( "%s\n%: $%,.2f\n\n",
25      hourlyEmployee, "earned", hourlyEmployee.earnings() );
26  System.out.printf( "%s\n%: $%,.2f\n\n",
27      commissionEmployee, "earned", commissionEmployee.earnings() );
28  System.out.printf( "%s\n%: $%,.2f\n\n",
29      basePlusCommissionEmployee,
30      "earned", basePlusCommissionEmployee.earnings() );
31
32  // create four-element Employee array
33  Employee[] employees = new Employee[ 4 ];
34
35  // initialize array with Employees
36  employees[ 0 ] = salariedEmployee;
37  employees[ 1 ] = hourlyEmployee;
38  employees[ 2 ] = commissionEmployee;
39  employees[ 3 ] = basePlusCommissionEmployee;
40
41  System.out.println( "Employees processed polymorphically:\n" );
42
43  // generically process each element in array employees
44  for ( Employee currentEmployee : employees )
45  {
46      System.out.println( currentEmployee ); // invokes toString
47
48      // determine whether element is a BasePlusCommissionEmployee
49      if ( currentEmployee instanceof BasePlusCommissionEmployee )
50      {
51          // downcast Employee reference to
52          // BasePlusCommissionEmployee reference
53          BasePlusCommissionEmployee employee =
54              ( BasePlusCommissionEmployee ) currentEmployee;
55
56          employee.setBaseSalary( 1.10 * employee.getBaseSalary() );
57
58          System.out.printf(
59              "new base salary with 10%% increase is: $%,.2f\n",
60              employee.getBaseSalary() );
61      } // end if
```

图 10.9 | Employee 层次结构测试程序。（第 1 部分，共 4 部分。）

