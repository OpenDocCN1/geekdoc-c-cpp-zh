
```cpp
    firstName = first; // should validate
    lastName = last; // should validate
    socialSecurityNumber = ssn; // should validate
    setGrossSales( sales ); // validate and store gross sales
    setCommissionRate( rate ); // validate and store commission rate
    setBaseSalary( salary ); // validate and store base salary
} // end BasePlusCommissionEmployee constructor

// set first name
void BasePlusCommissionEmployee::setFirstName( const string &first )
{
    firstName = first; // should validate
} // end function setFirstName

// return first name
string BasePlusCommissionEmployee::getFirstName() const
{
    return firstName;
} // end function getFirstName

// set last name
void BasePlusCommissionEmployee::setLastName( const string &last )
{
    lastName = last; // should validate
} // end function setLastName

// return last name
string BasePlusCommissionEmployee::getLastName() const
{
    return lastName;
} // end function getLastName

// set social security number
void BasePlusCommissionEmployee::setSocialSecurityNumber(
    const string &ssn )
{
    socialSecurityNumber = ssn; // should validate
} // end function setSocialSecurityNumber

// return social security number
string BasePlusCommissionEmployee::getSocialSecurityNumber() const
{
    return socialSecurityNumber;
} // end function getSocialSecurityNumber

// set gross sales amount
void BasePlusCommissionEmployee::setGrossSales( double sales )
{
    if ( sales >= 0.0 )
        grossSales = sales;
    else
        throw invalid_argument( "Gross sales must be >= 0.0" );
} // end function setGrossSales

// return gross sales amount
double BasePlusCommissionEmployee::getGrossSales() const
{
    return grossSales;
} // end function getGrossSales

// set commission rate
void BasePlusCommissionEmployee::setCommissionRate( double rate )
{
    if ( rate > 0.0 && rate < 1.0 )
        commissionRate = rate;
    else
        throw invalid_argument( "Commission rate must be > 0.0 and < 1.0" );
} // end function setCommissionRate

// return commission rate
double BasePlusCommissionEmployee::getCommissionRate() const
{
    return commissionRate;
} // end function getCommissionRate

// set base salary
void BasePlusCommissionEmployee::setBaseSalary( double salary )
{
    if ( salary >= 0.0 )
        baseSalary = salary;
    else
        throw invalid_argument( "Salary must be >= 0.0" );
} // end function setBaseSalary

// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const
{
    return baseSalary;
} // end function getBaseSalary

// calculate earnings
double BasePlusCommissionEmployee::earnings() const
{
    return baseSalary + ( commissionRate * grossSales );
} // end function earnings

// print BasePlusCommissionEmployee object
void BasePlusCommissionEmployee::print() const
{
    cout << "base-salaried commission employee: " << firstName << ' '
        << lastName << "\nsocial security number: " << socialSecurityNumber
```

**Fig. 12.8** | *BasePlusCommissionEmployee* 类表示除佣金外还领取底薪的雇员。（第 2 部分，共 4 部分。）

**Fig. 12.8** | *BasePlusCommissionEmployee* 类表示除佣金外还领取底薪的雇员。（第 3 部分，共 4 部分。）

```cpp
    // instantiate BasePlusCommissionEmployee object
    BasePlusCommissionEmployee
        employee( "Bob", "Lewis", "333-33-3333", 5000, .04, 300 );

    // set floating-point output formatting
    cout << fixed << setprecision( 2 );

    // get commission employee data
    cout << "\nEmployee information obtained by get functions: \n"
        << "\nFirst name is " << employee.getFirstName()
        << "\nLast name is " << employee.getLastName()
        << "\nSocial security number is "
        << employee.getSocialSecurityNumber()
        << "\nGross sales is " << employee.getGrossSales()
        << "\nCommission rate is " << employee.getCommissionRate()
        << "\nBase salary is " << employee.getBaseSalary() << endl;

    employee.setBaseSalary( 1000 ); // set base salary

    cout << "\nUpdated employee information output by print function: \n"
        << endl;
    employee.print(); // display the new employee information

    // display the employee's earnings
    cout << "\nEmployee's earnings: $" << employee.earnings() << endl;
} // end main
```

