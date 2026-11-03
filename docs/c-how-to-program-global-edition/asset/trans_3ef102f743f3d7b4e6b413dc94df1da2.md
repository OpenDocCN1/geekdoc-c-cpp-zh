
```
class CommissionEmployee
{
public:
CommissionEmployee( const std::string &, const std::string &,
    const std::string &, double = 0.0, double = 0.0 );

void setFirstName( const std::string & ); // set first name
std::string getFirstName() const; // return first name

void setLastName( const std::string & ); // set last name
std::string getLastName() const; // return last name

void setSocialSecurityNumber( const std::string & ); // set SSN
std::string getSocialSecurityNumber() const; // return SSN

void setGrossSales( double ); // set gross sales amount
double getGrossSales() const; // return gross sales amount

void setCommissionRate( double ); // set commission rate (percentage)
double getCommissionRate() const; // return commission rate

double earnings() const; // calculate earnings
void print() const; // print CommissionEmployee object
private:
std::string firstName;
std::string lastName;
std::string socialSecurityNumber;
double grossSales; // gross weekly sales
double commissionRate; // commission percentage
}; // end class CommissionEmployee
#endif
```

图 19.4 | CommissionEmployee 类头文件。 (第 2 部分，共 2 部分。)

```
// Fig. 19.5: CommissionEmployee.cpp
// Class CommissionEmployee member-function definitions.
#include <iostream>
#include <sstream>
#include "CommissionEmployee.h" // CommissionEmployee class definition
using namespace std;

// constructor
CommissionEmployee::CommissionEmployee(
    const string &first, const string &last, const string &ssn,
    double sales, double rate )
{
    firstName = first; // should validate
    lastName = last; // should validate
    socialSecurityNumber = ssn; // should validate
    setGrossSales( sales ); // validate and store gross sales
```

图 19.5 | 表示按销售额百分比领取报酬的员工的 CommissionEmployee 类的实现文件。 (第 1 部分，共 3 部分。)

```
setCommissionRate( rate ); // validate and store commission rate
} // end CommissionEmployee constructor

// set first name
void CommissionEmployee::setFirstName( const string &first )
{
    firstName = first; // should validate
} // end function setFirstName

// return first name
string CommissionEmployee::getFirstName() const
{
    return firstName;
} // end function getFirstName

// set last name
void CommissionEmployee::setLastName( const string &last )
{
    lastName = last; // should validate
} // end function setLastName

// return last name
string CommissionEmployee::getLastName() const
{
    return lastName;
} // end function getLastName

// set social security number
void CommissionEmployee::setSocialSecurityNumber( const string &ssn )
{
    socialSecurityNumber = ssn; // should validate
} // end function setSocialSecurityNumber

// return social security number
string CommissionEmployee::getSocialSecurityNumber() const
{
    return socialSecurityNumber;
} // end function getSocialSecurityNumber

// set gross sales amount
void CommissionEmployee::setGrossSales( double sales )
{
    if ( sales >= 0.0 )
        grossSales = sales;
    else
        throw invalid_argument( "Gross sales must be >= 0.0" );
} // end function setGrossSales

// return gross sales amount
double CommissionEmployee::getGrossSales() const
{
```

```
68 return grossSales;
69 } // end function getGrossSales
70

71 // set commission rate
72 void CommissionEmployee::setCommissionRate( double rate )
73 {
74    if ( rate > 0.0 && rate < 1.0 )
75       commissionRate = rate;
76    else
77       throw invalid_argument( "Commission rate must be > 0.0 and < 1.0" );
78 } // end function setCommissionRate

80 // return commission rate
81 double CommissionEmployee::getCommissionRate() const
82 {
83    return commissionRate;
84 } // end function getCommissionRate

86 // calculate earnings
87 double CommissionEmployee::earnings() const
88 {
89    return commissionRate * grossSales;
90 } // end function earnings

92 // print CommissionEmployee object
93 void CommissionEmployee::print() const
94 {
95    cout << "commission employee: " << firstName << ' ' << lastName
96        << "\n social security number: " << socialSecurityNumber
97        << "\n gross sales: " << grossSales
98        << "\n commission rate: " << commissionRate;
99 } // end function print
```

图 19.5 | 表示按销售额百分比领取报酬的员工的 CommissionEmployee 类的实现文件。 (第 3 部分，共 3 部分。)

## CommissionEmployee 构造函数

CommissionEmployee 构造函数的定义在该节的前几个示例中故意不使用成员初始化器语法，以便我们可以演示 private 和 protected 限定符如何影响派生类中的成员访问。如 Fig. 19.5 所示，第 13–15 行，我们在构造函数体中为数据成员 firstName、lastName 和 socialSecurityNumber 分配值。本节后面我们将重新使用成员初始化列表于构造函数中。

我们在将它们分配给相应的数据成员之前，并未对构造函数参数 first、last 和 ssn 的值进行验证。我们当然可以验证名字和姓氏——例如通过确保其长度合理。同样，社会安全号码也可以被验证以确保其包含九位数字，可带或不带连字符（例如 123-45-6789 或 123456789）。

## CommissionEmployee 成员函数 earnings 和 print

成员函数 earnings（第 87–90 行）计算 CommissionEmployee 的收入。第 89 行将 commissionRate 与 grossSales 相乘并返回结果。成员函数 print（第 93–99 行）显示 CommissionEmployee 对象的数据成员的值。

### 测试类 CommissionEmployee

图 19.6 测试类 CommissionEmployee。第 11–12 行实例化 CommissionEmployee 对象 employee 并调用构造函数，用 "Sue" 作为名字、"Jones" 作为姓氏、"222-22-2222" 作为社会安全号码、10000 作为销售额和 .06 作为佣金率来初始化该对象。第 19–24 行使用 employee 的 get 函数显示其数据成员的值。第 26–27 行调用对象的成员函数 setGrossSales 和 setCommissionRate 分别更改数据成员 grossSales 和 commissionRate 的值。然后第 31 行调用 employee 的 print 成员函数输出更新后的 CommissionEmployee 信息。最后，第 34 行显示 CommissionEmployee 的收入，该收入由对象的 earnings 成员函数使用数据成员 grossSales 和 commissionRate 的更新值计算得出。

```
```
```cpp
1  // Fig. 19.6: fig19_06.cpp
2  // CommissionEmployee class test program.
3  #include <iostream>
4  #include <iomanip>
5  #include "CommissionEmployee.h" // CommissionEmployee class definition
6  using namespace std;
7
8  int main()
9  {
10     // instantiate a CommissionEmployee object
11     CommissionEmployee employee(
12        "Sue", "Jones", "222-22-2222", 10000, .06 );
13
14     // set floating-point output formatting
15     cout << fixed << setprecision( 2 );
16
17     // get commission employee data
18     cout << "Employee information obtained by get functions: \n"
19        << "\nFirst name is " << employee.getFirstName()
20        << "\nLast name is " << employee.getLastName()
21        << "\nSocial security number is "
22        << employee.getSocialSecurityNumber()
23        << "\nGross sales is " << employee.getGrossSales()
24        << "\nCommission rate is " << employee.getCommissionRate() << endl;
25
26     employee.setGrossSales( 8000 ); // set gross sales
27     employee.setCommissionRate( .1 ); // set commission rate
28
29     cout << "\nUpdated employee information output by print function: \n"
30        << endl;
31     employee.print(); // display the new employee information
32
33     // display the employee's earnings
34     cout << "\n\nEmployee's earnings: $" << employee.earnings() << endl;
35  } // end main
```
```

图 19.6 | CommissionEmployee 类测试程序。 (第 1 部分，共 2 部分。)

