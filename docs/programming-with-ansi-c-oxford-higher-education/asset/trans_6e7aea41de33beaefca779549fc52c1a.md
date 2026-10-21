

## 80 使用 ANSI C++ 编程

> 注意
> 从技术上讲，FirstStudent.PrintDetails() 等同于 PrintDetails(&FirstStudent)，SecondStudent.PrintDetails() 等同于 PrintDetails(&SecondStudent)。指向调用类对象的指针将传递给函数。以这种方式传递的指针（第一种情况下是 &FirstStudent，第二种情况下是 &SecondStudent）称为 this 指针。我们实际上可以通过关键字 this 来指代该指针。

将指针传递给调用对象有助于为所有对象保留函数的单一副本。我们需要理解在所有对象之间共享成员函数的重要性。无论我们创建多少个对象，为成员函数的单一副本分配内存就足够了。此外，为每个对象分别准备一组完全相同的成员函数是没有意义的。

> 注意
> 即使我们定义了 100 个学生对象，PrintDetails() 函数也只有一个副本。同样，即使我们有 0 个学生对象，PrintDetails() 函数仍然有一个副本。另一方面，如果我们有 0 个学生对象副本，那么就有 0 个学号；如果我们有 100 个学生对象副本，就有 100 个学号，每个对象对应一个。因此，在定义类时，为函数分配内存；而在定义对象时，为非静态数据成员分配内存。

## 3.6 C++ 中结构体（struct）和类（class）的区别

在 C++ 中，结构体（structure）和类（class）之间的区别是模糊的。它们之间只有一个（看似）微不足道的区别。我们已经了解了 public 和 private 访问说明符；在定义类时，我们可以省略它们，如程序 3.3 所示。

## 程序 3.3 struct 与 class

```cpp
// StructClass.cpp
#include <iostream>
#include <string>
using namespace std;

class employee
{
/* Access specifier is omitted here, so it is private by default */
int EmpID;
string Name;
string Designation;
int Department;
int Salary;

public:
void InsertDetails()
{
cout << "Insert employee ID";
cin >> EmpID;
cout << "Insert name";
cin >> Name;
cout << "Insert designation";
cin >> Designation;
cout << "Insert department";
cin >> Department;
cout << "Insert salary";
cin >> Salary;
}
}
```

```
void DisplayDetails()
{
    cout << EmpID << "\n";
    cout << Name << "\n";
    cout << Designation << "\n";
    cout << Department << "\n";
    cout << Salary << "\n";
}
};

void main()
{
    employee Robin;
    Robin.InsertDetails();
    Robin.DisplayDetails();
}
```

> 注意 当我们定义一个类时，如果没有将数据成员写在任何访问说明符之下，它们默认被视为 private。

## 程序工作原理

如果对这个程序稍作修改，将第四行的 class employee 替换为 struct employee，程序运行结果完全相同。然而，有一个差异，目前还看不出来。在两个程序中（第一个程序中的 employee 是类，第二个程序中的 employee 是结构体）添加下面一行代码。main 函数现在变为如下形式：

```
void main()
{
    employee Robin;
    Robin.InsertDetails();
    Robin.DisplayDetails();
    // The following line is added
    Robin.EmpID = 10;
    /* This line will not be compiled in the case of class,
    but it will work fine in a structure */
}
```

第一个程序无法编译，但第二个程序可以。struct 定义中的默认行为不同。在结构体中，没有访问说明符名称的属性被视为 public，而在类中则是 private。这里，第一个程序中的 EmpID 是 private，而在第二个程序中它是 public。第二个程序的语句可以访问它，而第一个程序的语句不能，因此第二个程序可以编译。理解为什么类中默认是 private 并不难。除非显式指定（即在 public 下定义），否则类中定义的一切都应被视为 private。

结构体的行为方式与类相同，除了默认数据类型上看似微不足道的差异外，这看起来可能不合逻辑。结构体之所以有这样的行为，原因在于与 C 语言的向后兼容性。考虑以下借用自 C 语言的代码：

```
struct Evaluator
{
```

> 对于类，数据成员和成员函数默认是 private（除非另有声明），而对于结构体，其成员默认是 public。

```
char Name[30];
char Address[100];
}
```