```text
Employee information obtained by get functions:

First name is Bob
Last name is Lewis
Social security number is 333-33-3333
Gross sales is 5000.00
Commission rate is 0.04
Base salary is 300.00

Updated employee information output by print function:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 1000.00

Employee's earnings: $1200.00
```

**Fig. 12.9** | *BasePlusCommissionEmployee 类测试程序。（第 2 部分，共 2 部分。）*

## 探讨类 BasePlusCommissionEmployee 与类 CommissionEmployee 之间的相似性

类 BasePlusCommissionEmployee（图 12.7–12.8）的大部分代码与类 CommissionEmployee（图 12.4–12.5）的代码相似，甚至完全相同。例如，在类 BasePlusCommissionEmployee 中，私有数据成员 firstName 和 lastName，以及成员函数 `setFirstName`、`getFirstName`、`setLastName` 和 `getLastName` 与类 `CommissionEmployee` 中的相应内容完全相同。类 `CommissionEmployee` 和 `BasePlusCommissionEmployee` 也都包含私有数据成员 `socialSecurityNumber`、`commissionRate` 和 `grossSales`，以及用于操作这些成员的 get 和 set 函数。此外，`BasePlusCommissionEmployee` 构造函数与类 `CommissionEmployee` 的构造函数*几乎*相同，区别在于 `BasePlusCommissionEmployee` 的构造函数还设置了 `baseSalary`。类 BasePlusCommissionEmployee 的其他新增内容是私有数据成员 `baseSalary` 以及成员函数 `setBaseSalary` 和 `getBaseSalary`。类 `BasePlusCommissionEmployee` 的 `print` 成员函数与类 `CommissionEmployee` 的 `print` 成员函数*几乎相同*，区别在于 `BasePlusCommissionEmployee` 的 `print` 还输出数据成员 `baseSalary` 的值。

我们实际上从类 `CommissionEmployee` *复制*代码并*粘贴*到类 `BasePlusCommissionEmployee` 中，然后修改类 `BasePlusCommissionEmployee`，使其包含底薪以及操作底薪的成员函数。这种*复制粘贴*方法容易出错且耗时。

![](img/bfd978e7e9b192bab46ec2a89e481263_547_0.png)

### 软件工程观察 12.1

从一个类复制粘贴代码到另一个类，会散布同一代码的许多实体副本，并可能在整个系统中传播错误，造成代码维护噩梦。为避免重复代码（以及可能的错误），当你希望一个类“吸收”另一个类的数据成员和成员函数时，应使用继承，而不是“复制粘贴”方法。

![](img/bfd978e7e9b192bab46ec2a89e481263_547_1.png)

### 软件工程观察 12.2

使用继承时，层次结构中所有类的公共数据成员和成员函数都在基类中声明。当需要修改这些公共特性时，只需在基类中进行修改——派生类随后会继承这些修改。如果不使用继承，则需要对所有包含相关代码副本的源代码文件进行修改。

### 12.4.3 创建 CommissionEmployee–BasePlusCommissionEmployee 继承层次结构

现在，我们创建并测试一个新的 `BasePlusCommissionEmployee` 类（图 12.10–12.11），它*派生自*类 `CommissionEmployee`（图 12.4–12.5）。在此示例中，`BasePlusCommissionEmployee` 对象是一个 `CommissionEmployee` 对象（因为继承传递了类 `CommissionEmployee` 的能力），但类 `BasePlusCommissionEmployee` 还具有数据成员 `baseSalary`（图 12.10，第 23 行）。类定义第 11 行中的*冒号*（`:`）表示继承。关键字 `public` 表示*继承类型*。作为派生类（通过公有继承形成），`BasePlusCommissionEmployee` 继承类 `CommissionEmployee` 的*所有*成员，*除了*构造函数——每个类都提供自己特有的构造函数。（析构函数也不被继承。）因此，`BasePlusCommissionEmployee` 的公共服务包括其构造函数（第 14–15 行）以及继承自类 `CommissionEmployee` 的公有成员函数——尽管在 `BasePlusCommissionEmployee` 的源代码中看不到这些继承的成员函数，但它们仍然是派生类 `BasePlusCommissionEmployee` 的一部分。派生类的公共服务还包括派生成员函数 `setBaseSalary`、`getBaseSalary`、`earnings` 和 `print`（第 17–21 行）。
