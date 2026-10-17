
13. 可以将一个指针变量的值赋值给另一个相同类型的指针变量。

14. 在程序运行期间创建的变量被称为动态变量。

# 第 14 章：指针、类、虚函数和抽象类

- 16. `new` 运算符用于创建动态变量。

- 17. `delete` 运算符用于释放动态变量所占的内存。

- 18. 在 C++ 中，`new` 和 `delete` 都是保留字。

- 19. `new` 运算符有两种形式：创建一个单个动态变量和创建一个动态变量数组。

- 20. 如果 `p` 是 `int` 类型的指针，语句：

```cpp
p = new int;
```

在内存中某处分配类型 `int` 类型的存储空间，并将分配的存储地址存储在 `p` 中。

- 22. 如果 `p` 是 `int` 类型的指针，语句：

```cpp
delete p;
```

释放 `p` 所指向的内存。

- 23. 数组名是一个常量指针。它始终指向同一个内存位置，即数组第一个元素的位置。

- 24. 要创建一个动态数组，会使用创建动态变量数组的 `new` 运算符形式。例如，如果 `p` 是 `int` 类型的指针，语句：

```cpp
p = new int[10];
```

创建一个包含 10 个 `int` 类型元素的数组。数组的基地址存储在 `p` 中。我们称 `p` 为动态数组。

- 25. 可以使用数组表示法访问动态数组的元素。例如，`p*` 是一个包含 10 个元素的动态数组。那么，`p[0]` 指数组的第一个元素，`p[1]` 指第二个元素，特别是 `p[i]` 指的是数组的第 `(i+1)` 个元素，依此类推。

- 26. 在程序执行期间创建的数组被称为动态数组。

- 27. 如果 `p` 是动态数组，语句：

```cpp
delete p;
```

释放 `p` 所占的内存——即 `p` 的各个元素。

- 28. C++ 允许程序创建多维数组。

- 29. 在语句 `int **board;` 中，变量 `board` 是一个指向指针的指针。

- 30. 在浅拷贝中，两个或多个相同类型的指针指向同一个内存空间；也就是说，它们指向相同的数据。

- 31. 在深拷贝中，两个或多个相同类型的指针拥有它们自己的数据拷贝。

- 32. 如果一个类有析构函数，每当类对象离开作用域时，析构函数就会自动执行。

- 33. 如果类有指针成员变量，内置的赋值运算符将提供数据的浅拷贝。

- 34. 当对象通过另一个对象的值进行声明并初始化，以及当对象作为参数按值传递时，会执行拷贝构造函数。

- 35. C++ 允许用户将派生类对象传递给基类的形参参数。

- 36. 虚函数的绑定发生在执行时，而不是编译时，这被称为动态绑定或运行时绑定。

- 37. 在 C++ 中，虚函数是使用保留字 `virtual` 声明的。

- 38. 如果一个类包含一个或多个纯虚函数，则该类是抽象类。

- 39. 因为抽象类不是一个完整的类——因为它（它的实现不包含某些函数的定义）——你不能创建该类的对象。

- 40. 除了纯虚函数外，抽象类还可以包含实例变量、构造函数和非纯虚的函数。然而，抽象类必须提供构造函数和非纯虚函数的定义。

- 41. 运算符 `*` 的地址可以用于返回类私有成员变量的地址。

## 练习

1. 判断下列陈述对错。

a. 在 C++ 中，`pointer` 是保留字。

b. 在 C++ 中，指针变量使用 `pointer` 单词声明。

c. 语句 `delete p;` 释放指针变量本身。

d. 语句 `delete p;` 释放 `p` 所向的动态变量。

e. 给定声明：

```cpp
int list[10];
int *p;
```

语句：

```cpp
p = list;
```

在 C++ 中是有效的。

f. 给定声明：

```cpp
int *p;
```

语句：

```cpp
p = new int[50];
```

动态分配了一个包含 50 个 `int` 类型元素的数组，且 `p` 包含该数组的地址。

g. 运算符 `*` 返回其操作数的地址和值。

h. 如果 `p` 是指针变量，那么语句 `p = p * 2;` 是有效的。

2. 给定声明：

```cpp
int x;
int *p;
int *q;
```

标记下列陈述有效或无效。如果语句无效，解释原因。

a. `p = q;`

b. `*p = 5;`

c. `p = x;`

d. `*p = *q;`

e. `q = &x;`

f. `*p = q;`

3. 解释如何使用运算符 `*` 处理指针。

4. 考虑以下语句：

```cpp
int *p, q;
```

该语句可能导致什么类型的误解？

5. 下面 C++ 代码的输出是什么？

