

```cpp
{
cout<<"num1 = "<<num1<<endl;
cout<<"num2 = "<<num2<<endl;
}
void main()
{
int ABC::*varp1;
//Declaring a pointer to a data member
void (ABC::*funcp)();
//Declaring a pointer to a member function
ABC obj(20,40), *ptr;
ptr=&obj;
varp1=&ABC::num2;
//Assigning class member using pointer
funcp=&ABC::displayValue;
ptr->*varp1=75;
//Modifying data member using pointer
(*ptr->*funcp)();
//Calling member function using pointer
}
```

**输出：**

```text
num1 = 20
num2 = 75
```

在清单 31 中，创建了 ABC 类，该类有一个私有成员 num1，以及三个公有成员 num2、ABC() 和 displayValue()。ABC() 构造函数和 displayValue() 函数使用 :: 运算符在 ABC 类外部定义。在 main() 函数中，声明了指针 varp1 和 funcp，并分别将其赋值为 num2 变量和 ABC 类的 displayValue() 成员函数。此外，还创建了 ABC 类的两个对象 obj 和 ptr，其中 ptr 是一个指针对象，并用 obj 对象的引用进行初始化。然后，使用 ptr 指针对象配合 ->* 运算符以及 varp1 和 funcp 指针来访问 ABC 类的成员。

## 创建指针对象数组

可以创建指针对象数组，其中每个指针对象都指向一个单独的类对象。声明指针对象数组的语法为：

```cpp
<class_name> *pointer_name [array_size];
```

声明指针对象数组的示例如下：

```cpp
Employee *ptremp[10];
```

在前面的示例中，ptremp 表示 Employee 类的指针对象数组，数组大小为 10。

清单 32 展示了如何创建类的指针对象数组（可以在光盘的 Code\Chapter7 文件夹中找到 ArrayPointerObjects.cpp 文件）：

### 清单 32：创建类的指针对象数组

```cpp
#include<iostream.h>
class ABC
{
int num1;
//private data member
public:
int num2;
//public data member
void setValue(int);
void displayValue();
};
void ABC::setValue(int p)
{
num1=p;
}
void ABC::displayValue()
{
cout<<"num1 = "<<num1<<endl;
cout<<"num2 = "<<num2<<endl;
}
void main()
{
ABC obj[4];
//Declaring an array of objects
for(int i=0;i<4;i++)
{
obj[i].setValue(i+1);
obj[i].num2=(i+1)*5;
}
ABC *ptr[4];
for(int k=0;k<4;k++)
ptr[k]=&obj[k];
for(int j=0;j<4;j++)
{
cout<<"Object no. "<<j+1<<endl;
ptr[j]->displayValue();
cout<<endl;
}
}
```

**输出：**

```text
Object no.1
num1 = 1
num2 = 5

Object no.2
num1 = 2
num2 = 10

Object no.3
num1 = 3
num2 = 15

Object no.4
num1 = 4
num2 = 20
```

在清单 32 中，创建了 ABC 类，该类有一个私有成员 num1 和三个公有成员 num2、setValue() 和 displayValue()。setValue() 和 displayValue() 函数使用 :: 运算符在 ABC 类外部定义。在 main() 函数中，obj 是对象数组，而 ptr 是 ABC 类的指针对象数组。在 for 循环中，将 obj 对象数组的引用分别赋给 ptr 对象数组的每个元素。使用 -> 运算符访问 ABC 类的 displayValue() 函数。

## 创建基类和派生类的指针对象

在 C++ 中，指向基类的指针可以指向任意派生类的对象。以下代码片段展示了基类如何指向派生类对象：

```cpp
A *PtrObj;
PtrObj = & B;
PtrObj = & C;
```

在前面的代码片段中，A 表示基类，而 B 和 C 派生自该基类。PtrObj 是类 A 的指针对象，并用 B 类和 C 类的引用进行初始化。

清单 33 展示了如何创建和使用基类和派生类的指针对象（可以在光盘的 Code\Chapter7 文件夹中找到 PointerDerivedObjects.cpp 文件）：

### 清单 33：创建和使用基类和派生类的指针对象

```cpp
#include<iostream.h>
class ABC
{
int num1;
//private data member
public:
int num2;
//public data member
void setValue(int);

o4->displayValue();
}
```

**输出：**

