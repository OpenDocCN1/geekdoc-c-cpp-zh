
```cpp
int main()
{ S.m=8;
  cout<<S.m<< " "<<S1.m; }
```

- (a) 8 8
- (b) 8 0
- (c) 错误
- (d) 不可预测

答案：(b) 这是创建多个对象的一种方式。

## 43. 代码的输出是什么？(L1)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
int m=9;
}S,S1;
int main()
{ S.m=8;
cout<<S.m<< " "<<S1.m; }
```

- (a) 8 8
- (b) 8 9
- (c) 错误
- (d) 不可预测

答案：(b) 未初始化的对象会获得默认值。

## 44. 代码的输出是什么？(L1)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
int m; };
int main()
{ student S;
S.m=8;
cout<<S.m; }
```

- (a) 8
- (b) 0
- (c) 错误
- (d) 不可预测

答案：(a) 这是在 main 内创建对象的一种方式。

## 45. 代码的输出是什么？(L1)

```cpp
#include<iostream>
using namespace std;
class student;
class student
{ public:
int m; };
int main()
{ student S;
S.m=8;
cout<<S.m; }
```

- (a) 8
- (b) 0
- (c) 错误
- (d) 不可预测

答案：(a) 新语句 'class student;' 称为类的前向声明。它用于告知编译器这样的类将在稍后定义。这在声明多个类并在它们之间通信时很有用。但强制要求所有类都应在 'main()' 之前定义。否则会抛出类型不完整的错误。

## 46. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
int m;
}S;
int main()
{ student S;
S.m=8;
cout<<S.m; }
```

- (a) 8
- (b) 0
- (c) 错误
- (d) 不可预测

答案：(a) 实际上 main 内的对象 'S' 是局部变量。而类声明之后的对象是全局的。

## 52. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m; }
    student S;
    int main()
    { S.m=8;
    cout<<S.m; }
```

- (a) 8
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

答案：(b) 这是不合法的。

## 53. 代码抛出的错误将包含哪一部分？(L4)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m; }
    student S;
    int main()
    { S.m=8;
    cout<<S.m; }
```

- (a) 在 'S' 之前应有初始化器
- (b) 在 'student' 之前应有 ';'
- (c) 无效的实例声明
- (d) 以上都不是

答案：(a) 这完全是由于实例声明的混淆造成的。

## 54. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m; }
    (student) S;
    int main()
    { S.m=8;
    cout<<S.m; }
```

- (a) 8
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

答案：(b) 这里也会发生同样的情况。

## 55. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    class subject
    { public:
        char grade;
    }sb;
}S;
int main()
{ S.m=8;
    cout<<S.m; }
```

- (a) 8
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

答案：(a) 一个类可以位于另一个类内部。

## 56. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    class subject
    { public:
        char grade;
    }sb;
}S;
int main()
{ sb.grade= 'A';
    cout<<sb.grade; }
```

- (a) A
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

答案：(b) 这里的对象位于外部类内部，因此没有外部对象就无法访问它。

## 57. 代码将抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    class subject
    { public:
        char grade;
    }sb;
}S;
int main()
{ subject sb;
    sb.grade= 'A';
    cout<<sb.grade; }
```

- (a) 'sb' 未声明
- (b) 'sb' 在此作用域中未声明
- (c) 未知变量 'sb'
- (d) 'sb' 没有成员 'grade'

答案：(b) 这是因为 'sb' 被视为 'class student' 的成员。

## 58. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    class subject
    { public:
        char grade;
    }sb;
}S;
int main()
{ S.sb.grade= 'A';
    cout<<S.sb.grade; }
```

- (a) A
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

答案：(a) 这样能正常工作，因为 'sb' 被视为 'class student' 的对象。

## 59. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    class subject
    { public:
        char grade; };
}S;
int main()
{ subject sb;
    sb.grade= 'A';
    cout<<sb.grade; }