```cpp
int x;
int y;
int *p = &x;
int *q = &y;
p = 35;
*p = 98;
*p = *q;
cout << x << " " << y << endl;
cout << *p << " " << *q << endl;
```

6. 下面 C++ 代码的输出是什么？

```cpp
int x;
int y;
int *p = &x;
int *q = &y;
x = 35;
y = 46;
p = q;
*p = 78;
cout << x << " " << y << endl;
cout << *p << " " << *q << endl;
```

给定声明：

```cpp
int num = 6;
int *p = &num;
```

下列哪个语句增加了 `num` 的值？

a. `p++;`

b. `(*p)++;`

c. `num++;`

d. `(*num)++;`

7. 下面代码的输出是什么？

```cpp
int *p;
int *q;
p = new int;
q = p;
*p = 46;
*q = 39;
cout << *p << " " << *q << endl;
```

8. 下面代码的输出是什么？

```cpp
int *p;
int *q;
p = new int;
*p = 43;
q = p;
*q = 52;
p = new int;
*p = 78;
q = new int;
*q = *p;
cout << *p << " " << *q << endl;
```

9. 下面代码的输出是什么？

```cpp
int *p;
int *q;
p = new int;
q = new int;
*p = 27;
q = 35;
cout << *p << " " << *q << endl;
q = p;
*q = 73;
cout << *p << " " << *q << endl;
```

10. 下面 C++ 代码的输出是什么？

```cpp
int *p;
int *q;
p = new int;
q = new int;
*p = 27;
q = 35;
cout << *p << " " << *q << endl;
q = p;
*q = 73;
cout << *p << " " << *q << endl;
p = new int;
*p = 36;
q = 42;
cout << *p << " " << *q << endl;
```

11. 下面 C++ 代码的输出是什么？

```cpp
int *p;
int *q;
p = new int;
q = new int;
*p = 27;
*q = 35;
cout << *p << " " << *q << endl;
*q = *p;
*p = 73;
cout << *p << " " << *q << endl;
p = new int;
*p = 36;
q = p;
cout << *p << " " << *q << endl;
```

12. 下面代码哪里有问题？

```cpp
int *p;
int *q;
p = new int;
*p = 43;
q = p;
*q = 52;
delete q;
cout << *p << " " << *q << endl;
```

13. 下面代码的输出是什么？

```cpp
int x;
int *p;
int *q;
p = new int[10];
q = p;
*p = 4;
for (int j = 0; j < 10; j++) {
    x = *p;
    p++;
    *p = x + j;
}
for (int k = 0; k < 10; k++) {
    cout << *q << " ";
}
cout << endl;
```

14. `new` 运算符的作用是什么？

15. `delete` 运算符的作用是什么？

16. 下面代码的输出是什么？

```cpp
int *secret;
int j;

secret = new int[10];
secret[0] = 10;
for (j = 1; j < 10; j++)
    secret[j] = secret[j - 1] + 5;
for (j = 0; j < 10; j++)
    cout << secret[j] << "";
```

17. 考虑以下语句：

```cpp
int *num;
```

a. 编写将 `num` 初始化为包含10个整数数组的 C++ 语句。

b. 编写从标准输入向数组输入数据的 C++ 语句。

c. 编写释放 `num` 所占内存的 C++ 语句。

18. 考虑以下语句：

```cpp
int *secret;
int j;
```

a. 编写动态创建一个10个整数数组的 C++ 语句。

b. 编写从标准输入向数组输入数据的 C++ 代码。

c. 编写释放 `secret` 所占内存空间的 C++ 语句。

19. 解释浅拷贝和深拷贝之间的区别。

20. 下面代码哪里有问题？

```cpp
int *p;
int *q;

p = new int[5];
p[0] = 2;

for (int i = 1; i < 5; i++)
    p[i] = p[i - 1] + 2;

q = p;

for (int j = 0; j < 5; j++)
    cout << q[j] << " ";
cout << endl;
```

```cpp
void classA::print() const
{
    cout << "ClassA x: " << x << endl;
}

void classA::doubleNum()
{
    x = 2 * x;
}

classA::classA(int a)
{
    x = a;
}

class classB : public classA
public:
    void print() const;
    void doubleNum();
    classB(int a = 0, int b = 0);
private:
    int y;
};

void classB::print() const
{
    classA::print();
    cout << "ClassB y: " << y << endl;
}

void classB::doubleNum()
{
    classA::doubleNum();
    y = 2 * y;
}

classB::classB(int a, int b)
    : classA(a)
{
    y = b;
}

以下函数的输出是什么？
int main ()
{
    classA *ptrA;
    classA objectA(2);
    classB objectB(3, 5);

ptrA = &objectA;
ptrA->doubleNum();
ptrA->print();
cout << endl;

ptrA = &objectB;
ptrA->doubleNum();
ptrA->print();
cout << endl;

return 0;
}
```

