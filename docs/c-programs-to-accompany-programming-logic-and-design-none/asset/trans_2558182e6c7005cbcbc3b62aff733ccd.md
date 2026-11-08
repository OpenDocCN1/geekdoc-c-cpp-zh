
程序不再需要它们。图9-3所示的C++程序fileIOTest.cpp实现了本节讨论的文件输入和输出操作。

```cpp
// fileIOTest.cpp
// Input:  inputFile.dat
// Output: outputFile.dat

#include <fstream>
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string firstName;
    string lastName;
    double salary;
    double new_salary;
    const double INCREASE = 1.15;
    ifstream data_in;
    ofstream data_out;

    // Open input and output file
    data_in.open("inputFile.dat");
    data_out.open("outputFile.dat");

    // Read record from input file
    data_in >> firstName;
    data_in >> lastName;
    data_in >> salary;
    // Calculate new salary
    new_salary = salary * INCREASE;
    // Write record to output file
    data_out << firstName << endl;
    data_out << lastName << endl;
    data_out << new_salary << endl;
    // Close files
    data_in.close();
    data_out.close();
    return 0;
} // End of main function
```

图9-3 读取和写入文件数据

在编写打开文件和写入文件的代码时，需要注意两个潜在问题：第一，程序可能尝试打开一个不存在的文件；第二，程序可能尝试读取超过EOF标记的内容。随着你对C++的深入学习，你将学会如何处理这些错误情况。它们超出了本书的范围。

### 练习9-3：打开文件并执行文件输入

在本练习中，你将运用所学的打开文件以及从文件向程序输入内容的知识，回答有关图9-4所示代码的问题。

```cpp
1    ofstream data_in;
2    data_in.open(myVideoFile.dat);
3    string videoName, videoPrice, videoShelf;
4    data_in >> videoShelf;
5    data_in >> videoPrice;
6    data_in >> videoName;
```

**图9-4** 练习9-3的代码

- 1. 描述第1行中的错误，并解释如何修复它。
- 2. 描述第2行中的错误，并解释如何修复它。
- 3. 考虑来自输入文件`myVideoFile.dat`的以下数据：

    ```text
    Shrek 13.00 1A
    Jaws 14.00 2C
    Casablanca 17.00 3B
    ```

    - a. 变量`videoName`中存储了什么值？
    - b. 变量`videoPrice`中存储了什么值？
    - c. 变量`videoShelf`中存储了什么值？
    - d. 如果这些变量的值有问题，问题是什么？你如何修复它？

### 实验9-3：使用输入文件

在本实验中，你将在预先编写的C++程序中打开一个文件并从中读取输入。该程序应读取并打印存储在输入文件`fish.dat`中的鱼名。

- 1. 使用记事本或你选择的文本编辑器打开名为`Fish.cpp`的源代码文件。
- 2. 声明你需要的变量。
- 3. 编写C++语句，以读取方式打开输入文件`fish.dat`。
- 4. 包含打印标题和执行预读的语句。然后，编写一个`while`循环，读取输入直到到达EOF。
- 5. 在循环体内，打印每条鱼的名称并读取下一条鱼。退出循环后，记得关闭文件。
- 6. 将此源代码文件保存到你选择的目录中，然后将该目录设为你的工作目录。
- 7. 编译源代码文件`Fish.cpp`。
- 8. 执行程序。

## 10 面向对象的C++

**学习完本章后，你将能够：**

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_194_0.png)

- 解释面向对象的基本概念
- 创建一个简单的程序员定义的类
- 在C++程序中使用程序员定义的类
- 使用继承创建派生C++类
- 在C++程序中使用派生类

请注意，本章涵盖的主题包括Joyce Farrell所著《Programming Logic and Design, Fifth Edition, Comprehensive》第11章中的内容。

### 程序员定义的类

在继续学习本章之前，你应该花点时间回顾本书第1章以及《Programming Logic and Design, Fifth Edition, Comprehensive》第11章中介绍的面向对象术语（`class`、`attribute`和`method`）。

你在本书中一直在使用预定义的类、对象和方法。例如，你使用了`ifstream`和`ofstream`类的open方法来打开输入和输出文件。在本节中，你将学习如何创建自己的类，包含你选择的属性和方法。在编程术语中，由程序员创建的类被称为**程序员定义的类**或**自定义类**。

