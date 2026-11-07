
```cpp
personType& setFirstName(string first);
    //Function to set the first name.
    //Postcondition: firstName = first
    //               After setting the first name, a reference
    //               to the object, that is, the address of the
    //               object, is returned.

personType& setLastName(string last);
    //Function to set the last name.
    //Postcondition: lastName = last
    //               After setting the last name, a reference
    //               to the object, that is, the address of the
    //               object, is returned.

string getFirstName() const;
    //Function to return the first name.
    //Postcondition: The value of firstName is returned.

string getLastName() const;
    //Function to return the last name.
    //Postcondition: The value of lastName is returned.

personType(string first = "", string last = "");
    //Constructor
    //Sets firstName and lastName according to the parameters.
    //Postcondition: firstName = first; lastName = last

private:
    string firstName; //variable to store the first name
    string lastName;  //variable to store the last name
};
```

注意，在类 personType 的这个定义中，我们用一个带默认参数的构造函数替换了默认构造函数和带参数的构造函数。

函数 print、setName、getFirstName、getLastName 以及构造函数的定义与之前相同（参见示例 11–9）。函数 setFirstName 和 setLastName 的定义如下：

```cpp
personType& personType::setLastName(string last)
{
    lastName = last;

    return *this;
}
```

```cpp
personType& personType::setFirstName(string first)
{
    firstName = first;

    return *this;
}
```

下面的程序演示如何使用类 personType。（我们假设该类的定义位于文件 personType.h 中。）

```cpp
//Test Program: class personType

#include <iostream>
#include <string>
#include "personType.h"

using namespace std;

int main()
{
    personType student1("Angela", "Smith");            //Line 1

    personType student2;                                //Line 2

    personType student3;                                //Line 3

    cout << "Line 4 -- Student 1: ";                    //Line 4
    student1.print();                                   //Line 5
    cout << endl;                                       //Line 6

    student2.setFirstName("Shelly").setLastName("Malik"); //Line 7

    cout << "Line 8 -- Student 2: ";                    //Line 8
    student2.print();                                   //Line 9
    cout << endl;                                       //Line 10

    student3.setFirstName("Chelsea");                   //Line 11

    cout << "Line 12 -- Student 3: ";                   //Line 12
    student3.print();                                   //Line 13
    cout << endl;                                       //Line 14

    student3.setLastName("Tomek");                      //Line 15

    cout << "Line 16 -- Student 3: ";                   //Line 16
    student3.print();                                   //Line 17
    cout << endl;                                       //Line 18

    return 0;
}
```

### 示例运行结果：

```cpp
Line 4 -- Student 1: Angela Smith
Line 8 -- Student 2: Shelly Malik
Line 12 -- Student 3: Chelsea
Line 16 -- Student 3: Chelsea Tomek
```

第 1、2、3 行的语句分别声明并初始化对象 student1、student2 和 student3。对象 student2 和 student3 被初始化为空字符串。第 5 行的语句输出 student1 的值（参见示例运行结果中的第 4 行，它包含第 4、5、6 行的输出）。第 7 行的语句按如下方式工作。在语句：

```cpp
student2.setFirstName("Shelly").setLastName("Malik");
```

首先，表达式：

```cpp
student2.setFirstName("Shelly")
```

会被执行，因为点运算符的结合性是从左到右。该表达式将名字设置为 "Shelly"，并返回对象（即 student2）的引用。因此，接下来执行的表达式是：

```cpp
student2.setLastName("Malik")
```

它将 student2 的姓氏设置为 "Malik"。第 9 行的语句输出 student2 的值。第 11 行的语句将对象 student3 的名字设置为 "Chelsea"，并忽略返回的值。第 13 行的语句输出 student3 的值。注意第 12 行的输出。输出只显示了名字，而没有显示姓氏，因为我们尚未设置 student3 的姓氏。student3 的姓氏仍为空，这是第 3 行声明 student3 时由该语句设置的。接下来，第 15 行的语句设置 student3 的姓氏，第 17 行的语句输出 student3 的值。

## 类的友元函数