```text
Base class members
num1 = 1
num2 = 10
Base class members using derived object
num1 = 3
num2 = 30
Derived class members
num1 = 3
num2 = 30
num3 = 4
num4 = 40
```

在清单 33 中，ABC 和 XYZ 是两个类，其中 ABC 是基类，XYZ 是它的派生类。ABC 类有一个私有成员 num1 和三个公有成员 num2、setValue() 和 displayValue()。类似地，XYZ 类有一个私有成员 num3 和三个公有成员 num4、setValue() 和 displayValue()。这两个类的 setValue() 和 displayValue() 函数都使用 :: 运算符在类外部定义。

在 main() 函数中，o1 是 ABC 类的指针对象，o2 是 ABC 类的普通对象。将 o2 对象的引用赋给 o1 对象，并借助 -> 运算符通过 o1 指针对象访问 ABC 类的类成员。接下来，声明 XYZ 类的对象 o3。现在，将 o3 对象的引用赋给 o1 指针对象。借助 -> 运算符通过 o1 指针对象访问 ABC 类的类成员。最后，创建 XYZ 类的指针对象 o4，并用 o3 对象的引用对其进行初始化。不过，这一次是借助 -> 运算符通过 o4 指针对象访问 XYZ 类的类成员。

在创建和使用指针对象之后，让我们学习静态绑定和动态绑定及其在 C++ 中的实现。

## 7.11 实现静态绑定和动态绑定

在 C++ 中，可以通过函数重载、运算符重载以及使用虚函数实现动态绑定来实现多态。动态绑定是动态多态概念的实际实现。在解释动态绑定之前，我们先解释多态和动态多态。某种事物以不止一种形式出现的现象称为多态。多态可以细分为两种形式：静态多态和动态多态。本节重点介绍动态多态，它在 C++ 中用于派生类重写基类中声明的函数时。

动态多态是指实体根据其将要扮演的角色或所处的上下文改变其形式。这个概念可以类比为变色龙在不同环境下改变颜色。当一个函数以不止一种形式存在时，就说该函数表现出动态多态。C++ 编译器在运行时将函数调用与正确的函数定义相匹配，这称为 `dynamic binding`。不过，要实现动态绑定，虚函数的概念很重要。

让我们在静态绑定和动态绑定的背景下学习以下主题：

- 静态绑定或早期绑定
- 动态绑定或后期绑定与虚函数
- 静态绑定与动态绑定的区别
- 纯虚函数
- 抽象类
- 虚析构函数

### 实现静态绑定或早期绑定

绑定是指将对象或类与其成员关联起来的行为。清单 34 展示了一个绑定示例（可以在光盘的 Code\Chapter7 文件夹中找到 Binding.cpp 文件）：

### 清单 34：实现绑定

```cpp
#include <iostream.h>

class A
{
public:
    void display()
    {
        cout << "Class A" << endl;
    }
};
class B: public A
{
public:
    void display()
    {
        cout << "Class B" << endl;
    }
};
class C: public A
{
public:
    void display()
    {
        cout << "Class C" << endl;
    }
};
int main()
{
    A obj;
    obj.display();
    return 0;
}
```

**输出：**

```text
Class A
```

在清单 34 中，创建了类 A 的 obj 对象，并调用了 display() 成员函数，如下面的代码片段所示：

```cpp
A obj;
obj.display();
```

在前面的代码片段中，对 C++ 编译器来说不存在歧义，因为它知道 display() 函数的引用属于 A 类。

如果类的对象是指针类型，那么编译器调用该类的成员函数同样没有问题，如下面的代码片段所示：

```cpp
A *PtrObj;
PtrObj = new A;
PtrObj->display();
```

在前面的代码片段中，编译器需要将 display() 函数关联到某个特定的类。这里同样不存在歧义。编译器根据 PtrObj 指针对象的类型，将该函数关联到类 A。

默认情况下，C++ 在编译时将函数调用与正确的函数定义相匹配，这称为静态绑定或早期绑定。清单 35 展示了一个静态绑定或早期绑定的示例（可以在光盘的 Code\Chapter7 文件夹中找到 StaticBinding.cpp 文件）：

### 清单 35：实现静态绑定或早期绑定

```cpp
#include <iostream.h>
class X
{
public:
  void display()
  {
    cout << "Class X" << endl;
  }
```

