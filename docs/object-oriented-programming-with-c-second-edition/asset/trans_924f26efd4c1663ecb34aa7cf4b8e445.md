

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
