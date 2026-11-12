
```cpp
class bro
{ public:
    int c; }D;
int* sto::c = &(D.c);
int main()
{ D.c = 'l';
    cout<<*(sto::c); }
```

|  |  |
|---|---|
| (a) 108 | (b) 0 |
| (c) 不输出任何内容 | (d) 错误 |

**答案：(a)** 按正确格式书写时，这会按预期工作。因此，静态指针也可以指向其他类的非静态成员。

### 41. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
    static void fun()
    { cout<<sto::c; }
};
int sto::c = 4;
int main()
{ sto::fun(); }
```

|  |  |
|---|---|
| (a) 4 | (b) 0 |
| (c) 不输出任何内容 | (d) 错误 |

**答案：(a)** `static` 是唯一适用于函数的存储类。静态函数不依赖于对象。它通过类名调用。

### 42. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
    static void fun()
    { cout<<sto::c; }
};
int main()
{ sto::fun(); }
```

|  |  |
|---|---|
| (a) 0 | (b) 不输出任何内容 |
| (c) 不可预测 | (d) 错误 |

**答案：(d)** 静态变量只有在初始化时才会分配内存，因为它不与对象关联。因此，当值未初始化时，会产生缺少变量的错误 `undefined reference to 'sto::c'`。

### 43. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
    int b;
    static void fun()
    { cout<<b; }
};
int main()
{ sto::fun(); }
```

|  |  |
|---|---|
| (a) 0 | (b) 不输出任何内容 |
| (c) 不可预测 | (d) 错误 |

**答案：(d)** 静态函数不能访问非静态变量。

### 44. 代码会抛出什么错误？(L5)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
    int b;
    static void fun()
    { cout<<b; }
};
int main()
{ sto::fun(); }
```

|  |  |
|---|---|
| (a) `sto::b` 在 `sto::fun` 中不是静态的 | (b) 在静态成员函数中无效使用成员 `sto::b` |
| (c) 在静态成员函数 'sto::fun' 中无效使用非静态成员 'sto::b' | (d) 以上都不是 |

**答案：(b)** 除静态成员外，不允许使用任何变量。

### 45. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
int b = 9;
class sto
{ public:
    static int c;
    static void fun()
    { cout<<b; }
}S;
int main()
{ sto::fun(); }
```

|  |  |
|---|---|
| (a) 9 | (b) 不输出任何内容 |
| (c) 不可预测 | (d) 错误 |

**答案：(a)** 静态函数可以访问其他全局变量而不会有任何问题。

### 46. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class sup
{ public:
    static int b;
};
int sup::b = 8;
class sto
{ public:
    static int c;
    static void fun()
    { cout<<sup::b; }
}S;
int main()
{ sto::fun(); }
```

|  |  |
|---|---|
| (a) 8 | (b) 不输出任何内容 |
| (c) 不可预测 | (d) 错误 |

**答案：(a)** 这也能正确工作。

### 47. 代码的输出是什么？(L5)

```cpp
#include<iostream>
using namespace std;
int b = 4;
class sto
{ public:
    static int c;
    int b;
    static void fun()
    { cout<<b; }
}S;
int main()
{ sto::fun(); }
```

|  |  |
|---|---|
| (a) 4 | (b) 不输出任何内容 |
| (c) 不可预测 | (d) 错误 |

**答案：(d)** 在类函数内部，类成员比全局成员具有更高优先级。

### 48. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
    int b;
    static void fun()
    { cout<< "hai"; }
}S;
int main()
{ sto::fun(); }
```

|  |  |
|---|---|
| (a) hai | (b) 不输出任何内容 |
| (c) 不可预测 | (d) 错误 |

**答案：(a)** 静态函数不一定需要使用静态成员变量。

### 49. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
```

**答案：(d)** 它会抛出“`'b' has both 'extern' and initializer`”。编译器不接受二者同时存在。

### 55. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
int b = 8;
void fun()
{ cout<<b; }
int main()
{ extern int b;
  b = 7;
  cout<<b<< " ";
  fun(); }
```

- (a) 7 7
- (b) 7 8
- (c) 不可预测
- (d) 错误

**答案：(a)** 更改 extern 变量的值也会更改原始变量。

### 56. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
int b = 8;
void fun()
{ cout<<b; }
int main()
{ b = 7;
  cout<<b<< " ";
  fun(); }
```

- (a) 7 7
- (b) 7 8
- (c) 不可预测
- (d) 错误

**答案：(a)** 即使省略 extern 存储类，也会得到相同输出。但这仅在同一个文件内有效。因此，当需要处理多个文件和变量时，'extern' 是唯一可行的方法！

