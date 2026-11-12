
```cpp
init(); }
};
int main()
{ cons S; }
```

- (a) 输出 `class initiated`
- (b) 无输出
- (c) 不可预测
- (d) 错误

**答案：(d)** 它在构造函数内部提示“a function-definition is not allowed here”。

### 17. 代码会抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons()
    {
        void init();
        init();
    }
};
void cons::init()
{
    cout << "class initiated";
}
int main()
{
    cons S;
}
```

- (a) 没有 `void cons::init()` 成员函数在类 cons 中声明
- (b) 无效的成员函数声明
- (c) 在错误作用域中的无效函数声明
- (d) 以上都不是

**答案：(a)** 成员函数不能在构造函数内部声明或定义。

### 18. 代码会抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    void init();
    cons()
    {
        void init();
        init();
    }
};
void cons::init()
{
    cout << "class initiated";
}
int main()
{
    cons S;
}
```

- (a) 没有 `void cons::init()` 成员函数在类 cons 中声明
- (b) 无效的成员函数声明
- (c) 在错误作用域中的无效函数声明
- (d) 以上都不是

**答案：(d)** 在函数 `cons::cons()` 中，对 `init()` 的未定义引用。

### 19. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    void init();
    cons()
    {
        init();
    }
};
void cons::init()
{
    cout << "class initiated";
}
int main()
{
    cons S;
}
```

- (a) 小写形式的类名
- (b) 无输出
- (c) 不可预测
- (d) 以上都不是

**答案：(a)** 构造函数可以轻松调用成员函数。

### 20. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    class sub
    {
        void init()
        {
            cout << "class initiated";
        }
    };
    int m;
    cons()
    {
        d.init();
    }
};
int main()
{
    cons S;
}
```

- (a) `class initiated`
- (b) 无输出
- (c) 不可预测
- (d) 错误

**答案：** (a) 构造函数也可以调用局部类的成员函数。

### 21. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons()
    {
        cout << "class initiated";
        cons();
    }
};
int main()
{
    cons S;
}
```

- (a) 连续打印 `class initiated` 直到栈溢出
- (b) 打印一次 `class initiated`
- (c) 不打印任何内容
- (d) 错误

**答案：** (a) 构造函数可以递归调用。

### 22. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons()
    {
        cout << "class initiated";
    }
    void init()
    {
        cons();
    }
};
int main()
{
    cons S;
    S.init();
}
```

- (a) 打印两次 `class initiated`
- (b) 打印一次 `class initiated`
- (c) 不打印任何内容
- (d) 错误

**答案：** (a) 构造函数可以从同一类的其他成员函数中调用。

### 23. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons()
    {
        cout << "class initiated";
        main();
    }
};
int main()
{
    cons S;
}
```

- (a) 重复打印 `class initiated` 直到栈溢出
- (b) 打印一次 `class initiated`
- (c) 不打印任何内容
- (d) 错误

**答案：** (d) 构造函数不能调用作用域之外的函数。因此它不能调用 `main`。会抛出“`main` was not declared in this scope”。

### 24. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons()
    {
        int d=8;
    }
};
int main()
{
    cons S;
    cout << S.d;
}
```

- (a) 8
- (b) 0
- (c) 不打印任何内容
- (d) 错误

**答案：** (d) `d` 的作用域是构造函数。构造函数执行后它就被删除。因此无法从对象访问它。

### 25. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons()
    { cout << "basic constructor"; }
    cons(int d)
    { cout << "constructor with parameters"; }
};
int main()
{
    cons S(3);
}
```

- (a) 带参数的构造函数
- (b) 基本构造函数
- (c) 不打印任何内容
- (d) 错误

**答案：** (a) 这是重载构造函数的一种形式。它接受带参数的对象。

### 26. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << "constructor with parameters"; }
};
int main()
{
    cons S(3);
}
```

- (a) 带参数的构造函数
- (b) 不打印任何内容
- (c) 不可预测
- (d) 错误

**答案：** (a) 由于该对象只需要一个带参数的构造函数，跳过基本构造函数没有影响。

### 27. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << "constructor with parameters"; }
};
int main()
{
    cons S;
}
```

- (a) 带参数的构造函数
- (b) 不打印任何内容
- (c) 不可预测
- (d) 错误

**答案：** (d) 这里对象是一个基本对象。它会寻找基本构造函数。由于存在重载构造函数，它不会映射到隐式定义的构造函数。因此，它会抛出关于缺少构造函数的错误。

### 28. 代码会抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << "constructor with parameters"; }
};
int main()
{
    cons S;
}
```

- (a) 没有匹配的函数调用 `cons::cons()`
- (b) 在函数 `cons::cons()` 中，候选函数期望 1 个参数，但提供了 0 个参数
- (c) 没有匹配的构造函数可调用 `cons::cons()`
- (d) 'a' 和 'b' 两者
- (e) 'b' 和 'c' 两者

**答案：** (a) 选项 'b' 是作为附加说明连同更多说明一起抛出的。

### 29. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << d << " "; }
    cons(float d)
    { cout << d << " "; }
};
int main()
{
    cons S(3.34);
    cons S(3);
}
```

- (a) 3.34
- (b) 3
- (c) 不可预测
- (d) 错误

### 30. 代码会抛出什么错误？(L5)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << d << " "; }
    cons(float d)
    { cout << d << " "; }
};
int main()
{
    cons S(3.34);
    cons S(3);
}
```

- (a) 没有匹配的函数调用 `cons::cons(double)`
- (b) 对重载的 `cons(double)` 的调用存在歧义
- (c) 'a' 和 'b' 两者
- (d) 以上都不是

**答案：** (b) 编译器尝试将函数调用与两个函数定义之一匹配。但在两者之间选择存在歧义。因此抛出错误。问题在于 `3.34` 的类型是 double 而不是 float。

### 31. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << d << " "; }
    cons(double d)
    { cout << d << " "; }
};
int main()
{
    cons S(3.34);
    cons S(3);
}
```

- (a) 3.34
- (b) 3
- (c) 不可预测
- (d) 错误

**答案：(a)** 现在这是正确的。参数与适当的定义匹配，并被适当地调用。

### 32. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << d << " "; }
};
int main()
{
    cons S(3.34);
    cons S(3);
}
```

- (a) 3.34
- (b) 3
- (c) 不可预测
- (d) 错误

**答案：(b)** 由于构造函数只有一个重载定义，各种数据类型会在内部映射，并进行类型转换。这里不存在歧义，因为只有一个定义可用。

### 33. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << d << " "; }
    cons(int f)
    { cout << f << " "; }
};
int main()
{
    cons S(3);
}
```

- (a) 3 3
- (b) 3
- (c) 不可预测
- (d) 错误

**答案：(d)** 更改参数的变量名并不会改变这两个定义。在内部，两个定义被视为相同，并产生错误“`cons::cons(int)` cannot be overloaded”。

### 34. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << d << " "; }
    cons(void f)
    { cout << "basic constructor"; }
};
int main()
{
    cons S;
}
```

- (a) 基本构造函数
- (b) 不打印任何内容
- (c) 不可预测
- (d) 错误

**答案：(d)** 变量不能具有 `void` 类型。因此会因此抛出一系列错误。

### 35. 代码会抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class cons
{
public:
    int m;
    cons(int d)
    { cout << d << " "; }
    cons(void f)
    { cout << "basic constructor"; }
};
int main()
{
    cons S;
}
```
