
```cpp
cout << "Number of Players: "
     << sp[i].numberOfPlayers << endl;
cout << "Team Payroll: $" << sp[i].teamPayroll << endl;
cout << "Coach Salary: $" << sp[i].coachSalary << endl;
cout << "--------------------------------" << endl
     << endl;
}

for (int j = 0; j < 20; j++)
    printData(soccer[j]);
```

## 第10章

- 1. a. 错误；b. 错误；c. 正确；d. 错误；e. 错误

- 3. 构造函数没有类型。第6行的语句应为

```cpp
syntaxErrors2(int = 0,
              double = 0);    //Line 6
```

另外，将 `private` 后的 `;` 替换为 `:`。第7行应为

```cpp
private:                         //Line 7
```

- 5. 函数 `set` 必须有返回类型。构造函数不能是 `const`。将 `}` 后的 `:` 替换为 `;`。第4、6和12行的语句应如下：

```cpp
void set(string, int, double);        //Line 4
syntaxErrors4() const;                //Line 6
};                                   //Line 12
```

- 7.
  - a.

```cpp
void foodType::set(string s, int c, double f, int su,
                   double cr, double p)
{
    name = s;

    if (c >= 0)
        calories = c;
    else
        calories = 0;

    if (f >= 0)
        fat = f;
    else
        fat = 0;

    if (su >= 0)
        sugar = su;
    else
        sugar = 0;

    if (cr >= 0)
        carbohydrate = cr;
    else
        carbohydrate = 0;

    if (p >= 0)
        potassium = p;
    else
        potassium = 0;
}
```

  - b.

```cpp
void foodType::print() const
{
    cout << "Name: " << name << endl;
    cout << "Calories: " << calories << endl;
    cout << "Fat: " << fat << endl;
    cout << "Sugar: " << sugar << endl;
    cout << "Carbohydrate: " << carbohydrate << endl;
    cout << "Potassium: " << potassium << endl;
}
```

  - c.

```cpp
string foodType::getName() const
{
    return name;
}

int foodType::getCalories() const
{
    return calories;
}

double foodType::getFat() const
{
    return fat;
}

int foodType::getSugar() const
{
    return sugar;
}

double foodType::getCarbohydrate() const
{
    return carbohydrate;
}

double foodType::getPotassium() const
{
    return potassium;
}
```

  - d.

```cpp
foodType::foodType()
{
    set("", 0, 0.0, 0, 0.0, 0.0);
}
```

  - e.

```cpp
foodType::foodType(string s, int c, double f,
                   int su, double cr, double p)
{
    set(s, c, f, su, cr, p);
}
```

  - f. `fruit2.print();`
  - g. `foodType myFruit("Apple", 52, 0.2, 10, 13.8, 148.0);`

- 9. 函数 `print`、`getQuantitiesInStock`、`getPrice` 和 `getDiscount` 是访问器；函数 `set`、`setQuantitiesInStock`、`updateQuantitiesInStock`、`setPrice` 和 `setDiscount` 是修改器。

- 11. a. 28；b. 8；c. 1；d. 9

- 13.
  - a. 14
  - b. 3
  - c. 类 `temporary` 只有一个构造函数。因为这是一个带默认参数的构造函数，所以可以在不指定任何参数的情况下初始化对象。例如，以下语句创建对象 `newObject`，其实例变量分别初始化为 `""`、0 和 0。

```cpp
temporary newObject;
```

- 15. 第1行的语句创建 `object1`，并将该对象的实例变量初始化为 `""`、0 和 0，即 `object1.description = ""; object1.first = 0.0;` 和 `object1.second = 0.0;`。第2行的语句创建 `object2`，并将该对象的实例变量初始化如下：`object2.description = "rectangle"; object2.first = 3.0;` 和 `object2.second = 5.0;`。第3行的语句创建 `object3`，并将该对象的实例变量初始化如下：`object3.description = "circle"; object3.first = 6.5;` 和 `object3.second = 0.0;`。第4行的语句创建 `object4`，并将该对象的实例变量初始化如下：`object4.description = "cylinder"; object4.first = 6.0;` 和 `object4.second = 3.5;`。

- 17. 类对象有两种内置操作：成员访问（.）和赋值（=）。

- 19.

```text
10:17:00
23:59:29
00:00:29
```

- 21.
  - a. `personType student("Buddy", "Arora");`
  - b. `student.print();`
  - c. `student.setName("Susan", "Gilbert");`

