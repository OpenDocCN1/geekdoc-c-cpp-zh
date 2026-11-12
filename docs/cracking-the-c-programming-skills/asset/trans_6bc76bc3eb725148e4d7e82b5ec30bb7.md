
- (a) 'f' 具有不完整类型
- (b) 没有匹配的函数可用于调用 'cons::cons()'
- (c) 'void' 的使用无效
- (d) 'a' 和 'b' 都正确
- (e) 以上全部正确

**答案：** (e) 'void' 被视为不完整变量，因此在特定构造函数定义中导致错误。

### 36. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons(int d)
    { cout<< d<< " "; }
    cons(void)
    { cout<< "basic constructor"; }
};
int main()
{ cons S(void); }
```

- (a) 基本构造函数
- (b) 不打印任何内容
- (c) 不可预测
- (d) 错误

**答案：** (a) 这里对象创建和构造函数都被视为基本定义，而 'void' 没有实际含义。因此它像任何普通构造函数一样起作用。

### 37. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons(int d)
    { cout<< d<< " ";
        cons(); }
    cons( )
    { cout<< "basic constructor"; }
};
int main()
{ cons S(8); }
```

- (a) 8 基本构造函数
- (b) 8
- (c) 不打印任何内容
- (d) 错误

**答案：** (a) 可以从重载构造函数中调用基本构造函数。

### 38. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons(int d)
    { cout<< d<< " ";
        cons(6); }
    cons( )
    { cout<< "basic constructor"; }
};
int main()
{ cons S(8); }
```

- (a) 打印“8 6”
- (b) 打印“8 6 6 6....（直到栈溢出）段错误”
- (c) 不打印任何内容，编译器陷入陷阱
- (d) 错误

**答案：** (b) 该调用是正确的，但无限递归导致了这种情况。

### 39. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons(int d)
```

```cpp
{ public:
   int m;
   cons(sup &d)
   { m=d.a;
       cout<< m; }
   cons( )
   { m=9; }
};
int main()
{ sup S;
   cons F(S); }
```

- (a) 9
- (b) 8
- (c) 不可预测
- (d) 错误

**答案：** (b) 这里对象是通过引用另一个类的对象来创建的。

### 47. 代码中使用了哪种重载形式的构造函数？(L4)

```cpp
#include<iostream>
using namespace std;
class sup
{ public:
    int a;
};
class cons
{ public:
    int m;
    cons(sup &d)
    { m=d.a;
        cout<< m; }
};
int main()
{ sup S;
    S.a=6;
    cons F(S); }
```

- (a) 拷贝构造函数
- (b) 带参数的构造函数
- (c) 用户定义数据类型构造函数

**答案：** (a) 构造函数只有三种类型。这里属于引用类型，因为一个对象作为引用传给另一个对象。如果对象不是作为引用传递，那么就会是 'b'。

### 48. 代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons(sup &d)
    { m=d.a;
        cout<< m; }
    cons( )
    { m=9; }
};
class sup
{ public:
    int a;
    sup()
    { a=8; }
};
int main()
{ sup S;
    cons F(S); }
```

- (a) 9
- (b) 0
- (c) 不可预测
- (d) 错误

**答案：** (d) 编译器在执行 main 之前会组织所有类。这里类 'sup' 在 'sup' 定义之前就被用于 'cons' 的构造函数中。因此编译器不知道它，并抛出错误。

### 49. 代码会抛出什么错误？(L5)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons(sup &d)
    { m=d.a;
        cout<< m; }
    { m=9; }
}
```

```cpp
{ cout<< "destructor"; }
};
int main( )
{ cons F; }
```

- (a) 析构函数 析构函数
- (b) 不打印任何内容
- (c) 析构函数
- (d) 错误

**答案：** (d) 析构函数只有一种类型。

### 57. 代码会抛出什么错误？(L5)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    ~cons( )
    { cout<< "destructor"; }
    ~cons(int d)
    { cout<< "destructor"; }
};
int main( )
{ cons F; }
```

- (a) 析构函数不能有参数
- (b) 'cons::~cons()' 不能被重载
- (c) 无效的析构函数 'cons::~cons(int)'
- (d) 'a' 和 'b' 都正确
- (e) 'a'、'b' 和 'c' 都正确

**答案：** (d) 析构函数重载是不可能的，一个程序中只能有一个析构函数。

### 58. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons( )
    { cout<< "constructor"; }
    ~cons( )
    { cout<< "destructor";
      cons(); }
};
int main( )
{ cons F; }
```

- (a) 构造函数 析构函数 析构函数
- (b) 构造函数 构造函数 析构函数 析构函数
- (c) 错误
- (d) 以上都不是

**答案：** (d) 它会无限打印“constructor destructor constructor destructor...”直到栈溢出。这是因为，每次调用构造函数时都会分配对象内存。因此，每个构造函数都必须执行析构函数来释放已分配的内存。于是，循环继续，并在栈溢出时停止。

### 59. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class cons
{ public:
    int m;
    cons( )
    { cout<< "constructor"; }
    ~cons( )
    { cout<< "destructor";
      S.~cons(); }
};
int main( )
{ cons F; }
```

- (a) 构造函数 析构函数 析构函数
- (b) 构造函数 构造函数 析构函数 析构函数
- (c) 错误
- (d) 以上都不是

**答案：** (c) 它会抛出“'S' 在此作用域中未声明”。实际上，类不知道 'S' 是什么，因为它只在类定义之后才定义。

### 60. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class sup
{ public:
    ~sup()
    { cout<< "sup destructor"; } }S;
class cons
{ public:
    ~cons( )
    { cout<< "destructor";
      S.~sup(); }};
int main()
{ cons F; }
```

- (a) sup 析构函数 析构函数
- (b) 析构函数 sup 析构函数
- (c) 错误
- (d) 以上都不是

**答案：** (b) 这里 'S' 是一个全局对象。因此它按预期正常工作。

## 4 存储类

变量的存储特性可以通过在声明时指定存储类来改变。本章深入探讨各种存储类的使用细节和属性。

### 1. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
void fun()
{ auto int m=9;
  cout<< m; }
int main()
{ fun();}
```

|  |  |
|---|---|
| (a) 9 | (b) 0 |
| (c) 不可预测 | (d) 错误 |

**答案：** (a) 'auto' 是一种存储类。它意味着变量在定义它的代码块完成后会被自动删除。所有变量默认都是 'auto'。因此没有必要显式指定它。

### 2. 代码会抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
void fun()
{ auto int m=9;
  cout<< m; }
int main()
{ fun();
  cout<<m; }
```

- (a) 未知变量 'm'
- (b) 'm' 在此作用域中未声明
- (c) 'm' 被声明为 auto，但在 main 中被访问
- (d) 以上都不是

**答案：** (b) 'main' 不知道 'm'。

### 3. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
  auto int m;
};
int main()
{ S.m=9;
  S.fun(); }
```

|  |  |
|---|---|
| (a) 9 | (b) 0 |
| (c) 不可预测 | (d) 错误 |

**答案：** (d) 类成员不能声明为 'auto'。

### 4. 代码会抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
  auto int m;
};
int main()
{ S.m=9;
  S.fun(); }
```

- (a) 类成员声明为 'auto'
- (b) 为 'm' 指定了存储类

