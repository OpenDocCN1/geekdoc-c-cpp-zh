
现在主函数开始。为 `ClassNewPtr01`（由于是指针，所以是四个字节）分配内存。目前，它是一个垃圾值。接下来是 `ClassNew` 的 `new` 运算符函数。创建两个指针：`temp`（用于保存 `head` 的当前值，以便 `head` 移动到下一个块）和 `p`（用于遍历池）。`temp` 指针初始化为 `head` 的当前值。现在评估 `head` 指针的值。在第一次调用 `new` 运算符期间，其值将为 NULL。很快就会发现，在某种特定情况下其值也将 NULL。`if` 结构中的测试表达式执行成功。因此，执行 `if` 块。通过调用 `new` 运算符分配了足够存放 `NO_OF_OBJECTS` 个对象的内存。随后，该池的地址（即该池中第一个对象的地址）被存储在 `temp` 指针中。此后，循环将新创建池中每个对象（最后一个对象除外）的 `next` 指针设置为下一个对象的地址。循环结束后，`if` 块的最后语句将最后一个对象的 `next` 指针置为 NULL。至此，`if` 块结束。函数的最后语句使 `head` 指针指向池中的第二个对象。`new` 运算符函数返回 `temp` 的值，即池第一个对象的地址。因此，`ClassNewPtr01` 现在指向池的第一个对象。`ClassNewPtr01` 现在通过调用该 `ClassNew` 的函数来操作池中的第一个对象。

现在让我们看列表 8.48 中主函数的第四条语句。`ClassNew` 类的 `new` 运算符函数将被再次调用。同样，`temp` 指针将初始化为 `head` 的当前值，该值不是 NULL（`head` 指向池中的第二个对象）。如果执行 `if` 块，则执行最后两条语句。`head` 指针增加以指向下一个对象（在本例中为第三个），以及当前正在运行的对象地址（在本例中为第二个对象）。

这一过程将一直持续直到第五次调用 `ClassNew` 的 `new` 函数（`ClassNew * ClassNewPtr05 = new ClassNew`）。尽管这是 `if` 块的测试表达式将执行，但 `head` 指针的值将为 NULL，同时返回池头和最后一个对象的地址。现在，当第六次调用 `new` 运算符时，`if` 块的测试表达式成功。分配一个新的池并重复该过程。

为了使 `new` 运算符函数成功，需要使用循环释放内存。这需要在池的每个对象中存在 `next` 指针。由于这个 `next` 指针导致的内存浪费（这会违背重载 `new` 运算符的初衷），可以通过使用联合体（union）来轻易防止。

现在让我们看看如何删除 `ClassNew` 类的 `delete` 运算符。`delete` 运算符将被重载，使其不再释放内存。相反，应用 `delete` 运算符所指向的块将被放回空列表。当下次调用 `new` 运算符时，将返回该块的地址。在查看实际代码之前，让我们先看看它的效果。

考虑仅调用一次 `new` 运算符的情况。该孤立调用之后是是对 `delete` 运算符的调用（列表 8.49）。

### 列表 8.49 调用重载的 delete 运算符

```cpp
/**ClassName NewDeleteForMemorySaveMain.cpp*/
#include<iostream>
#include"NewDeleteForMemorySave.h"
void main() {
    ClassNew* ClassNewPtr01 = new ClassNew;
    ClassNewPtr01->setx(10);
    cout<<ClassNewDeletePtr01->get()<<endl;
    delete ClassNewDeletePtr01;
}
```

```cpp
temp->v.next = head;
head = temp;
}
/*End of NewDeleteForMemorySave.cpp*/
/*Beginning of NewDeleteForMemorySave.cpp*/
#include<iostream>
#include"NewDeleteForMemorySave.h"
void main() {
    ClassNewDelete* ClassNewDeletePtr01 = new ClassNewDelete;
    ClassNewDeletePtr01->set(10);
    cout<<ClassNewDeletePtr01->get()<<endl;
    delete ClassNewDeletePtr01;
}
/*End of NewDeleteForMemorySaveMain.cpp*/
```

让我们带有谨慎的态度来讨论这个问题。`new` 运算符和运算符函数会被继承。这会导致 Bug 的产生。我们很快就会看到为什么了。然而，首先让我们证明这种继承并没有发生。请参见列表 8.51。

# 列表 8.51 new 运算符和 delete 函数被继承

