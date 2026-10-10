
输出
257 2.2

然而，应用程序程序员这种显式地址操作是无法防止的。这留给读者作为一个练习，以解释上述段落（列表 2.12）的输出。

## 2.1.9 箭头运算符

可以通过指向对象的指针调用对象的成员函数。箭头运算符（`->`）实现了这一点。列表 2.13 展示了一个说明性示例。

### 列表 2.13 通过指针访问成员

```cpp
/*Beginning of PointerMember.cpp*/

#include<iostream.h>

#include"Distance.h"

void main() {
    Distance d1;           //对象
    Distance * dPtr;      //指针
    dPtr=&d1;               //指针初始化
    /*相当于 d1.setFeet(1.1) 和 d1.getInches(1.1)*/
    dPtr->setFeet(1);      //调用成员函数
    dPtr->setFeet(1.1);    //通过指针
    /*相当于 d1.getInches() << d1.getInches()*/
    cout<<dPtr->getInches<<" "<<dPtr->getInches()endl;
}

/*End of PointerToMember.cpp*/
```

# 输出
11.1

有趣的是，点（`.`）运算符和箭头（`->`）运算符的定义在 C++ 中得到了扩展。它在 C++ 中不仅接收右侧的数据成员，还将成员函数作为其右侧的操作数。如果右侧的操作数是数据成员，则箭头的行为与 C 语言中相同。然而，如果它是一个类的成员函数，且其左侧的操作数是相同类型，那么编译器简单地将指针的值作为隐式的起始参数传递给函数调用。因此，语句

```
dPtr->setFeet(1);
```

在转换后变为

```cpp
setFeet(dPtr,1);
```

现在，`dPtr` 的值被拷贝到该指针。因此，该指针也指向 `dPtr` 所指向的同一个对象。

## 2.1.10 从另一个函数调用成员函数

可以从另一个函数调用成员函数。列表 2.14 展示了一个说明性示例。

| 列表 2.14 | 从另一个函数调用成员函数 |
| :--- | :--- |

```cpp
/*Beginning of NestedCall.cpp*/

class A
{
    int x;
public:
    void setindirect(int q);
    void setx(int p);
};

void A::setindirect(int q)
{
    x=q;
}

void A::setx(int p)
{
    setindirect(p);
}

void main()
{
    A A1;
    A1.setindirect(1);
    A1.setx(2);
}

/*end of NestedCall.cpp*/
```

## 2.2.2 成员函数形式参数的默认值

我们已经知道可以为非成员函数的参数分配默认值。也可以为成员函数的形式参数指定默认值。列表 2.17 给出了一个说明性示例。

**Listing 2.17** 给成员函数的参数赋予默认值

```cpp
/*Beginning of memFuncDefault.cpp*/

#include<iostream.h>

class A {
public:
    void show(int p=1);
};

void A::show(int p) {
    for(int i=0;i<p;i++)
        cout<<"Hello\n";
}

void main() {
    A A1;
    A1.show();                   //使用了默认值
    A1.show(3);                  //默认值被覆盖
}

/*End of memFuncDefault.cpp*/
```

输出

Hello
Hello
Hello
Hello

再次，必须记住，如果为成员函数的某些或全部形式参数指定了默认值，那么在重载成员函数时要小心。例如，当编译器在列表 2.18 中找到类 `A` 的 `show()` 函数的第二个原型时，它会报告*歧义错误*。

**Listing 2.18** 给重载成员函数的参数赋予默认值会导致歧义错误

```cpp
class A {
public:
    void show();
    void show(int p=0);             //歧义错误
};
```

此类歧义错误的原因已经在第 1 章的重载节中解释过。与非成员函数的情况一样，如果为多个形式参数指定了默认值，则必须从右向左指定。同样，默认值必须在函数原型中指定，而不是在函数定义中指定。此外，可以为任何类型的形式参数指定默认值。

## 2.2.3 内联成员函数

通过以下两种方法之一可以将成员函数变为内联函数：

- 在类内部定义函数（如列表 2.5 所示）
- 仅在类内声明函数原型而不定义函数。该函数使用作用域解析运算符在类外定义。该定义以 `inline` 关键字为前缀。对于非成员函数，内联函数的定义必须在调用它之前出现。因此，函数应该定义在与其类相同的同一个头文件中。列表 2.19 阐述了。

