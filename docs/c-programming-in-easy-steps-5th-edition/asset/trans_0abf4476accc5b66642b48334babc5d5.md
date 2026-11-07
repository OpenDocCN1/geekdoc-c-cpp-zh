
普通整型变量、一个引用和两个指针

```cpp
int main()
{
    int num = 100, sum = 500;
    int& rNum = num;
    int* ptr = &num;
    void (*fn)(int& a, int* b) = add;
    // Add more statements here.
    return 0;
}
```

- 4. 在 main 函数中，插入语句以通过引用和指针输出第一个整型变量的值。

```cpp
cout << "Reference: " << rNum << endl;
cout << "Pointer: " << *ptr << endl;
```

- 5. 现在，将第二个整型变量赋给指针，并通过该指针输出其值，然后调用函数指针以输出这些变量值之和。

```cpp
ptr = &sum;
cout << "Pointer now: " << *ptr << endl;
fn(rNum, ptr);
```

- 6. 保存、编译并运行程序以查看输出。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_112_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_112_1.png)

C 程序员倾向于将 `&` 和 `*` 字符放在变量名之前，但在 C++ 中通常将它们放在数据类型之后——因为该特性是数据类型的属性，而不是名称的属性。

## 总结

- 数据存储在计算机内存中按顺序编号的地址内。
- **=** 运算符左侧的操作数是左值，右侧的操作数是右值。
- 右值只能出现在 **=** 运算符的右侧。
- 指针是一个变量，它存储另一个变量的内存地址——即它所指向的变量。
- **\*** 字符在指针声明中作为左值出现，表示该语句将创建一个指针变量。
- 一旦声明，**\*** 解引用运算符可用于引用指针所指向变量中的值。
- 指针算术可用于遍历存储在数组元素中的值。
- 变量按值传递给函数，而指针和引用按引用传递。
- 按引用传递允许接收函数直接操作调用函数中声明的变量。
- 可以将字符串值赋给 **char** 数据类型的指针，并使用指针名检索整个字符串。
- 指针数组中的每个元素都可以存储数据或指针。
- 引用不是变量，而只是变量的别名。
- **&** 字符在引用声明中作为左值出现，表示该语句将创建一个别名。
- **&** 引用运算符可用于引用存储在指针中的内存地址。
- 引用比指针更易使用，但与指针不同，引用必须始终在其声明中初始化，并且永远不能赋值为另一个变量。

## 创建类和对象

本章介绍封装和继承这两个主题——C++ 面向对象编程的前两个原则。

- 封装数据
- 创建对象
- 创建多个对象
- 初始化类成员
- 重载方法
- 继承类属性
- 调用基类构造函数
- 重写基类方法
- 总结

## 封装数据

类是一种数据结构，可以在单个实体中同时包含变量和函数。它们统称为类的“成员”，而函数称为类的“方法”。

从类外部对类成员的访问由类声明中的“访问说明符”控制。通常，这些说明符会拒绝对变量成员的访问，但允许访问能够存储和检索这些变量成员数据的方法。这种“数据隐藏”技术确保存储的数据安全地封装在类的变量成员中，并且是面向对象编程（OOP）的第一项原则。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_115_0.png)

类声明以 **class** 关键字开头，后跟一个空格，然后是由程序员指定的名称——遵循通常的 C++ 命名约定，但以大写字母开头。接下来是访问说明符和类成员，它们包含在一对花括号中。每个类声明都必须在右花括号后以分号结尾，因此类声明语法如下所示：

```cpp
class ClassName
{
    access specifier:
        member1;
        member2;
    access specifier:
        member3;
        member4;
};
```

访问说明符可以是 **public**、**private** 或 **protected** 中的任意一个关键字，用于指定其列出的成员的访问权限：

- 公有成员可从类可见的任何位置访问。
- 私有成员仅可由同一类的其他成员访问。
- 受保护成员仅可由同一类的其他成员以及从该类派生的类的成员访问。

默认情况下，所有类成员都具有私有访问权限——因此，类声明中未带访问说明符出现的任何成员都将具有私有访问权限。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_115_1.png)

使用 **protected** 访问说明符的派生类将在本章后面介绍。

任何现实世界中的对象都可以通过其属性和行为来定义。例如，狗具有年龄、体重和颜色等属性，以及它可以执行的行为，例如吠叫。C++ 中的类机制提供了一种在程序中创建虚拟狗对象的方式，其中类的变量成员可以表示其属性，而方法表示其行为：

```cpp
class Dog
{
    private: // The default access level.
        int age, weight;
```

```cpp
        string color;
public:
    void bark();
};
// ... Plus methods to store/retrieve data.
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_116_0.png)

虽然程序中的类无法完美模拟现实世界中的对象，但其目标是封装所有相关属性和行为。

重要的是要认识到，类声明只定义了一种数据结构——为了创建对象，必须声明该数据结构的“实例”。实现方式与声明常规 C++ 数据类型的实例完全相同：

```cpp
int num;        // Creates an instance named “num”.
                // of the regular C++ int data type.

Dog fido;       // Creates an instance named “fido”
                // of a programmer-defined Dog data structure.
```

或者，可以通过在类声明的右花括号与其最后的分号之间指定实例对象的名称来创建实例对象。通过指定以逗号分隔的对象名列表，可以用这种方式创建多个实例。例如，下面列出的类声明创建了 Dog 类的四个实例对象，名称分别为“fido”、“pooch”、“rex”和“sammy”。

```cpp
class Dog
{
    int age, weight;
    string color;
public:
    void bark();
    // ... Plus methods to store/retrieve data.
} fido, pooch, rex, sammy;
```

C++ 编程中的封装原则描述了将数据和功能组合在类成员中——Dog 类中的年龄、体重和颜色属性以及吠叫行为。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_116_1.png)

按照惯例，类名以大写字符开头，对象名以小写字符开头。

## 创建对象

为了向类的私有成员分配数据和从中检索数据，必须向类中添加特殊的公有访问器方法。这些方法是用于分配数据的“setter”方法和用于检索数据的“getter”方法。访问器方法通常以其所处理的变量命名，将首字母大写，并分别加上“set”或“get”前缀。例如，用于处理 age 变量的访问器方法可以命名为 `setAge()` 和 `getAge()`。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_117_0.png)

object.cpp

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀，开始一个新程序。

```cpp
#include <string>
#include <iostream>
using namespace std;
```

- 2. 声明一个名为“Dog”的类。

```cpp
class Dog
{
};
```

- 3. 在 Dog 类声明的花括号之间，声明三个 **private** 变量成员。

```cpp
int age, weight;
string color;
```

- 4. 在 **private** 变量之后，添加一个 **public** 访问说明符。

```cpp
public:
```

- 5. 通过添加一个在被调用时输出 **string** 的方法，开始公有成员列表。

```cpp
void bark() { cout << "WOOF!" << endl; }
```

- 6. 添加 **公有 setter 方法**，为每个 **private** 变量分配各自的值。

```cpp
void setAge(int yrs) { age = yrs; }
void setWeight(int lbs) { weight = lbs; }
void setColor(string hue) { color = hue; }
```

- 7. 添加 **公有 getter 方法**，从每个 **private** 变量中检索各自的值。

```cpp
int getAge() { return age; }
int getWeight() { return weight; }
string getColor() { return color; }
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_117_1.png)

在访问说明符之前声明的成员默认是 **private**，并且请记住在每个类声明后添加最后的分号。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_117_2.png)

在类声明中，请注意所有方法都声明为 **public**，所有变量都声明为 **private**。这种“公有接口、私有数据”的概念是创建类时的关键概念。