类的**友元函数**是该类的非成员函数，但可以访问该类的所有成员（公有或非公有）。要使一个函数成为某个类的友元，保留字 `friend` 应放在函数原型之前（在类定义中）。单词 `friend` 只出现在类定义中的函数原型里，而不出现在友元函数的定义中。

考虑以下语句：

```cpp
class classIllusFriend
{
        friend void two(/*parameters*/);
        .
        .
        .
};
```

在类 `classIllusFriend` 的定义中，two 被声明为类 `classIllusFriend` 的友元。也就是说，它是类 `classIllusFriend` 的非成员函数。当你编写函数 two 的定义时，任何 `classIllusFriend` 类型的对象——无论是 two 的局部变量还是 two 的形式参数——都可以在函数 two 的定义中访问其私有成员。（示例 14–3 说明了这一概念。）此外，由于友元函数不是类的成员，其声明可以放在类的私有、受保护或公有部分中。不过，这类声明通常放在任何成员函数声明之前。

### `friend` 函数的定义

编写 `friend` 函数的定义时，函数头中 `friend` 函数的名称前不加类名和作用域解析运算符。另外，请记住，单词 `friend` 不出现在 `friend` 函数定义的头中。因此，前面的 `class` classIllusFriend 中函数 two 的定义为：

```cpp
void two(/*parameters*/)
{
    .
    .
    .
}
```

当然，我们会将 `friend` 函数的定义放在实现文件中。

下一节将说明当我们为特定类重载某些运算符时，成员函数与非成员函数（`friend` 函数）之间的区别。

下面的示例展示 `friend` 函数如何访问类的 `private` 成员。

### 示例 14-3

考虑以下类：

```cpp
class classIllusFriend
{
    friend void two(classIllusFriend cIFObject);

public:
    void print();
    void setx(int a);

private:
    int x;
};
```

在 `class` classIllusFriend 的定义中，two 被声明为友元函数。假设 `class` classIllusFriend 的成员函数定义如下：

```cpp
void classIllusFriend::print()
{
    cout << "In class classIllusFriend: x = " << x << endl;
}
```

```cpp
void classIllusFriend::setx(int a)
{
    x = a;
}
```

```cpp
void two(classIllusFriend cIFObject)                         //Line 1
{
    classIllusFriend localTwoObject;                         //Line 2

    localTwoObject.x = 45;                                   //Line 3

    localTwoObject.print();                                  //Line 4

    cout << "Line 5: In Friend Function two "
         << "accessing private member variable "
         << "x = " << localTwoObject.x
         << endl;                                            //Line 5

    cIFObject.x = 88;                                         //Line 6

    cIFObject.print();                                        //Line 7

    cout << "Line 8: In Friend Function two "
         << "accessing private member variable "
         << "x = " << cIFObject.x << endl;                   //Line 8
}
```

函数 two 包含一个形式参数 cIFObject 和一个局部变量 localTwoObject，二者的类型都是 classIllusFriend。在第 3 行的语句中，对象 localTwoObject 访问其私有成员变量 x，并将其值设置为 45。如果 two 未被声明为类 classIllusFriend 的友元函数，那么该语句将导致语法错误，因为对象不能直接访问其私有成员。类似地，在第 6 行的语句中，形式参数 cIFObject 访问其私有成员变量 x，并将其值设置为 88。同样，如果 two 未被声明为类 classIllusFriend 的友元函数，该语句将导致语法错误。第 5 行的语句通过直接访问 x 来输出 localTwoObject 的私有成员变量 x 的值。类似地，第 8 行的语句通过直接访问 cIFObject 的 x 来输出其值。函数 two 还通过使用函数 print 来打印 x 的值（参见第 4 行和第 7 行的语句）。

现在考虑以下函数 main 的定义：

```cpp
int main()
{
    classIllusFriend aObject;                                //Line 9

    aObject.setx(32);                                         //Line 10

    cout << "Line 11: aObject.x: ";                          //Line 11
    aObject.print();                                          //Line 12
    cout << endl;                                             //Line 13
}
```
