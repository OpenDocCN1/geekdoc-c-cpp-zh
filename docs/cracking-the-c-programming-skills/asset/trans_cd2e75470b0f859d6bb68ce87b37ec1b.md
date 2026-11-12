
- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (b) 尽管它没有访问该值，但它有一个访问该值的代码块。因此同样会抛出相同的错误。

## 132. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    int fun()
    { cout<<f; }
};S;
class blo
{ public:
    void fun(int a)
    { if(a%2 == 0)
        ((stud *)this)->fun();
      else
        cout<<((stud *)this)->fun(); }
};D;
int main()
{ D.fun(7); }
```

- (a) 1 个垃圾值
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (d) 它给出‘0 garbage value’。与‘C’中相同，这里当‘int’函数没有显式返回值时，编译器在成功时自动返回 0。

## 133. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    blo *s;
};D;
class blo
{ public:
    int b;
    void fun(int a)
    { cout<<((stud *)this)->s->b; }
};S;
int main()
{ S.b = 2;
  S.fun(); }
```

- (a) 2
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (b) ‘blo’仅在‘stud’之后定义。因此编译器不知道‘blo’。

## 134. 代码将抛出什么错误？(L5)

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    blo *s;
};D;
class blo
{ public:
    int b;
    void fun(int a)
    { cout<<((stud *)this)->s->b; }
};S;
int main()
{ S.b = 2;
  S.fun(); }
```

- (a) 未知类型‘blo’
- (b) ‘blo’未命名类型
- (c) 无效的指针类型‘blo’
- (d) 以上都不是

**答案：** (b) 声明只期望一个类型。

```cpp
int b;
void fun(int a)
{ cout<<((stud *)this)->s->b; }
}S;
class stud
{ public:
    blo *s;
}D;
int main()
{ S.b = 2;
  S.fun(); }
```

- (a) 无效使用不完整类型‘class stud’
- (b) ‘class stud’的前向声明
- (c) ‘a’和‘b’都是
- (d) 以上都不是

**答案：** (c) 实际上，前向声明本身没有错误；但由于错误出在所声明类的不完整定义中，编译器会连同前向声明一起抛出错误。

## 139. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class blo;
class stud
{ public:
    blo *s;
};
class blo
{ public:
    int b;
    void fun(int a)
    { cout<<((stud *)this)->s->b; }
}S;
int main()
{ S.b = 2;
  S.fun(); }
```

- (a) 2
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (d) 发生段错误。这是因为指向对象‘blo *s’的指针未初始化为任何对象。因此尝试访问未初始化的地址会导致核心转储。

## 140. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class blo;
class stud
{ public:
    blo *s;
}D;
class blo
{ public:
    int b;
    void fun(int a)
    { cout<<((stud *)this)->s->b; }
}S;
int main()
{ D.s = &S;
  S.b = 2;
  S.fun(); }
```

- (a) 2
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (d) 即使现在也会发生段错误。初始化‘D.s = &S’仅针对对象‘D’。因此一般调用时该指针仍未初始化。如果指针‘stud *s’是‘static’，并在外部用‘&S’赋值，那么这将正常工作。初始化语句将是在 main 外部的“blo* stud::s = &S”。

## 4. 代码将抛出什么错误？(L2)

```cpp
#include<iostream>
using namespace std;
class cons
{ protected:
 cons()
 { m=9; }
 public:
 cons()
 { m=9; }
 int m;
}S;
int main()
{ cout<< "S.m";}
```

- (a) ‘cons::cons()’是受保护的
- (b) ‘cons::cons()’不能被重载
- (c) ‘a’和‘b’都是
- (d) 以上都不是

**答案：** (c) 重载将在后续章节中详细讨论。

## 5. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
 int m;
 void cons()
 { m=9; }
}S;
int main()
{ cout<< "S.m";}
```

- (a) 9
- (b) 0
- (c) 不可预测
- (d) 错误