```

- (a) A
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

答案：(b) 在另一个类内部定义的类不能被其他类访问。

## 60. 代码将抛出什么错误？(L4)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    class subject
    { public:
        char grade; };
}S;
int main()
{ subject sb;
    sb.grade= 'A';
    cout<<sb.grade; }
```

- (a) 'subject' 在此作用域中未声明
- (b) 在 'sb' 之前应有 ';'
- (c) 'sb' 在此作用域中未声明
- (d) 以上所有

答案：(d) 'subject' 无法从外部访问。

## 61. 代码的输出是什么？(L3)

```cpp
    #include<iostream>
    using namespace std;
    class student
    { public:
        int m;
        class subject
        { public:
            char grade; };
    }S;
    int main()
    { S.subject sb;
      sb.grade= 'A';
      cout<<sb.grade; }
```

- (a) A
- (b) 不可预测
- (c) 错误
- (d) 以上都不是

答案：(c) 这不是为其他类内部的类创建对象的合法方式。

## 62. 代码将抛出什么错误？(L4)

```cpp
    #include<iostream>
    using namespace std;
    class student
    { public:
        int m;
        class subject
        { public:
            char grade; };
    }S;
    int main()
    { S.subject sb;
      sb.grade= 'A';
      cout<<sb.grade; }
```

- (a) 'sb' 在此作用域中未声明
- (b) 在 'sb' 之前应有 ';'
- (c) 'class student::subject' 的使用无效
- (d) 'a' 和 'b' 两者
- (e) 'a'、'b' 和 'c'

答案：(e) 不能在外层类之外为定义在其他类内部的类创建对象。

## 63. 代码将抛出什么错误？(L4)

```cpp
    #include<iostream>
    using namespace std;
    class student
    { public:
        int m;
        class student
        { public:
            char grade; };sb;
    }S;
    int main()
    { S.m=9;
      cout<<S.m; }
```

- (a) 重复声明 'class student'
- (b) 'class student' 不完整
- (c) 构造函数的使用无效
- (d) 'student::student' 与其声明所在类同名
- (e) 无错误

答案：(d) 在类内部定义同名类是不可能的。

## 64. 代码抛出的错误将包含哪一部分？(L4)

```cpp
    #include<iostream>
    using namespace std;
    class student
    { public:
        int m; }S;
    class student
    { public:
        char grade; };sb;
    int main()
    { S.m=9;
      cout<<S.m; }
```

- (a) 重复声明 'class student'
- (b) 重新定义 'class student'

答案：(a) 这是创建成员函数的一种方式。

## 74. 代码的输出是什么？(L1)

```cpp
#include<iostream>
using namespace std;
class student
{ void fun()
    { cout<<m;}
  public:
    int m; };S;
int main()
{ S.m=9;}
```

- (a) 不打印任何内容
- (b) 不可预测的符号
- (c) 错误
- (d) 以上都不是

答案：(a) 成员函数也可以是私有的。

## 75. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    void fun(); };S;
void student::fun()
{ cout<<m;}
int main()
{ S.m=9;
  S.fun();}
```

- (a) 9
- (b) 0
- (c) 错误
- (d) 以上都不是

答案：(a) 这是在类内声明函数并在类外定义函数的方式。在类内定义称为内联定义。

## 76. 代码的输出是什么？(L2)

```cpp
#include<iostream>
using namespace std;
class student
{ void fun();
  public:
    int m; };S;
void student::fun()
{ cout<<m;}
int main()
{ S.m=9;}
```

- (a) 不打印任何内容
- (b) 不可预测
- (c) 错误
- (d) 以上都不是

答案：(a) 即使是私有函数也可以这样定义。

## 77. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    void fun(); };S;
student::fun()
{ cout<<m;}
int main()
{ S.m=9;
  S.fun();}
```

- (a) 9
- (b) 0
- (c) 错误
- (d) 以上都不是

答案：(c) 当定义未指定返回类型时，它将被视为 'int'。由于定义与声明不一致，因此会抛出一些错误。

## 78. 代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int m;
    void fun(); };S;
student::void fun()
{ cout<<m;}
int main()
{ S.m=9;
  S.fun();}
```
