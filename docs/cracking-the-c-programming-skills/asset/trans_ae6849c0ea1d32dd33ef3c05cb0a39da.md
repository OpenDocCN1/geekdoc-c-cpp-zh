
```cpp
{ public:
    class sub
    { public:
        void fun()
        { cout<< "sub-class";}
    }D;
}S;
int main()
{ S.D.fun();}
```

- (a) sub-class
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) 现在可以访问该函数。

## 105. 代码的输出是什么？（L4）

```cpp
#include<iostream>
using namespace std;
class student
{ class sub
    { public:
        void fun()
        { cout<< "sub-class";}
    };
    public: sub D;
}S;
int main()
{ S.D.fun();}
```

- (a) sub-class
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) 这也是正确的。尽管该类定义在私有作用域中，但该类的对象在公有作用域中，因此可以轻松访问它。

## 106. 代码的输出是什么？（L4）

```cpp
#include<iostream>
using namespace std;
class student
{ class sub
    { public:
        void fun();
    };
public:
    void sub::fun()
    { cout<< "sub-class";}
    sub D;
}S;
int main()
{ S.D.fun();}
```

- (a) sub-class
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (b) 报错信息：“无法在 student 内部使用 ‘::’ 运算符定义成员函数 ‘student::sub::fun’。”

## 107. 代码的输出是什么？（L4）

```cpp
#include<iostream>
using namespace std;
class student
{ class sub
    { public:
        void fun();
    };
    public:
        sub D;
}S;
void student::sub::fun()
{ cout<< "sub-class";}
int main()
{ S.D.fun();}
```

- (a) sub-class
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) 这是正确的定义。由于该类被限定在内部类的作用域内，在显式定义函数时，需要完整的作用域层级。

## 108. 代码会抛出什么错误？（L4）

```cpp
#include<iostream>
using namespace std;
class student
{ class sub
    { public:
        void fun()
        { cout<< "sub-class";}
    }D;
    public:
    void fun()
    { D.fun(); }
}S;
int main()
{ S.fun(); }
```

- (a) sub-class
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) 即使是这样的写法也能正常工作。

## 112. 代码的输出是什么？（L4）

```cpp
#include<iostream>
using namespace std;
class student
{ public:
      int c;
      int *f;
};
int main()
{ S.c = 3;
      S.f = &(S.c);
      cout<<*(S.f); }
```

- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) 类成员也可以是指针。

## 113. 代码的输出是什么？（L4）

```cpp
#include<iostream>
using namespace std;
class student
{ public:
      int *f;
};
int main()
{ int c = 3;
      S.f = &c;
      cout<<*(S.f); }
```

- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) 指针成员也可以指向非成员。

## 114. 代码的输出是什么？（L4）

```cpp
#include<iostream>
using namespace std;
class student
{ public:
      int c;
      int *f;
};
int main()
{ S.c = 3;
      S.f = &S.c;
      cout<<*S.f; }
```

- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) `.` 运算符的优先级高于 `*` 和 `&` 运算符，所以代码仍然正确运行。

## 115. 代码的输出是什么？（L4）

```cpp
#include<iostream>
using namespace std;
class student
{ public:
      int *f;
      int fun()
      { return 3; }
};
int main()
{ S.f = &(S.fun());
      cout<<*(S.f); }
```

- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (b) 指针不能指向函数。这主要是因为这里间接指向了一个常量，这是不可能的。

## 116. 代码会抛出什么错误？（L4）

```cpp
#include<iostream>
using namespace std;
class student
{ public:
    int *f;
    int fun()
    { return 3;}
}S;
int main()
{ S.f = &(S.fun());
  cout<<*(S.f); }
```

- (a) 对常量地址“&”的访问无效
- (b) 一元“&”操作数需要左值
- (c) 一元运算符“&”的操作数无效
- (d) 以上都不是

**答案：** (b) 编译器只期望左值和表达式。

## 117. 代码的输出是什么？（L3）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    void fun()
    { cout<<f;}
}S;
int main()
{ stud *C;
    C = &S;
    *C.f = 3;
    *C.fun(); }