### 57. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
int b = 6;
class sto
{ public:
    extern int b;
    void fun( )
    { cout<<b; }
}S;
int main( )
{ S.fun(); }
```

- (a) 6
- (b) 不输出任何内容
- (c) 不可预测
- (d) 错误

**答案：(d)** 类成员不能具有除 'static' 以外的存储类。

### 58. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
int b = 6;
class sto
{ public:
    void fun( )
    { extern int b;
      cout<<b; }
}S;
int main( )
{ S.fun( ); }
```

- (a) 6
- (b) 不输出任何内容
- (c) 不可预测
- (d) 错误

**答案：(a)** 这是可能的，因为该变量是局部变量，而不是类成员。

### 59. 代码会抛出什么错误？(L5)

```cpp
#include<iostream>
using namespace std;
int b = 6;
class sto
{ public:
    int b;
}S;
int main( )
{ S.b = extern int b;
  cout<<S.b; }
```

- (a) 在 `'extern'` 前应有 `';'`
- (b) 在 `'extern'` 前应有主表达式
- (c) 'a' 和 'b' 两者
- (d) 没有错误

**答案：(c)** `'extern int b;'` 是声明。应单独进行声明，然后初始化 `'s.b'`。

### 60. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
int main ()
{
    register int b = 9;
    cout<<b;
}
```

- (a) 9
- (b) 不输出任何内容
- (c) 不可预测
- (d) 错误

**答案：(a)** `register` 存储类表示请求将值存储在寄存器中而不是 RAM 中。它对变量的行为没有任何影响。

### 61. 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    auto int p;
    auto int q = 10;
    cout <<"default value " <<p <<"\n";
    cout <<"default value " <<q <<"\n";
    getchar ();
    return 0;
}
```

- (a) 取决于编译器
- (b) 垃圾值和 10
- (c) 1 和 10
- (d) 编译错误

**答案：(a)** 代码的行为会因编译器不同而不同。现代编译器会赋值为零，并且在大多数地方避免了垃圾值的概念。但是，传统编译器和 Dev C++ 之类的编译器会用垃圾值初始化 p，用 10 初始化 q。因此，答案取决于编译器。

### 62. 代码的输出是什么？

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int p;
    auto int q;
    cout <<"default value " <<p <<"\n";
    cout <<"default value " <<q <<"\n";
    getchar ();
    return 0;
}
```

- (a) 取决于编译器
- (b) 垃圾值和 0
- (c) 1 和 0
- (d) 编译错误

**答案：(a)** 代码的行为会因编译器不同而不同。现代编译器会赋值为零，并且排除了垃圾值的概念。但是，传统编译器和 Dev C++ 之类的编译器会用垃圾值初始化。因此，答案取决于编译器。

### 63. 以下代码片段的输出是什么？假设编译器为 Dev C++ 或传统编译器？(L3)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int p;
    auto int q;
    static int r;
    cout <<"default value "<<p<<"\n";
    cout <<"default value "<<q<<"\n";
    cout <<"default value "<<r<<"\n";
    getchar ();
    return 0;
}
```

- (a) 垃圾值，垃圾值，垃圾值
- (b) 0，垃圾值，垃圾值
- (c) 0，0，垃圾值
- (d) 以上都不是

**答案：(a)** 未初始化的整数（无论是否使用 auto）以及静态变量将具有垃圾值。在现代编译器中可能观察不到此行为。

### 64. 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int auto_verify ()
{
    int sum = 0;
    sum = sum + 1;
    cout <<"\n" << sum;
}
int main ()
{
    int i, ret;
    for (i=1;i<=5;i++)
    {
        ret = auto_verify();
    }
    getchar ();
    return 0;
}
```

- (a) 1,1,1,1,1
- (b) 0,0,0,0,0
- (c) 1,2,3,4,5
- (d) 以上都不是

**答案：(a)** 输出源于 auto 的行为。默认存储限定符是自动的，无需显式提及。

### 65. 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int auto_verify ()
{
    auto int sum = 0;
    sum = sum + 1;
    cout <<"\n" << sum;
}
int main ()
{
    int i, ret;
    for (i=1;i<=5;i++)
    {
        ret = auto_verify();
    }
    getchar ();
    return 0;
}
```

- (a) 1,1,1,1,1
- (b) 0,0,0,0,0
- (c) 1,2,3,4,5
- (d) 以上都不是

**答案：(a)** 输出源于 auto 的行为。

### 66. 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
static int variable;
int variable1;
int main ()
{
    cout <<"\n" << "static " << variable;
    cout <<"\n" << "global " << variable1;
}
```

