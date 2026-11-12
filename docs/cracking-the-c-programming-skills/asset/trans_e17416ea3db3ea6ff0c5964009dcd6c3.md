
- (a) 9
- (b) 0
- (c) 错误
- (d) 以上都不是

答案：(c) 这不是在类外定义函数的合法方式。

### 79. 代码将抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    void fun(); };
student::void fun()
{ cout<<m;}
int main()
{ S.m=9;
    S.fun();}
```

- (a) 在 'void' 之前需要函数名
- (b) 'function' 的限定标识符 'void'
- (c) 在 'void' 之前需要非限定标识符
- (d) 以上都不是

答案：(c) 'void' 被视为函数名。

### 80. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
void student::fun()
{ cout<<m;}
class student
{ public:
    int m;
    void fun(); };
int main()
{ S.m=9;
    S.fun();}
```

- (a) 9
- (b) 0
- (c) 错误
- (d) 以上都不是

答案：(c) 由于 student 在函数定义之前未定义，因此会产生错误。

### 81. 代码将抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
void student::fun()
{ cout<<m;}
class student
{ public:
    int m;
    void fun(); };
int main()
{ S.m=9;
    S.fun();}
```

- (a) 'student' 尚未声明
- (b) 未知类型 'student'
- (c) 'm' 未在此作用域中声明
- (d) 'a' 和 'c' 都正确
- (e) 'b' 和 'c' 都正确

答案：(d) 在定义 'student' 之前不能访问它。

### 82. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
void fun()
{ cout<<m;}
class student
{ public:
    int m;
    void fun(); };
int main()
{ S.m=9;
    S.fun();}
```

- (a) 9
- (b) 0
- (c) 错误
- (d) 以上都不是

答案：(e) 同名全局函数和成员函数不会映射到一起。类成员 'fun' 不会映射到全局 'fun' 的定义。

### 83. 代码将抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
void fun()
{ cout<<m;}
class student
{ public:
    int m;
    void fun(); };S;
int main()
{ S.m=9;
    S.fun();}
```

- (a) 'student::fun' 的无效重写
- (b) 对 'student::fun()' 的未定义引用
- (c) 'student::fun' 的无效重写
- (d) 以上都不是

**答案：(b)** 成员函数 'fun' 未定义。

### 84. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    void fun()
    { cout<< "hai";}
};S;
void student::fun()
{ cout<<m;}
int main()
{ S.m=9;
    S.fun();}
```

- (a) 9
- (b) hai
- (c) hai9
- (d) 错误

**答案：(d)** 一个成员只能定义一次。

### 85. 代码将抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    void fun()
    { cout<< "hai";}
};S;
void student::fun()
{ cout<<m;}
int main()
{ S.m=9;
    S.fun();}
```

- (a) 'fun' 被重定义
- (b) 'void fun' 的重定义
- (c) 'void student::fun()' 的重定义
- (d) 以上都不是

**答案：(c)** 成员只能通过类名来标识。

### 86. 代码将抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    void fun()
    { cout<< "hai";}
};S;
void student::fun();
int main()
{ S.m=9;
    S.fun();}
```

- (a) 'void student::fun()' 的重新声明
- (b) 类成员 'void fun' 的重新声明
- (c) 在类外声明 `void student::fun()` 不是定义
- (d) 没有错误

答案：(c) 成员函数不能在类外声明。

### 87. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{
    public:
        int m; };
void student::fun()
{ cout<<m; }
int main()
{ S.m=9;
    S.fun(); }
```

- (a) 9
- (b) 0
- (c) 不可预测
- (d) 错误

答案：(d) 这不会使 'fun' 成为 'student' 的成员。

### 88. 代码将抛出什么错误？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m; };
void student::fun()
{ cout<<m; }
int main()
{ S.m=9;
    S.fun(); }
```

- (a) 类 'student' 中没有声明成员函数 'void student::fun()'
- (b) 'class student' 没有名为 'fun' 的成员
- (c) 'a' 和 'b' 都正确
- (d) 以上都不是

答案：(c) 定义有错误，函数调用给出第二个错误。

### 89. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m; };
void student::fun();
fun()
{ cout<<m; }
int main()
{ S.m=9;
    S.fun(); }
```

- (a) 9
- (b) 0
- (c) 不可预测
- (d) 错误

答案：(d) 即使这样也有同样的问题。

### 90. 代码抛出的错误中有一部分是什么？(L5)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m; };
void student::fun();
fun()
{ cout<<m; }
int main()
{ S.m=9;
    S.fun(); }
```

- (a) 'fun' 的无效声明
- (b) ISO C++ 禁止声明无类型的 'fun' [-fpermissive]
- (c) 声明无类型的 '::fun'
- (d) 以上都不是

答案：(b) 在 C++ 中函数必须有返回类型。

### 91. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ student s;
    S.m=9;
    s=S;
    s.fun(); }
```

- (a) 9
- (b) 0
- (c) 不可预测
- (d) 错误

答案：(a) 这按预期工作。

### 96. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    void fun()
    { cout<<m; }
}S;
int main()
{ S.m=9;
    student s(S);
    s.fun(); }
```

- (a) 9
- (b) 0
- (c) 不可预测
- (d) 错误

答案：(a) 这是从另一个对象创建对象的另一种方式。其工作原理将在后续章节中解释。

### 97. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    void fun()
    { cout<<m; }
}S;
int main()
{ S.m=9;
    student s(S);
    s.m=7;
    S.fun(); }
```

- (a) 9
- (b) 0
- (c) 不可预测
- (d) 错误

答案：(a) 这是从另一个对象创建对象的另一种方式。其工作原理将在后续章节中解释。

- (a) 9
- (b) 7
- (c) 不可预测
- (d) 错误

答案：(a) 新对象中的更改不会反映到被引用对象的值上。

### 98. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
class student
{ protected:
    int m;
    public:
    void fun()
    { m=9;
        cout<<m; }
}S;
int main()
{ S.fun(); }
```

- (a) 9
- (b) 0
- (c) 不可预测
- (d) 错误

答案：(a) 类成员可以访问 'protected' 成员。

### 99. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
class student
{ private:
    int m;
    public:
    void fun()
    { m=9;
        cout<<m; }
}S;
int main()
{ S.fun(); }
```

- (a) 9
- (b) 0
- (c) 不可预测
- (d) 错误

答案：(a) 类成员可以访问 'private' 成员。

### 100. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
class student
{ void game()
{ m=8; }
private:
int m;
public:
void fun()
{
game();
cout<<m; }
}S;
int main()
{ S.fun(); }
```

- (a) 8
- (b) 0
- (c) 不可预测
- (d) 错误

答案：(a) 成员函数可以调用任何成员函数。函数可以访问任何数据成员。因此它按预期工作。

### 101. 代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class student
{ protected:
int m;
public:
void fun()
{ game();
cout<<m; }
}S;
void game()
{ cout<< "game " ; }
int main()
{ S.m=8;
S.fun(); }
```

- (a) game 8
- (b) game
- (c) 不可预测
- (d) 错误

答案：(d) 成员函数不能调用非成员函数。

### 102. 代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
class sub
{ void fun()
{ cout<< "sub-class"; }
}D;
}S;
int main()
{ S.D.fun(); }
```

- (a) 子类
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

答案：(b) 嵌套类的函数可从 main 访问。但这里内部类的函数 'fun()' 处于私有作用域。

### 103. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
class sub
{ public:
void fun()
{ cout<< "sub-class"; }
}D;
}S;
int main()
{ S.D.fun(); }
```

- (a) 子类
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

答案：(a) 现在可以访问该函数。

### 104. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
```