856 | 第 14 章：指针、类、虚函数、抽象类

27. 如果将 `classA` 的定义替换为以下定义，那么练习 26 中 `main` 函数的输出是什么？

```cpp
class classA
{
public:
    virtual void print() const;
    virtual void doubleNum();
    classA(int a = 0);

private:
    int x;
}
```

28. 编译时绑定（compile-time binding）和运行时绑定（run-time binding）之间有什么区别？

29. 有一个所有成员函数都是虚函数的抽象类是合法的吗？

30. 考虑以下 `studentType` 类的定义：

```cpp
public studentType : public personType
{
public:
    void print();
    void calculateGPA();
    void setID(long id);
    void setCourses(const string c[], int noOfCourses);
    void setGrades(const char c[], int noOfCourses);

    void getID();
    void getCourses(string c[], int noOfCourses);
    void getGrades(char c[], int noOfCourses);
    void studentType(string fName = "", string lastName = "",
        long id, string c[] = NULL,
        char c[] = NULL, int noOfCourses = 0);

private:
    long studentId;
    string courses[6];
    char coursesGrade[6];
    int noOfCourses;
}
```

重写 `studentType` 类的定义，使得 `print` 和 `calculateGPA` 函数成为纯虚函数。

- 31. 假设在本章的示例 14-8 中给出了 `employeeType`、`fullTimeEmployee` 和 `partTimeEmployee` 类的定义。以下语句是合法的？

- a. `employeeType tempEmp;`

- b. `fullTimeEmployee newEmp();`

- c. `partTimeEmployee pEmp("Molly", "Burton", 101, 0.0, 0);`

# 编程练习

- 1. 使用动态数组重做第 9 章的编程练习 5。

- 2. 使用动态数组重做第 9 章的编程练习 6。

- 3. 使用动态数组重做第 9 章的编程练习 7。你向用户询问候选人的数量，并创建相应的数组来存储数据。

- 4. 第 9 章中的编程练习 11 解释了如何相加大整数数组。然而，该程序可以实现大整数的相加。设计一个 `largeInteger` 类，使其能够执行加法、减法、乘法和比较操作。该类应包含构造函数、访问器、设置器、初始化和打印函数。

- 5. 假设在本章中给出了 `employeeType`、`fullTimeEmployee` 和 `partTimeEmployee` 类的定义。以下哪些是合法的？

在第12章中，你学习了如何使用C++ 类将数据以及对该数据的操作组合在单个实体中。将数据和对数据的操作相结合的能力被称为**封装**。它是面向对象设计（OOD）的第一原则。第12章定义了抽象数据类型（ADT），并描述了C++ 类如何实现 ADT。第13章讨论了如何通过继承机制从现有类派生新类。继承是面向对象设计的第二个原则，它鼓励代码的重用。

本章涵盖了运算符重载和模板。模板允许程序员为相关的函数和类编写泛型代码。我们还将通过使用类型（称为函数模板）来简化（在第7章引入的）函数重载。

## 为什么需要运算符重载

第12章定义并实现了 `clockType` 类。它还向你展示了可以使用 `clockType` 类来表示程序中的一天时间。让我们回顾 `clockType` 类的一些特征。

考虑以下语句：

```
myClock(8, 23, 34);
yourClock(4, 5, 30);
```

第一条语句将 `myClock` 声明为 `clockType` 类型的对象，并将 `myClock` 的成员变量 `hr`、`min` 和 `sec` 分别初始化为 8、23 和 34。第二条语句将 `yourClock` 声明为 `clockType` 类型的对象，并将 `yourClock` 的成员变量 `hr`、`min` 和 `sec` 初始化为 4、5 和30。

现在考虑以下语句：

```
myClock.printTime();

myClock.incrementSeconds();

myClock.equalTime(yourClock);
```

第一条语句以 `hr:min:sec` 的形式打印 `myClock` 的值。第二条语句将 `myClock` 的值增加一秒。第三条语句检查 `myClock` 的值是否与 `yourClock` 的值相同。

这些语句可以完成工作。然而，如果我们使用插入运算符 `<<` 输出 `myClock` 的值，使用递增运算符 `++` 将 `myClock` 的值加一秒，并使用关系运算符进行比较，我们可以大大增强 `clockType` 类的活性。具体来说，我们更倾向于使用以下语句代替之前的语句：

```
cout << myClock;
```

```
myClock++;
```

```
if (myClock == yourClock)
```