### Listing 2.19 内联成员函数

```cpp
/*Beginning of memInline.cpp*/

class A {
  public:
    void show();
}

inline void A::show() //在头文件中定义
{ // //A::show()函数的定义
}

/*End of memInline.cpp*/
```

## 2.2.4 常量成员函数

让我们考虑这种情况：库程序员希望其类的一个成员函数不能改变成员数据的值。该函数应该能够读取数据成员中包含的值，但不能修改它们。然而，他担心在定义函数时可能会意外编写执行此类操作的代码。为了防止这一点，他寻求编译器的帮助。如果他将函数声明为常量，从而防止通过函数更改数据成员的值，编译器将抛错误。

让我们考虑 `Distance` 类。`Distance::get()`、`Distance::inches()` 和 `Distance::add()` 函数显然应该是常量函数。它们不应意外改变调用对象成员的值。

通过在原型和函数定义头后面加上 `const` 关键字，可以将成员函数指定为常量。列表 2.20 展示了 `Distance` 类成员函数修改后的原型和定义。

### Listing 2.20 常量成员函数

```cpp
/*Beginning of Distance.h*/
/*包含 Distance 类定义的头文件*/

class Distance
{
    int iFeet;
    float fInches;
public:
    void setFeet(int);
    int getFeet() const;
    void setInches(float) const;
    float getInches() const;
    Distance add(Distance) const;
};

//End of Distlib.h*/

/*Beginning of Distlib.cpp*/
/*Distance 类的实现文件*/

#include"Distance.h"

void Distance::setFeet(int x)
{
    iFeet=x;
}

int Distance::getFeet() const
{
    iFeet++;
    //错误!!
    return iFeet;
}

void Distance::setInches(float y)
{
    fInches=y;
}

float Distance::getInches() const
{
    fInches=0.0;
    //错误!!
    return fInches;
}

Distance Distance::add(Distance dd) const
{
    Distance temp;
    temp.iFeet=iFeet+dd.iFeet;
    temp.setInches(fInches+dd.fInches);
    iFeet++;
    //错误!!
    return temp;
}/*End of Distlib.cpp*/
```

对于常量成员函数，调用对象占用的内存是只读内存。编译器如何管理此点？此指针变成了“指向常量的常量指针”，而不是“常量指针”。例如，此指针对于 `Distance::get()`、`Distance::inches()` 和 `Distance::add(Distance)` 的类型为 `Distance* const`。显然，常量成员函数不能相对于对象调用。

## 2.2.5 可变成员 (Mutable Members)

`mutable` 成员甚至可以在常量函数内部被修改。这是因为数据成员是用 `mutable` 关键字声明的。列表 2.21 说明了这一点。

### Listing 2.21 可变成员

```cpp
/*Beginning of mutable.h*/

class A
{
    int x;
    mutable int y;
public:
    void abc() const
    {
        y++;
    }
    void def() const
    {
        y++;
    }
};

/*End of mutable.h*/
```

## 2.2.6 友元 (Friends)

类可以将非成员函数和其他类的成员函数作为其友元。这些函数可以访问私有成员。

### 非成员函数

友元函数是具有访问私有成员特殊权的非成员函数。在本节中，我们将只研究不是成员函数的函数。友元函数在其旨在成为友元的类定义内部原型。原型以 `friend` 关键字为前缀。列表 2.22 给了一个示例。

### Listing 2.22 友元函数

```cpp
/*Beginning of friend.cpp*/

class A
{
    int x;
public:
    friend void abc(A); //友元函数的原型
};

void abc(A& Aobj) //友元函数的定义
{
    Aobj.x++; //访问对象的私有成员
}

void main()
{
    A A1;
    abc(A1);
}/*End of friend.cpp*/
```

关于友元函数，我们必须记住的几点是：

- `friend` 关键字应该出现在原型中，而不是定义中。
- 由于它是作为友元的类的非成员函数，因此可以在该类的私有部分或公共部分进行原型。
- 与执行相同任务的成员函数相比，友元函数多了一个参数。这是因为其不能相对于任何对象调用。相反，对象本身作为显式参数出现在友元调用中。
- 在定义友元函数时，不需要也不应该使用作用域解析运算符。

### 友类