```cpp
/*Beginning of A.h*/
#include<new.h>
class A {
    int x;
public:
    void setx(const int p = 0);
    int get() const;
    static void operator new(const size_t);
    static void operator delete(void * const, const size_t);
};
/*End of A.h*/
/*Beginning of A.cpp*/
#include"A.h"
#include<iostream>
void A::setx(const int p) {
    x=p;
}
int A::get() const {
    return x;
}
void * A::operator new(const size_t) {
    cout<<"operator new of class A called\n";
}
void A::operator delete(void * const p, const size_t) {
    cout<<"operator delete of class A called\n";
}
/*End of A.cpp*/
```

```cpp
/*Beginning of B.h*/
#include"A.h"
class B : public A {
    int y;
public:
    void sety(const int p = 0);
    int get() const;
};
/*End of B.h*/
```

```cpp
/*Beginning of B.cpp*/
#include"B.h"
void B::sety(const int q) {
    y=q;
}
int B::get() const {
    return y;
}
/*End of B.cpp*/
```

```cpp
/*Beginning of Main.cpp*/
#include<iostream>
#include"B.h"
void main() {
    B* Bptr01 = new B;
    delete Bptr01;
}
/*End of Main.cpp*/
```

# 输出

operator new of class A called

operator delete of class A called

当通过传递派生类类型作为参数来调用 new 和 delete 运算符时，可以看到的是基基的运算符函数被调用了。这为什么会是一个问题呢？

这种继承引起的问题在于，当调用 `new` 运算符时，头 指针指向了错误的地方。让我们假设在列表 8.5 中为类 A 重载了 `new` 运算符。在 `new` 运算符第一次执行完毕后，即使传递了派生类类型作为参数给 `new` 运算符，头指针指针也指向距离内存池第一个字节 4 个字节的地方。因此，当第二次调用 `new` 运算符时，返回的是第 5 个字节的地址，而不是第 9 个字节。我们需要第 9 个字节的地址，因为类 B 的对象将占用 8 个字节——4 字节用于 'x'，4 字节用于 'y'。从列表 8.5 可以清楚地理解产生的问题。

**列表 8.52 继承的 operator new 和 delete 函数产生的不良副作用**

```cpp
/*Beginning of Main.cpp*/
#include"B.h"
#include<iostream>
void main() {
    B* Bptr01 = new B;
    B* Bptr02 = new B;
    Bptr02->set(20);
    cout<<Bptr02->get()<<endl;
    Bptr01->set(10);
    cout<<Bptr02->get()<<endl;
}
/*End of Main.cpp*/
```

# 输出

2

10

在列表 8.5 的前两个语句之后，'Bptr01' 将指向内存池的第一个字节，而 'Bptr02' 将指向第五个字节。第三条语句将 20 写入从第 5 个字节到第 8 个字节的字节块。然而，第五条语句将 '10' 写入同一个内存块！

为了消除这种继承的影响，应该将目标分配释放内存块的大小与重载运算符的类的大小进行比较。如果两者不匹配，则应该调用全局 `new` 或全局 `delete` 运算符（参见列表 8.5）。

**列表 8.5 防止继承的 new 和 delete 运算符产生不良影响**

```cpp
void* A::operator new(const size_t size) {
    if(size != sizeof(class A)) // 如果传递的参数是派生类类型则为真
        return ::operator new(size);
    //其余代码
}

void A::operator delete(void* p, const size_t size) {
    if(size != sizeof(class A)) // 如果传递的参数是派生类类型则为真
        ::operator delete(p);
        return;
    //其余代码
}
```

## 8.2.8 重载下标运算符

重载下标运算符的语法如列表 8.4 所示。

**列表 8.4 重载下标运算符的语法**

```cpp
class <class_name> {
public:
    return_type operator[](param_list); // 声明
};
// 定义
return_type <class_name> :: operator[](param_list)
{
    // 语句
}
```

重载下标运算符的函数必须是类的静态成员。

让我们为 String 类重载下标运算符，使其返回存储在传递给它的位置上的字符。参见列表 8.5。

# 8.5 为 String 类重载下标运算符

```cpp
/*Beginning of String.h*/
class String
{
public:
    char& operator[](const int p);
    /*
    String类的其余部分
    */
};
/*End of String.h*/
/*Beginning of String.cpp*/
#include"String.h"
char& String::operator[](const int p)
{
    if(p<0 || p>len-1)
        throw "Invalid Subscript";
    return str[p];
}
/*
  String 类其他函数的定义
*/
/*End of String.cpp*/
/*Beginning of StringMain.cpp*/
#include"String.h"
#include<iostream>
void main() {
    String s("abcd");
    cout<<s.getString()]<<endl;
    s[0]='x';
    cout<<s.getString]<<endl;
}
/*End of StringMain.cpp*/
```