- 23. 构造函数是类的成员，当实例化类对象并在对象声明中指定调用构造函数时，它会自动执行。类中包含构造函数是为了在声明对象时正确初始化对象。

- 25. 析构函数是类的成员，如果类中包含析构函数，那么当类对象超出作用域时，它会自动执行。其主要目的是释放对象创建的动态内存。

- 27. 它通常会在每次调用函数的位置插入内联函数的代码。

- 29.
  - a. `myClass::count = 0;`
  - b. `myClass::incrementCount();`
  - c. `myClass.printCount();`

```cpp
int myClass::count = 0;
void myClass::setX(int a)
{
    x = a;
}

void myClass::printX() const
{
    cout << x;
}

void myClass::printCount()
{
    cout << count;
}

void myClass::incrementCount()
{
    count++;
}

myClass::myClass(int a)
{
    x = a;
}
```

  - e. `myClass myObject1(5);`
  - f. `myClass myObject2(7);`
  - g. 第1行和第2行的语句是有效的。

第3行的语句应为 `myClass::printCount();`

第4行的语句无效，因为成员函数 `printX` 不是类的 `static` 成员，所以不能使用类名调用它。

第5行的语句无效，因为 `count` 是类的 `private static` 成员变量。

  - h.

```text
5
2
2
3
14
3
3
```

## 第11章

- 1. a. 错误；b. 错误；c. 正确；d. 正确；e. 正确；f. 正确；g. 正确；h. 正确；i. 错误；j. 错误；k. 正确

- 3. 可以添加到类 `employeeType` 的一些成员变量如下：`department`、`salary`、`employeeCategory`（例如主管和总裁）和 `employeeID`。一些成员函数如下：`setInfo`、`setSalary`、`getSalary`、`setDepartment`、`getDepartment`、`setCategory`、`getCategory`、`setID` 和 `getID`。

```cpp
class employeeType: public personType
{
public:
    void setInfo(string, string, string, double, string, string);
    void setSalary(double);
    void setDepartment(string);
    void setCategory(string);
    void setID(string);
    double getSalary() const;
    string getDepartment() const;
    string getCategory() const;
    string getID() const;

private:
    string department;
    double salary;
    string employeeCategory;
    string employeeID;
};
```

- 5.
  - a. 基类是 `shoe`，派生类是 `runningShoe`。
  - b. 这是私有继承。

- 7. 对象 `newCylinder` 的私有成员是 `xCoordinate`、`yCoordinate`、`radius` 和 `height`。

- 9. 省略 `employee` 前的单词 `class`。第一条语句应为

```cpp
class hourlyEmployee : public employee
```

在第三行中，将 `::` 替换为 `:`。该语句应为

```cpp
public:
```

从函数 `setHoursWorked` 和 `setPay` 的原型中省略单词 `const`，因为这些函数会修改实例变量。这些原型应如下：

```cpp
void setHoursWorked(double hrsWk);
void setPay();
```

将标签 `private` 后的 `;` 替换为 `:`。该语句应为 `private:`

- 11.
  - a. `void print() const;`
  - b.

```cpp
void set(int, int, int);
void get(int&, int&, int&);
```

- 13. 首先会执行 `class one` 的构造函数，然后执行 `class two` 的构造函数，最后执行 `class three` 的构造函数。

- 15.
  - a. 无效。因为 `z` 是派生类的实例变量，所以类 `smart` 的成员不能访问它。
  - b. 无效。`secret` 是类 `smart` 的私有成员。不能在类外直接访问它。此外，`z` 是类 `superSmart` 的私有成员。不能在类外直接访问它。
  - c. 有效
  - d. 无效。`smart` 是类名，而不是该类的对象。不能使用它调用其成员函数 `print`。
  - e. 无效。`superSmart` 是类名。不能使用它访问其成员。

- 17. 在预处理指令 `#ifndef` 和 `#endif` 之间。类 one 和类 two 的定义可以放在这些指令之间，如下所示：

```cpp
#ifndef H_one                         #ifndef H_two
#define H_one                         #define H_two

//place the definition of the       //place the definition
//the class one here                //of the class two here

#endif                              #endif
```

- 19. 在私有继承中，基类的公有成员是派生类的私有成员。它们可以在派生类中直接访问。基类的受保护成员是派生类的私有成员。它们可以由派生类的成员函数（以及友元函数）直接访问。基类的私有成员在派生类中被隐藏。它们不能在派生类中直接访问。它们可以由成员函数（以及友元