回顾一下，请记住过程式编程侧重于：1）声明数据；2）定义与数据分离的函数；3）调用这些函数对数据进行操作。这是你在本书第1章到第9章一直使用的编程风格。面向对象编程也关注数据以及操作这些数据所需的函数。然而，面向对象编程与过程式编程有很大不同。数据和函数（在面向对象编程中称为“方法”）被**封装**在类中。单个对象作为类的实例被创建。程序通过向对象传递消息来告诉它执行任务。这样的消息包含一个执行类方法的指令。然后，类方法操作数据（数据是对象本身的一部分）。

### 创建程序员定义的类

在《Programming Logic and Design, Fifth Edition, Comprehensive》第11章中，你学习了Employee类的伪代码。该伪代码如图10-1所示。实现Employee类的C++代码如图10-2所示。

```text
1    class Employee
2        string lastName
3        num hourlyWage
4        num weeklyPay
5
6        void setLastName(string name)
7            lastName = name
8            return
9
10       void setHourlyWage(num wage)
11           hourlyWage = wage
12           calculateWeeklyPay()
13           return
14
15       string getLastName()
16       return lastName
17
18       num getHourlyWage()
19       return hourlyWage
20
21       num getWeeklyPay()
22       return weeklyPay
23
24       void calculateWeeklyPay()
25           num WORK_WEEK_HOURS = 40
26           weeklyPay = hourlyWage * WORK_WEEK_HOURS
27       return
28   endClass
```

**图10-1** Employee类的伪代码

```cpp
1    // Employee.cpp
2    #include <string>
3    using namespace std;
4    class Employee
5    {
6    public:
7        void setLastName(string);
8        void setHourlyWage(double);
9        double getHourlyWage();
10       double getWeeklyPay();
11       string getLastName();
12   private:
13       string lastName;
14       double hourlyWage;
15       double weeklyPay;
16       void calculateWeeklyPay();
17   }; // You end a class definition with a semicolon
18
19   void Employee::setLastName(string name)
20   {
21       lastName = name;
22       return;
23   }
24   void Employee::setHourlyWage(double wage)
25   {
26       hourlyWage = wage;
27       calculateWeeklyPay();
28       return;
29   }
30   string Employee::getLastName()
31   {
32       return lastName;
33   }
34   double Employee::getHourlyWage()
35   {
36       return hourlyWage;
37   }
38   double Employee::getWeeklyPay()
39   {
40       return weeklyPay;
41   }
42   void Employee::calculateWeeklyPay()
43   {
44       const int WORK_WEEK_HOURS = 40;
45       weeklyPay = hourlyWage * WORK_WEEK_HOURS;
46       return;
47   }
```

**图10-2** 用C++实现的Employee类

查看图10-1中伪代码的第1行，你会看到创建类时首先要指定它是一个类。查看图10-2中的C++代码，你会看到第1行是注释，第2行是预处理指令`#include <string>`，第3行是using语句`using namespace std;`。（你在本书第1章学习了预处理指令和using语句。）接下来是第4行Employee类的类声明。它以关键字class开头，指定后面是一个C++类。第5行的左花括号和第17行的右花括号标记了类的开始和结束。

注意第17行的右花括号后面有一个分号。这个分号是*绝对必要的*，因为它是创建类的C++语法的一部分。省略这个分号是一个常见错误。

### 向类添加属性

下一步是定义Employee类中包含的属性（数据）。如图10-1中伪代码的第2、3、4行所示，该伪代码类中有三个属性：string lastName、num hourlyWage和num weeklyPay。

图10-2中的第13、14、15行将这些属性包含在Employee类的C++版本中。注意在C++代码中，hourlyWage和weeklyPay使用double数据类型定义，lastName定义为string。另外，注意所有三个属性都包含在类的**private**部分中。private部分通过在第12行包含关键字private后跟冒号来定义。正如《Programming Logic and Design, Fifth Edition, Comprehensive》中所解释的，这意味着数据不能被不属于该类的任何方法（函数）访问。使用Employee类的程序必须使用属于该类的方法来访问私有数据。

