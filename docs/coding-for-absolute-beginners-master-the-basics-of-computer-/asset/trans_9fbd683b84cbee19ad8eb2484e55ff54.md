
在程序运行期间。这些语句在代码中从上到下依次执行，以便完全满足程序逻辑。

程序并不依赖于语句的线性顺序，为此 C++ 提供了特定的流程控制语句。

## C++ 中的流程控制语句

- 1. If else 语句
- 2. For 循环
- 3. Do while 循环
- 4. Break 和 Continue
- 5. Switch 语句
- 6. Goto 语句

### If 语句

在 C++ 编程中，当程序内有多条语句或多种情况需要执行时，会使用 if 语句。If 语句的语法表明，仅当给定语句为真时才会执行括号中的内容，否则假语句会被自动忽略。

```cpp
if(condition){
        statement;
}
```

### If 语句的流程图

用于说明 C++ 中 If 语句的示例程序：

```cpp
#include <iostream>
using namespace std;
int main(){
    int marks=80;
    if( marks < 100 ){
        cout<<"Marks are less than 100";
    }

    if(marks > 100){
        cout<<"Marks are greater than 100";
    }
    return 0;
}
```

### 嵌套 If 语句

在 C++ 中，语句中的语句称为嵌套 If 语句。例如：

```cpp
if(condition_1) {
    Statement1;
    if (condition_2) {
        Statement2;
    }
}
```

### If Else 语句

```cpp
if(condition_1) {
    Statement;
}
else if (condition_2) {
    Statement;
}
```

### Switch Case

在 C++ 编程中，当程序中给出多个条件，并且需要根据所提供的条件执行操作时，会使用 Switch Case 语句。Break 和 Continue 操作也是 Switch 语句的重要组成部分。C++ 中 Switch Case 的语法如下：

```cpp
#include <iostream>
using namespace std;
int main(){
    int num=10;
    switch(num+5) {
        case 1:
        cout<<"Case1: Value is: "<<num<<endl;
        case 2:
        cout<<"Case2: Value is: "<<num<<endl;
        case 3:
        cout<<"Case3: Value is: "<<num<<endl;
        default:
        cout<<"Default: Value is: "<<num<<endl;
    }
    return 0;
}
```

### Go To 语句

C++ 中的 goto 语句用于改变程序的执行，并将控制权转移到同一程序内另一个带标签的语句。

goto 语句的语法：

```cpp
goto label;
```

## 循环和函数

### 循环

在 C++ 编程语言中，循环语句用于执行特定代码块一定次数的迭代，直到满足所提供的条件。由于循环允许程序员一次执行多项任务，循环语句会执行函数中的第一条语句，并按需继续执行下一条。

循环的类型

- **While 循环：** 在所提供的条件为真时重复执行语句，并在执行循环体之前重新检查。
- **Do While 循环：** 在循环执行时检查条件。
- **For 循环：** 多次执行特定语句，并且也管理循环变量。
- **嵌套循环：** 一个循环内包含多个循环。

循环可以通过不同的控制语句执行，例如 Break 语句、Continue 语句和 goto 语句。

### 函数

函数负责组合不同的代码段，并将它们一起执行以完成给定操作。C++ 编程语言中的两种主要函数类型包括库函数和用户定义函数。库函数在 C++ 中是预定义的，而用户定义函数由程序员自己创建。

要定义函数，我们可以使用以下语法：

```cpp
Return_type function_name(parameter list) {
    Function body
}
```

min() 函数的示例代码：

```cpp
int min(int num1, int num2) { //function declaration
    // local variable declaration
    int result;

    if (num1 < num2)
        result = num1;
    else
        result = num2;

    return result;
}
```

### 函数调用

要在 C++ 中调用函数，我们可以使用以下方法：

- 按引用调用。
- 按值调用。
- 按指针调用。

### 函数重载

当两个或多个函数具有相同名称但参数不同时，此过程称为函数重载。C++ 中函数重载的语法如下所示：

```cpp
void sameFunction(int a);
int sameFunction(float a);
void sameFunction(int a, double b);
```

## 数组、字符串、指针和引用

### 数组

数组在编程语言中经常使用，因为它们允许我们处理大量相同类型的数据。通常，数组被称为数据的集合，其中包含固定数量的值。

在 C++ 中声明数组的语法：

```cpp
datatype arrayName[arraySize];
```

初始化：

```cpp
int age[5] = {15, 20, 25, 30, 35};
```

使用数组求 10 个数字之和的 C++ 示例程序：

```cpp
#include <iostream>
using namespace std;
int main()
{
        int numbers[10], sum = 0;

        cout << "Enter 10 numbers: ";

        for (int i = 0; i < 10; ++i)
        {
                cin >> numbers[i];
                sum += numbers[i];
        }
        cout << "Sum = " << sum << endl;
        return 0;
}
```

### 字符串

字符串被称为字符的集合。在 C++ 编程中，常用的两种字符串类型是 C 字符串和标准 C++ 库字符串类。

以下语法可用于定义字符串：

```cpp
char str[] = "Programming";
```

### 指针

指针被定义为一个变量，其值被视为另一个变量的地址。要在 C++ 编程语言中使用指针，我们需要定义一个指针变量，并将某个变量的地址赋给指针。之后，我们可以通过指针变量中给出的地址访问该值。

整个操作通过使用一元运算符 * 来完成。以下是 C++ 编程中最常用的指针：

- 空指针
- 指针数组
- 指向指针的指针
- 将指针传递给函数
- 从函数返回指针

## 面向对象的 C++

### 类和对象

C++ 语言中的面向对象编程是创建对象并执行多种操作的一种简单方式。首先，在创建对象之前，我们需要定义一个类，为此可以使用下面提到的语法：

```cpp
class className
{
        //data
};
```

类可以定义为 Public、Private 或 Protected，以便数据成员只能在程序中特定访问。

示例代码：

```cpp
class student
{

        private:

                char name[20];

                int  rollNo;

                int  total;

                float perc;

        public:

                //member function to get student's details

                void getDetails(void);

                //member function to print student's details

                void putDetails(void);
};
```

### 继承和多态

在编写实现继承的程序时，我们可以考虑 C++ 中基类和派生类的概念。由于一个类可以从一个或多个类派生，我们也可以从不同的基类继承函数和数据。

派生类可以访问其基类的所有非私有成员。除了从基类继承属性外，用户还可以从现有类创建新类。C++ 中继承的语法定义如下：

```cpp
class A  // base class
{
        ..........
};
class B : access_specifier A  // derived class
{
        ..........
};
```

### 访问说明符

在 C++ 中，访问说明符用于确定类成员在该类之外的可用性限制。Private、Protected 和 Public 是定义类成员可访问级别的主要访问说明符。

创建类时使用 private 访问说明符，使得基类的 protected 和 public 数据成员成为派生类的 private 成员，而基类的 private 成员仍然保持为 private。

在 protected 访问说明符中，基类的 public 和 protected 数据成员成为派生类的 protected 成员。基类的 private 成员仍然不可访问。

使用 public 访问说明符时，基类的 public 数据成员成为派生类的 public 成员。protected 成员在派生类中成为 protected，而基类的 private 成员仍然不可访问。

在 C++ 中使用访问说明符的语法：

```cpp
class MyClass {  // class
```
