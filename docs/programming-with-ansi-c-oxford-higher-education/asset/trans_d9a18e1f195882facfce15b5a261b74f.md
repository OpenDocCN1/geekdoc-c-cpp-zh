

![](img/0da15892b2796544fb447dc5727e9ab4_395_0.png)

## 9.5 C++ 对象模型中的继承

实现第 9.4 节所述各点的办法可能有多种。C++ 对象模型选择了最简单的一种。编译器在派生时将基类完全嵌入到派生类中。相反，编译器本可以提供一个指向基类对象的指针。这种机制可以节省空间。

这里不提供指针有一个简单的理由。可能存在一条很长的继承链，其中 class1 派生 class2，而 class2 又派生 class3，等等。在这种情况下，当引用 classN 时，需要遍历 N 个指向基类的指针才能获得关于 classN 的完整信息。这在时间上效率不高。

访问基类元素与引用派生类元素在时间上的性能相似。这提供了对类的所有成员的统一访问，无论是同一类的成员、其基类的成员，还是该类的基类的成员，等等。

> 正如 C++ 对象模型的设计以效率为首要标准，它选择在派生发生时将基类复制到派生类对象中。

这种技术非常高效。然而，这种效率是有代价的。第一个问题是类大小的增加。派生类的大小等于基类的大小加上其自身元素总大小的和。这种技术的第二个问题是，有时会导致奇怪的后果。考虑一个从中派生出类并在若干应用中使用的库类的情形。如果原始基类发生变化，就需要重新编译所有使用该派生类的应用。这是因为尽管原始基类已发生变化，但在使用派生类时所做的复制

在编译时所使用的副本保持不变。如果它指向基类的指针，则无需重新编译应用程序，因为指针会自动指向新的基类。

程序 9.4 验证了 C++ 对象模型将基类嵌入到派生类中的事实。

### 程序 9.4 验证基类是否嵌入在派生类中

```
//ObjectModelImplementation.cpp
#include <iostream>
using namespace std;

class Base
{
    int i;
};

class Derived : public Base
{
    int j;
};

void main()
{
    Base BaseObject;
    Derived DerivedObject;

    cout << "Size of base object is" << sizeof(BaseObject) << "\n";
    cout << "Size of derived object is" << sizeof(DerivedObject) << "\n";
}
```

Output
Size of base object is 4
Size of derived object is 8

### 程序的工作原理

我们只讨论程序的架构以及它如何实现目的。基类没有任何公开的数据。私有整数变量未被继承；因此，派生对象的大小必须等于基类对象的大小（因为两者都有一个整数作为成员），但事实并非如此。基类对象被嵌入到派生类对象中，因此其大小等于其自身大小（int j 的大小）加上基类的大小（等于 int i 的大小）。该示例指出了将基类嵌入到派生类中的方案的第一个缺点，即可能的代码膨胀。

当使用虚基类时，C++ 对象模型表现出不同的行为。我们将在第 9.12 节学习虚基类。

考虑到对象模型的特殊性，数据成员的访问说明符有各种组合，并且可以有不同类型的派生。以下各节讨论不同访问说明符和不同派生的组合。

## 9.6 派生类的不同方式

从另一个类派生类有三种不同方式——公有、私有和保护继承。它们都会对成员产生不同类型的访问限制。我们将在以下小节中描述它们各自以及它们之间的差异。

### 9.6.1 公有派生

图 9.2 显示了使用公有访问说明符从基类派生类的第一种情况。基类的私有成员被复制到派生类但不可见。基类的公有成员被复制为派生类中的公有成员。

| Base | Derived |
|------|---------|
| Private → | Not directly accessible |
| int PrivateBaseInt; | int PrivateBaseInt; |
| Public → | Public |
| int PrivateBaseInt; | int PrivateBaseInt; |
| void SetPrivateBaseInt() | void SetPrivateBaseInt() |