# 输出

abcd

abxd

```

# 使用 C++ 面对象编程

```cpp

throw "Invalid Subscript";

return cStr[p];

/*

String 类其余函数的定义

*/

/*String.cpp 结束*/

```

现在，有了单独的函数来对常量对象和非常量对象的下标运算符 `[]` 进行重载。然而，列表 8.56 中给出的函数仍然不完善。让我们考虑下面这段代码。

```cpp

const String s("abcd"); //不可接受，但编译器没有报错

s[1]='x'; // 报错！

```

代码中的第二条语句针对常量对象调用了常量函数。该函数通过引用返回所选元素，并将所选元素的值设置为 'x'。虽然编译器可以通过编译，但根据我们对“常量”的理解，第二条语句不应该是可以编译的。为了确保这一点，我们必须让常量 `String::operator[]` 函数返回常量引用而非非常量引用。参见列表 8.57。

列表 8.57 为常量对象返回常量值

```cpp

/*String.h 开始*/

class String {

public:

    char& operator[](const int); // 用于非常量对象

    const char& operator[](const int) const; // 用于常量对象

/*

String 类的其余部分

*/

};

/*String.h 结束*/

/*String.cpp 开始*/

#include"String.h"

char& operator[](const int p) // 用于非常量对象

{

    if(p<0 || p>=plen-1)

        throw "Invalid Subscript";

    return cStr[p];

}

const char& operator[](const int p) const // 用于常量对象

{

    if(p<0 || p>=plen-1)

        throw "Invalid Subscript";

    return cStr[p];

}

# 运算符重载、类型转换、新式强制转换和 RTTI 265

```cpp
/*String 类其余函数的定义
/*String.cpp 结束**/（注：原文此处存在格式错误）
```

如所愿，像这样的语句：

```cpp
s[1]='x';
```

如果调用对象 's' 是常量，则将不再通过编译。

我们包含这一关于重载下标运算符的章节是为了提供更多信息。重载下标运算符的函数形式参数可以是任何类型。在列表 8.57 的示例中，形式参数的类型是 `int`。然而，它可以是任何类型，例如 `char`、`float`、`double`。参见列表 8.58。

> **列表 8.58** 重载下标运算符的函数形式参数可以是任何类型

```cpp
/*String.h 开始*/
class String
{
public:
    int operator[](const char); // 用于非常量对象
    int operator[](const char) const; // 用于常量对象
/*String 类的其余部分*/
};/*String.h 结束*/
```

## 8.2.9 重载成员指针 (->) 运算符（智能指针）

重载成员指针 (->) 运算符稍微复杂。首先，让我们理解它是一个后缀运算符。如果它如下所示被重载：

```cpp
class A
{
public:
    B * operator->();
/*A 类的其余部分*/
};
```

那么随其后的第二条语句：

```cpp
A p;
p->abc();
```

将翻译为：

```cpp
(p.operator->())->abc();
```

显然，'abc' 必须是类 B 的成员。

成员指针 (->) 运算符可以被重载以创建智能指针。

智能指针与普通指针不同，它可以被设计为不可避免地指向有效对象。相比之下，普通指针必须由客户端显式初始化。因此，在每次使用之前必须对其有效性进行测试。智能指针是类对象。让我们创建一个行为类似于指向 String 类指针的类对象。参见列表 8.59。

# 列表 8.59 智能指针类

```cpp
/*StrPtr.h 开始*/
#include "String.h"
class StrPtr
{
    String * p;
public:
    StrPtr(String&); // 唯一的构造函数
};
/*StrPtr.h 结束*/
/*StrPtr.cpp 开始*/
#include "String.h"
StrPtr::StrPtr(String& ss)
{
    p=ss;
}
/*StrPtr.cpp 结束*/
```

我们必须注意列表 8.59 的类定义中特意省略了无参数构造函数。这迫使客户端在创建 `StrPtr` 类对象时，必须传递一个 `String` 类对象作为参数。因此，`StrPtr` 类的嵌入指针始终指向一个 `String` 类对象。客户端可以如下方式创建列表 8.59 中的类对象：

StrPtr si("abc");

StrPtr p(si);

```

为了完全模拟指针，`StrPtr` 类的对象应该能够如下使用：

```cpp

p->setString("def");

```

为了这一点，需要为 `StrPtr` 类重载成员指针运算符 (->)。这可以像列表 8.60 所示完成。

# 列表 8.60 为智能指针重载成员指针运算符

```cpp

/*StrPtr.h 开始*/

#include "String.h"

class StrPtr

{

    String * p;

public:
