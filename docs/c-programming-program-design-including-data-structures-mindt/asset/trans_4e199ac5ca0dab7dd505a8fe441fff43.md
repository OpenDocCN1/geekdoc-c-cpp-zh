
因为我们不想包含`class shape`的函数**绘制**和**移动**的定义，所以必须将这些函数转换为**纯虚函数**。在这种情况下，这些函数的原型是：

```cpp
virtual void draw() = 0;
virtual void move(double x, double y) = 0;
```

注意分号前的表达式`= 0`。一旦你在`class shape`中将这些函数设为纯虚函数，就不再需要为`class shape`提供这些函数的定义。

一旦一个类包含一个或多个纯虚函数，那么这个类就被称为**抽象类**。因此，`class shape`的抽象定义类似于以下内容：

```cpp
class shape
{
public:
    virtual void draw() = 0;
        //Function to draw the shape. Note that this is a
        //pure virtual function.

    virtual void move(double x, double y) = 0;
        //Function to move the shape at the position (x, y).
        //Note that this is a pure virtual function.
    .
    .
    .

};
```

由于抽象类（或其实现文件）不包含某些函数的定义，因此它*不*是一个完整的类，你不能创建该类的对象。

现在假设我们从`class shape`派生出`class rectangle`。为了使`rectangle`成为非抽象类，以便我们可以创建该类的对象，该类（或其实现文件）必须提供其基类（即`class shape`）的纯虚函数的定义。

注意，除了纯虚函数之外，抽象类还可以包含实例变量、构造函数和非纯虚函数。但是，抽象类必须提供构造函数和非纯虚函数的定义。下面的例子进一步说明了抽象类如何工作。

## 示例 12-9

在第11章中，我们定义了`class partTimeEmployee`，它派生自`class personType`，用以说明继承。我们还注意到有两种类型的员工：全职和兼职。全职员工的基本工资通常一年固定不变。此外，全职员工可能会获得奖金。另一方面，兼职员工的工资通常根据每小时工资率和工作小时数计算。在本例中，我们首先定义class employeeType，它派生自class personType，用于存储员工的姓名和ID。我们包含设置ID和获取ID的函数。我们还包含纯虚函数print和calculatePay，用于打印员工的数据，包括员工的ID、姓名和工资。

从class employeeType派生出类fullTimeEmployee和partTimeEmployee，并提供class employeeType的纯虚函数的定义。

class employeeType的定义如下：

```cpp
class employeeType: public personType
{
public:
    virtual void print() const = 0;
       //Function to output employee's data.

    virtual double calculatePay() const = 0;
       //Function to calculate and return the wages.
       //Postcondition: Pay is calculated and returned

    void setId(long id);
       //Function to set the ID.
       //Postcondition: personId = id

    long getId() const;
       //Function to retrieve the id.
       //Postcondition: returns personId

    employeeType(string first = "", string last = "",
                 long id = 0);
       //Constructor with parameters
       //Sets the first name, last name, payRate, and
       //hoursWorked according to the parameters. If
       //no value is specified, the default values are
       //assumed.
       //Postcondition: firstName = first;
       //               lastName = last; personId = id

private:
    long personId;       //stores the id
};
```

class employeeType的构造函数和非纯虚函数的定义如下：

```cpp
void employeeType::setId(long id)
{
    personId = id;
}

long employeeType::getId() const
{
    return personId;
}

employeeType::employeeType(string first, string last, long id)
        : personType(first, last)
{
    personId = id;
}
```

class fullTimeEmployee的定义如下：

```cpp
class fullTimeEmployee: public employeeType
{
public:
    void set(string first, string last, long id,
             double salary, double bonus);
    //Function to set the first name, last name,
    //id, and salary according to the parameters.
    //Postcondition: firstName = first; lastName = last;
    //                personId = id; empSalary = salary;
    //                empBonus = bonus

    void setSalary(double salary);
    //Function to set the salary.
    //Postcondition: empSalary = salary

    double getSalary();
    //Function to retrieve the salary.
    //Postcondition: returns empSalary

    void setBonus(double bonus);
    //Function to set the bonus.
    //Postcondition: empBonus = bonus

    double getBonus();
    //Function to retrieve the bonus.
    //Postcondition: returns empBonus

    void print() const;
    //Function to output the id, first name, last name,
    //and the wages.
    //Postcondition: Outputs
    //        Id:      id
    //        Name:    firstName lastName
    //        Wages:   $$$$.$$

    double calculatePay() const;
    //Function to calculate and return the wages.
    //Postcondition: Pay is calculated and returned

    fullTimeEmployee(string first = "", string last = "",
                     long id = 0, double salary = 0,
                     double bonus = 0);
        //Constructor with default parameters.
        //Sets the first name, last name, id, salary, and
        //bonus according to the parameters. If
        //no value is specified, the default values are assumed.
        //Postcondition: firstName = first; lastName = last;
        //               personId = id; empSalary = salary;
        //               empBonus = bonus

private:
    double empSalary;
    double empBonus;
};
```

`class fullTimeEmployee`的构造函数和函数的定义如下：

```cpp
void fullTimeEmployee::set(string first, string last,
                           long id,
                           double salary, double bonus)
{
    setName(first, last);
    setId(id);
    empSalary = salary;
    empBonus = bonus;
}

void fullTimeEmployee::setSalary(double salary)
{
    empSalary = salary;
}

double fullTimeEmployee::getSalary()
{
    return empSalary;
}

void fullTimeEmployee::setBonus(double bonus)
{
    empBonus = bonus;
}

double fullTimeEmployee::getBonus()
{
    return empBonus;
}

void fullTimeEmployee::print() const
{
    cout << "Id: " << getId() << endl;
    cout << "Name: ";
    personType::print();
    cout << endl;
    cout << "Wages: $" << calculatePay() << endl;
}

double fullTimeEmployee::calculatePay() const
{
    return empSalary + empBonus;
}

        //constructor
fullTimeEmployee::fullTimeEmployee(string first, string last,
                                    long id, double salary,
                                    double bonus)
    : employeeType(first, last, id)
{
    empSalary = salary;
    empBonus = bonus;
}
```

class partTimeEmployee的定义如下：

```cpp
class partTimeEmployee: public employeeType
{
public:
    void set(string first, string last, long id, double rate,
             double hours);
        //Function to set the first name, last name, id,
        //payRate, and hoursWorked according to the
        //parameters.
        //Postcondition: firstName = first; lastName = last;
        //               personId = id;
        //               payRate = rate; hoursWorked = hours

    double calculatePay() const;
        //Function to calculate and return the wages.
        //Postcondition: Pay is calculated and returned

    void setPayRate(double rate);
        //Function to set the pay rate.
        //Postcondition: payRate = rate

    double getPayRate();
        //Function to retrieve the pay rate.
        //Postcondition: returns payRate

    void setHoursWorked(double hours);
        //Function to set the hours worked.
        //Postcondition: hoursWorked = hours

    double getHoursWorked();
        //Function to retrieve the hours worked.
        //Postcondition: returns hoursWorked

    void print() const;
        //Function to output the Id, first name, last name,
        //and the wages.
        //Postcondition: Outputs
```