基类子对象埋藏在派生类对象中。基类的私有部分虽被复制，但对派生类不可访问（尽管基类子对象成员函数如 void SetPrivateBaseInt() 可以访问它。）

![](img/0da15892b2796544fb447dc5727e9ab4_397_0.png)

### 9.6.2 私有派生

在这种情况下，基类的公有成员成为派生类的私有成员。同样，私有成员不被继承。尽管基类的私有成员被复制到派生类，但它们不可见。这在图 9.3 中显示。

| Base | Derived |
|------|---------|
| Private → | Not accessible |
| int PrivateBaseInt; | int PrivateBaseInt; |
| void SetPrivateBaseInt() | void SetPrivateBaseInt() |
| Private | Private |
| int PrivateDerivedInt; | int PrivateDerivedInt; |
| void SetPrivateDerivedInt() | void SetPrivateDerivedInt() |
| Public → | Public |
| int PublicDerivedInt; | int PublicDerivedInt; |
| void SetPublicPrivateDerivedInt() | void SetPublicPrivateDerivedInt() |

![](img/0da15892b2796544fb447dc5727e9ab4_397_1.png)

### 9.6.3 保护派生

在保护派生的情况下，基类的受保护成员以及公有成员成为派生类的受保护成员，如图 9.4 所示。

| Base | Derived |
|------|---------|
| Protected → ProtectedBaseInt; | Protected int ProtectedBaseInt; int PublicBaseInt; void SetProtectedBaseInt() |
| Protected | int ProtectedBaseInt; int ProtectedDerivedInt; int PublicDerivedInt; void SetProtectedBaseInt() void SetPublicProtectedInt() |
| Public | int PublicDerivedInt; void SetProtectedDerivedInt() void SetPublicProtectedInt() |

> 基类子对象埋藏在派生类对象中。基类的公有和受保护成员在这里已成为基类的成员。

# 图 9.4 受保护派生

如果一个类的受保护成员被继承为公有，它们仍保持受保护；而如果被继承为私有，则变为私有。其一个重要影响是对进一步继承的影响。如果派生为公有（或受保护），受保护成员将可用于进一步的公有（或受保护）派生继承（即，可以从该类的派生类再派生一个类）。假设我们有以下内容：

```
Class GrandpaBase
{
private:
int PrivateGB;
protected:
int ProtectedGB;
}
class Base1 : public GrandpaBase
{
private:
int PrivateB;
protected:
int ProtectedB;
}
class Base2 : private GrandpaBase
{
private:
int PrivateB;
protected:
int ProtectedB;
}
class Derived1 : public Base1
{ };
```

```
class Derived2 : public Base2
{
};
```

在这种情况下，ProtectedGB 将可供 Derived1 使用（作为受保护），但不可供 Derived2 使用；这是因为 Base2 是从 GrandpaBase 私有派生的。

## 9.7 访问控制

类的成员函数和派生类的成员函数、友元和对象可以访问类的不同部分。对公有、私有和受保护成员的访问对所有这些实体是不同的。访问控制描述了谁可以访问什么以及以何种形式。图 9.5 显示了访问控制。

![](img/0da15892b2796544fb447dc5727e9ab4_399_0.png)

可用的或可访问的实体可由访问控制确定。可供访问的三个实体如下：

- 1. Public
- 2. Private
- 3. Protected members

访问它们的三种实体类型如下：

- 1. 类的成员函数和类的友元
- 2. 派生类的成员函数
- 3. 类以及派生类的对象

## 9.8 访问声明

如前所述，如果一个类以私有方式派生，则无法使用派生类对象访问基类的数据成员。相反，如果类以公有方式派生，则所有成员都可以作为公有访问。如果某人想派生一个类并且只想让其中一些而不是所有公有成员可供派生类对象使用，则必须提供访问声明。使用访问声明，即使在私有派生之后，也可以为基类的某些成员提供公有访问。请考虑程序 9.5 以更好地理解该概念。