**答案：** (d) 这里函数‘cons()’被视为普通成员函数，因为该函数有返回类型。编译器发现这是一个带返回类型的构造函数，并抛出“构造函数‘void cons’的返回类型说明”。

## 6. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
 int m;
 cons()
 { m=9; }
 cons()
 { m=11; }
}S;
int main()
{ cout<< "S.m";}
```

- (a) 9
- (b) 11
- (c) 不可预测
- (d) 错误

**答案：** (d) “cons::cons()”不能被重载。

## 7. 代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
 int m;
 cons();
}S;
cons::cons()
{ m=11; }
int main()
{ cout<< "S.m";}
```

- (a) 0
- (b) 11
- (c) 不可预测
- (d) 错误

**答案：** (b) 这种构造函数定义是允许的。

## 8. 代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
 int m;
};

cons::cons()
{
    m=11;
}

int main()
{
    cout<< "S.m";
}
```

- (a) 0
- (b) 11
- (c) 不可预测
- (d) 错误

**答案：** (d) 在上一题中，构造函数有声明。它只是向编译器表明该构造函数将在稍后或外部定义。因此外部的定义会正确地映射到它。这里声明被移除了。因此外部对构造函数的定义与预定义构造函数冲突。

## 9. 代码将抛出什么错误？(L5)

```cpp
#include<iostream>
using namespace std;
class cons
{
  public:
    int m;
};

cons::cons()
{
    m=11;
}

int main()
{
    cout<< "S.m";
}
```

- (a) `cons::cons()`不能被重载
- (b) 遇到隐式函数`cons`的定义
- (c) 隐式声明的`cons::cons()`的定义
- (d) 以上都不是

**答案：** (c) 这意味着编译器将`cons()`视为隐式函数，但它的定义却在外部指定。

## 10. 代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{
  public:
    int m;
    void cons()
int m;
cons()
{
    cout<< "constructor";
}

int main()
{
    cons S;
    S.cons();
}
```

- (a) constructor
- (b) constructor constructor
- (c) 不可预测
- (d) 错误

**答案：** (d) 构造函数不能由对象显式调用。

## 11. 代码将抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{
  public:
    int m;
    cons()
    {
        cout<< "constructor";
    }
};

int main()
{
    cons S;
    S.cons();
}
```

- (a) 无效使用构造函数
- (b) 无效使用`cons::cons()`
- (c) 类`cons`没有名为`cons()`的成员
- (d) 以上都不是

**答案：** (b) 通过任何对象访问构造函数都会产生此错误。

## 12. 代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{
  public:
    int m;
    void cons()
{ cout<<"constructor"; }
};
int main()
{ cons S;
  S.cons(); }
```

- (a) constructor
- (b) constructor constructor
- (c) 不可预测
- (d) 错误

**答案：** (d) 构造函数不能有返回类型。

## 13. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    void init()
    { m=80; }
    cons()
    { init(); }
};
int main()
{ cons S;
    cout<<S.m; }
```

- (a) 80
- (b) 0
- (c) 不可预测
- (d) 错误

**答案：** (a) 构造函数可以调用类的其他成员函数。

## 14. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons()
    { init(); }
};
void init()
{ cout<<"class initiated"; }
int main()
{ cons S; }
```

- (a) class initiated
- (b) 无输出
- (c) 不可预测
- (d) 错误

**答案：** (d) 构造函数不能调用非成员函数，这一点与其他类成员函数不同。

## 15. 代码将抛出什么错误？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons()
    { init(); }
};
void init()
{ cout<<"class initiated"; }
int main()
{ cons S; }
```

- (a) 类‘cons’没有名为‘init’的成员
- (b) ‘init’在此作用域中未声明
- (c) 缺少‘cons::init’的定义
- (d) 以上都不是

**答案：** (b) 构造函数在其可访问性范围方面存在限制。

## 16. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons()
    { void init()
        { cout<<"class initiated"; }
```