类可以是另一个类的友元。友元类的成员函数可以访问该友类对象的私有数据成员。要把类 `B` 成为类 `A` 的友元，那么该语句应该写在类 `A` 的定义内部。

## 列表 2.23 声明友类

```cpp
class A
{
    friend class B;              //将 B 声明为 A 的友类
    /*
    类 A 的其余部分
*/
};
```

将类 `B` 声明为友类的语句出现在类 `A` 的私有部分还是公共部分都没有关系。现在，类 `B` 的成员函数可以访问类 `A` 对象的私有数据成员。列表 2.24 示例说明了这一点。

## 列表 2.24 声明友类的影响

```cpp
/*friendClass.cpp 的开始*/

class B; //前向声明...这是必要的因为
//类 B 的定义位于将类 B 声明为 A 的友类的
//语句之后。

class A
{
    int x;
public:
    void setx(const int x=0);
    int getx()const;
    friend class B;              //将 B 声明为 A 的友类
};

class B
{
    A * Aptr;
public:
    void Map(A * const);
    void test_friend(const int);
};

void B::Map(A * const p)
{
    Aptr = p;
}

void B::test_friend(const int i)
{
    Aptr->x=i;              //访问私有数据成员
}

/*friendClass.cpp 的结束*/
```

我们可以看到，尽管类 `B` 的成员函数不是类 `A` 的成员函数，但它们能够访问类 `A` 对象的私有数据成员。这是因为它们是类 `A` 的友类。友谊关系不是传递的。例如，考虑列表 2.25。

## 列表 2.25 友谊关系不是传递的

```cpp
class B;
class C;

/*friendTran.cpp 的开始*/

class A
{
    friend class B;
    int a;
};

class B
{
    friend class C;
};

class C
{
    void f(A * p)
    {
        p->a++; //错误：C 不是 A 的友类
                //尽管它是友类的友类
    }
};

/*friendTran.cpp 的结束*/
```

## 友元成员函数

我们如何让一个类的某些特定成员函数成为另一个类的友元？为了仅让 `B::test_friend()` 函数成为类 `A` 的友元，将类 `A` 声明中的行
`friend class B;`
替换为行
`friend void B::test_friend();`

修改后的类 `A` 定义为：
```cpp
class A
{
    /*
    类 A 的其余部分
    */
    friend void B::test_friend();
}
```

为了成功编译此代码，编译器应该先看到类 `B` 的定义。否则，它不知道 `test_friend()` 是类 `B` 的成员函数。这意味着我们应该将类 `B` 的定义放在类 `A` 的定义之前。

类型为 `A *` 的指针是类 `B` 的一个私有数据成员。因此，编译器在编译类 `B` 的定义之前也应该知道存在一个类 `A`。这种循环依赖问题通过前向声明来解决。这是通过在类 `B` 的定义之前插入行
`class A;`
// 仅声明！不是定义！！
现在，两个类的声明和定义如列表 2.26 所示。

## 列表 2.26 对需要友类的类进行前向声明

```cpp
/*friendFunc.h 的开始*/

class A;

class B
{
    A * Aptr;
    public:
    void Map(A * const);
    void test_friend(const int);
};

class A
{
    int x;
    public:
    friend void B::test_friend(const int);
};

/*friendFunc.h 的结束*/
```

如果我们尝试将 `B::test_friend()` 作为内联函数定义在类内部，就会出现另一个问题。见列表 27。

## 27. 在类内部定义友元函数的问题

```cpp
class B
{
    /*
    类 B 的其余部分
    */
    friend void test_friend(const int)
    {
        // 错误
    }
};
```

## 28. 声明为内联友元函数

```cpp
/*friendFunc.cpp 的开始*/

class A;

class B
{
    A * Aptr;
    public:
    void Map(A * const);
    void test_friend(const int);
    void test_friend(const int i)
    {
        Aptr->x=i;
    }
};

class A
{
    int x;
    public:
    friend void B::test_friend(const int);
};

/*friendFunc.cpp 的结束*/
```

## 29. 友类作为桥梁

```cpp
/*friendClass.cpp 的开始*/

class B; //前向声明

class A
{
    /*
    类 A 的其余部分
*/
    friend class B;
};

class B
{
    /*
    类 B 的其余部分
*/
    friend void func(const int);
};

/*friendClass.cpp 的结束*/