如果在 C++ 中把结构体做得与类相似（即未提供访问说明符时默认为 private），那么想想这段代码会发生什么。程序将无法执行如下语句：

```
Evaluator MrBaxi;
Strcpy(MrBaxi.Name, "Chandrakant Baxi");
```

它能够访问 Name 这一事实表明 Name 是一个 public 数据成员。通过保持默认为 public，C++ 的结构体仍然与 C 的结构体向后兼容。C++ 的惯例是：当我们需要一个类时使用 class，当我们需要一个类似 C 的结构体时使用 struct。

> 注意 如果 struct 默认不是 public，那么复制到 C++ 程序中的 C 代码将无法工作。C++ 的设计者需要向后兼容性，并希望 C 程序在被 C++ 编译器编译时只需做最少的修改即可运行。

## 3.7 联合体（union）与类的区别

在 C++ 中，联合体可以拥有访问说明符，并且可以同时定义数据和函数；与结构体类似，它们的默认访问说明符是 public。（原因与第 3.6 节讨论的相同。）联合体有一个重要特性：所有数据元素（但成员函数除外）共享同一内存位置。它们还必须保持与 C 语言中联合体的兼容性。

C++ 定义了一种 C 语言中没有的特殊联合体类型，即匿名联合体（anonymous union）。在这种联合体中，定义时不会提供联合体的名称。这向编译器表明数据元素共享同一内存位置。匿名联合体的成员可以直接访问，无需定义联合体类型的对象，也无需使用点运算符。以下是对所讨论的联合体相关要点的总结。

- 1. 总的来说，C++ 中的联合体与 C 中相同，可能还会添加成员函数。
- 2. 所有数据成员与 C 一样共享同一内存。
- 3. 默认访问说明符与结构体一样是 public。
- 4. 在 C++ 中，可以定义一个没有名称的联合体，即匿名联合体。

程序 3.4 演示了联合体的类型。

## 程序 3.4 联合体与类

```
//UnionExample.cpp
#include <iostream>
using namespace std;

union IntChar
{
    void SetValue()
    // Without access specifier, treated as public
    {
        CharView[0]=0;  // 00000000
```

```
CharView[1]=1;  // 00000001
CharView[2]=0;  // 00000000
CharView[3]=0;  // 00000000
}
/* This value is equivalent to 00000000 00000000 00000001 00000000, that is, 2^8 */
void GetValue()
{
    cout << IntView; // displays 256, that is, 2^8
}
private:
    unsigned int IntView;
    char CharView[4];
    /* These two data members share the same memory location */
};
void main()
{
    IntChar IC;
    IC.SetValue();
    IC.GetValue();

    // The following is an anonymous union

    union
    {
        int AnoInt;
        char AnoChar[4];
    };
    AnoInt = 65;    // AnoInt is accessed directly
    cout << "\n The AnoChar 1st element is" << AnoChar[0];
    cout << "\n The AnoChar 2nd element is" << AnoChar[1];
    cout << "\n The AnoChar 3rd element is" << AnoChar[2];
    cout << "\n The AnoChar 4th element is" << AnoChar[3] << endl
}
```

## 输出

```
256
The AnoChar 1st element is A
The AnoChar 2nd element is
The AnoChar 3rd element is
The AnoChar 4th element is
```

## 程序工作原理

IntValue 数据成员的值打印为 256，即 2^8。AnoChar[0] 数据成员打印 A（char 值 65），其余打印 null（char 值 0）。以下是关于程序 3.4 需要注意的一些要点：

- 1. 函数 SetValue() 和 GetValue() 没有在任何访问说明符下定义，因此被视为 public。
- 2. AnoChar 和 AnoInt 可以在不使用点表示法的情况下访问。可以看到，当 AnoInt 的值设为 65 时，AnoChar[0] 的值是“A”。这是一个简单的例子，说明 AnoChar 和 AnoInt 实际上共享同一内存位置。

> 注意 匿名联合体定义在主联合体内部，也就是说，它是一个局部联合体。如果我们想定义全局匿名联合体，在 C++ 中必须将其定义为 static。普通联合体则不是这样。在程序 3.4 中，联合体 IntChar 被定义为全局的。