```

- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (b) 对象可以拥有指针，但不应像这样用于访问。

## 118. 代码会抛出什么错误？（L4）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    void fun()
    { cout<<f;}
}S;
int main()
{ stud *C;
    C = &S;
    *C.f = 3;
    *C.fun(); }
```

- (a) 在“*C.f = 3”中“C”之前需要“(”
- (b) “*”操作数的左值无效
- (c) 对“stud”类的指针无效使用“.”运算符
- (d) 以上都不是

**答案：** (d) 它抛出错误：“请求‘C’中的成员‘f’，而‘C’是指针类型‘stud*’（也许您想使用‘->’？）”。这是对象指针的语法。

## 119. 代码的输出是什么？（L3）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    void fun()
    { cout<<f;}
}S;
int main()
{ stud *C;
    C = &S;
    C->f = 3;
    C->fun(); }
```

- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) ‘->’被称为箭头运算符。它必须用于类对象的指针。

## 120. 代码的输出是什么？（L3）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    void fun()
    { cout<<f; }
}S;
int main()
{ S.f = 2;
    ((stud *)this)->fun(); }
```

- (a) 2
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (b) ‘this’指针只能在类内部使用。

## 125. 代码会抛出什么错误？（L5）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    void fun()
    { cout<<f; }
}S;
int main()
{ S.f = 2;
    ((stud *)this)->fun(); }
```

- (a) 在非成员函数中无效使用‘this’
- (b) 在非成员中使用了‘this’
- (c) ‘this’的使用未映射到类
- (d) 以上都不是

**答案：** (a) ‘this’只能在成员函数内部使用。

## 126. 代码的输出是什么？（L5）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
}S;
class blo
{ public:
    void fun()
    { cout<<((stud *)this)->f; }
}D;
int main()
{ S.f = 2;
    D.fun(); }
```

- (a) 2
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (d) 它输出“0”。这是因为“2”被赋值给了特定对象“S”，而‘this’指针调用的是通用的函数，而不是特定于“S”的函数。

```cpp
int main()
{ cout<<"this in different class"; }
```

- (a) 这是不同的类
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) ‘this’指针也可以在不同的、无关的类中使用。

## 127. 代码的输出是什么？（L5）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
}S;
class blo
{ public:
    void fun()
    { cout<<((stud *)this)->f; }
}D;
int main()
{ S.f = 2;
    D.fun(); }
```

- (a) 2
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (d) 它输出“0”。这是因为“2”被赋值给了特定对象“S”，而‘this’指针调用的是通用的函数，而不是特定于“S”的函数。

## 128. 代码的输出是什么？（L5）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    static int f;
}S;
int stud::f = 3;
class blo
{ public:
    void fun()
    { cout<<((stud *)this)->f;}
}D;
int main()
{ D.fun(); }
```

- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (a) `static`变量对类来说是共享的，因此会输出该值。`static`变量的详细内容和使用将在后续章节中讨论。

## 129. 代码的输出是什么？（L5）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    void fun()
    { cout<<f; }
}S;
class blo
{ public:
    void fun()
    { ((stud *)this)->fun(); }
}D;
int main()
{ D.fun(); }
```

- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (c) 当对象被具体声明但被一般地调用时，变量会得到垃圾值。

## 130. 代码的输出是什么？（L5）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    void fun()
    { cout<<f; }
}S;
class blo
{ public:
    void fun(int a)
    { if(a%2 == 0)
        ((stud *)
    this)->fun();
    else
        cout<<((stud *)this)->fun(); }
}D;
int main()
{ D.fun(7); }
```

- (a) 3
- (b) 错误
- (c) 不可预测
- (d) 以上都不是

**答案：** (b) 它试图从一个‘void’函数中获取值并打印。

## 131. 代码的输出是什么？（L5）

```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    void fun()
    { cout<<f; }
}S;
class blo
{ public:
    void fun(int a)
    { if(a%2 == 0)
        ((stud *)
    this)->fun();
    else
        cout<<((stud *)this)->fun(); }
}D;
int main()
{ D.fun(6); }
```

