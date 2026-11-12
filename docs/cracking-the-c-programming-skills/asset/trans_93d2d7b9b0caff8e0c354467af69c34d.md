

```cpp
void fun()
{ cout<< b<< " "; }
};
    class dev1 : virtual public base
{ }S;
class dev2 : virtual public base
{ }D;
class dev3 : public dev1, public dev2
{ }E;
    int main()
{ S.b = 3;
  D.b = 2;
  E.b = 5;
  S.fun();
  D.fun();
  E.fun(); }
```

- (a) 3 2 5
- (b) 不可预测
- (c) 错误
- (d) 以上都不是

**答案：(c)** 这是可能的。但继承将是私有模式。因此，'D.base::b' 不可访问。

### 101. 这段代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;
    void fun()
    { cout<< b<< " "; }
};
    class dev1 : virtual public base
{ public:
    int b; }S;
class dev2 : virtual public base
{ }D;
class dev3 : public dev1, public dev2
{ }E;
    int main()
{ S.b = 3;
  D.b = 2;
  E.b = 5;
  S.fun();
  D.fun();
  E.fun(); }
```

- (a) 0 2 5
- (b) 不可预测，取决于编译环境
- (c) 错误
- (d) 以上都不是

**答案：(d)** 它打印 '0 3 0 '。当调用变量时，编译器指向层次结构中最近的变量。因此在 'E.b' 中，初始化的值是 'dev1::b' 而不是 'base::b'。所以当调用 'base::fun()' 时，打印的是 0 而不是 5。

### 102. 这段代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;
    void fun()
    { cout<< b<< " "; }
};
    class dev1 : public base
{ public:
    int b; }S;
class dev2 : public base
{ }D;
class dev3 : public dev1, public dev2
{ }E;
    int main()
{ S.b = 3;
  D.b = 2;
  E.b = 5;
  S.fun();
  D.fun();
  E.fun(); }
```

- (a) 0 2 5
- (b) 不可预测，取决于编译环境
- (c) 错误
- (d) 以上都不是

**答案：(c)** 即使改变了优先项，继承时所有成员仍会随之而来。因此会发生重复，并抛出错误。

### 103. 这段代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class base
{
public:
    int b;
    void fun()
    { cout<< b<< "  "; }
};
class dev1 : virtual public base
{  }S;
class dev2 : virtual public dev1
{  }D;
class dev3 : virtual public dev1
{  }E;
class dev4 : public dev2, public dev3
{  }F;
int main()
{ F.b = 3;
    F.fun(); }
```

- (a) 3
- (b) 什么也不打印
- (c) 错误
- (d) 以上都不是

**答案：(a)** 这按预期工作。

### 104. 这段代码的输出是什么？(L3)

```cpp
#include<iostream>
using namespace std;
class base
{
public:
    int b;
    void fun()
    { cout<< b<< "  "; }
};
    class dev1 : virtual public base
{  }S;
class dev2 : virtual public dev1
{  }D;
class dev3 : virtual public dev1
{  }E;
class dev4 : virtual public dev2, virtual public dev3
{  }F;
int main()
{ F.b = 3;
    F.fun(); }
```

- (a) 3
- (b) 什么也不打印
- (c) 错误
- (d) 以上都不是

**答案：(a)** 这也能正常工作，但在继承 dev4 时指定的 'virtual' 变得无用。

### 105. 这段代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class base
{
public:
    int b;
    void fun()
    { cout<< b<< "  "; }
};
class dev1 : public base
{  }S;
class dev2 : virtual public dev1
{  }D;
class dev3 : virtual public dev1
{  }E;
class dev4 : public dev2, public dev3
{  }F;
int main()
{ F.b = 3;
    F.fun(); }
```

- (a) 3
- (b) 什么也不打印
- (c) 错误
- (d) 以上都不是

**答案：(a)** 即使这样也能正确工作。'virtual' 的必要性仅在层次继承部分。

### 106. 这段代码的输出是什么？(L4)

```cpp
#include<iostream>
using namespace std;
class base
{ };
class dev1 : public base
{ }S;
class dev2 : public dev1
{ }D;
class dev3 : public dev1
{ }E;
class dev4 : public dev2, public dev3
{ }F;
int main()
{ cout<<"fun"; }
```

- (a) fun
- (b) 什么也不打印
- (c) 错误
- (d) 以上都不是

**答案：(a)** 当两个基类都为空时，不存在冲突的可能，可以跳过 'virtual' 关键字。但它没有意义。

### 107. 使用了哪种继承类型？(L3)

```cpp
#include<iostream>
using namespace std;
class base
{ //block }A;
class dev1 : public base
{ //block }S;
class dev2 : public dev1
{ //block }D;
class dev3 : public dev1
{ //block }E;
class dev4 : public dev2, public dev3
{ //block }F;
class dev5 : public dev4
{ //block }V;
int main()
{ //block }
```

- (a) 混合继承
- (b) 层次继承
- (c) 多层继承
- (d) 多重继承

**答案：(a)** 它是简单、多层和层次模式的组合。

### 108. 使用了哪种继承类型？(L3)

```cpp
#include<iostream>
using namespace std;
class base
{ //block }A;
class dev1 : public base
{ //block }S;
class dev2 : public dev1
{ //block }D;
class dev3 : public dev2
{ //block }E;
class dev4 : public dev3
{ //block }F;
class dev5 : public dev3
{ //block }V;
int main()
{ //block }
```

- (a) 混合继承
- (b) 层次继承
- (c) 多层继承
- (d) 多重继承

**答案：(a)** 它先是多层继承，然后是层次继承。

### 109. 使用了哪种继承类型？(L5)

```cpp
#include<iostream>
using namespace std;
class base
{ //block }A;
class dev1 : public base
{ //block }S;
class dev2 : public dev1
{ //block }D;
class dev3 : public dev2
{ //block }E;
class dev4 : public dev3
{ //block }F;
class dev5 : public dev4, public dev3
{ //block }V;
int main()
{ //block }
```

- (a) 混合继承
- (b) 层次继承
- (c) 多层继承
- (d) 多重继承

**答案：(a)** 它被认为是混合继承的一种类型。

### 110. 使用了哪种继承类型？(L5)

```cpp
#include<iostream>
using namespace std;
class base
{ //block }A;
class dev1 : public base
{ //block }S;
class dev2 : public base
{ //block }D;
class dev3 : public dev2 , public dev1
{ //block }E;
int main()
{ //block }
```

- (a) 混合继承
- (b) 层次继承
- (c) 多层继承
- (d) 多重继承

**答案：(a)** 它也被认为是混合继承的一种类型。

### 7. 预测以下程序的输出。(L2)

```cpp
#include <iostream>
using namespace std;
class Inc
{
  private:
    int num;

  public:
  Inc(int b)
  {
  num=b;
  }

    int operator ++() {
    return num=num+1;
    }

  };
int main()
{
  Inc t(10);
  cout<<++t;
  return 0;
}
```

- (a) 错误，因为我们不能对类的实例使用 ++
- (b) 打印 11
- (c) 打印一个垃圾值
- (d) 以上都不是

**答案：(b) 打印 11**

### 8. 默认情况下，编译器重载一个运算符。选择该运算符。(L1)

- (a) =
- (b) *
- (c) ?:
- (d) ==

**答案：(a)** 赋值运算符能够处理任何类型的值和变量。这是通过重载实现的。

### 9. 将一个对象赋值给同类型的另一个对象，这种技术称为什么？(L2)

```cpp
int main()
{
  Inc t(10),t1(0);
  cout<<++t<<endl;
  t1=t;
  cout<<++t1;
    return 0;
}
```

- (a) 拷贝构造函数
- (b) 重载构造函数
- (c) 拷贝运算符
- (d) 重载运算符

**答案：(a) 拷贝构造函数**

### 10. 指出下列关于运算符函数的正确陈述。(L1)

- (a) 它们与成员函数类似，不同之处在于它们有关键字 operator 和待重载的符号
- (b) 返回类型可以是 void
- (c) 它可以按值返回或按引用返回
- (d) 以上所有

**答案：(d) 以上所有**

### 11. 预测以下代码的输出。(L2)

```cpp
#include <iostream>
using namespace std;
class Inc
{
  private:
    int num;
  public:
Inc(int b)
{
num=b;
}
    int operator ++() {
return num=num+1;
    }
};
int main()
{
    Inc t(10),t1(0);
    cout<<++t<<"\t";
    t1=t;
    cout<<++t1;
    return 0;
}
```

- (a) 由于 operator= 没有被重载，赋值 t1=t 是非法的。它会抛出错误
- (b) 11 12
- (c) 11 1
- (d) 11 2

**答案：** (b) t 初始为 10，递增为 11。然后 t1 获得 t 的值，即 11。因此对 t 的进一步递增会得到 12。

### 12. 如何区分后缀和前缀运算符重载？(L1)

- (a) 我们不允许在同一个类中重载这两个运算符
- (b) 我们会将后缀运算符重载为全局函数
- (c) 我们会将前缀运算符重载为全局函数
- (d) 我们会向后缀运算符重载函数传递一个虚拟值

**答案：** (d) 我们会向后缀运算符重载函数传递一个虚拟值

### 13. 找出以下代码的问题。(L2)

```cpp
#include<iostream>
using namespace std;
class Negation
{
    int param1;
    public:
        Negation()
        { }
        Negation(int paramPassed)
        {
            param1=paramPassed;
        }
        int operator +(Negation obj)
        {
            return param1+obj.param1;
        }
        int operator +(int obj)
        {
            return param1+obj;
        }
};
int main()
{
    Negation obj1(100),obj2(200);
    cout<<"add 2 obj->"<<obj1+obj2<<endl;
    cout<<"add a scalar number with obj->"<<obj1<<endl;
}
```

- (a) 我们不能多次重载同一个运算符
- (b) 没有问题，输出为 add 2 obj➔300
  add a scalar number with obj➔300
- (c) 没有问题，输出为 add 2 obj➔300
  add a scalar number with obj➔100
- (d) 以上都不是

**答案：** (b) 它正常工作，符合预期。

### 14. 指出以下程序的输出。(L3)

```cpp
#include<iostream>
using namespace std;
class Negation
{
    int param1;
    public:
        Negation()
        { }
        Negation(int paramPassed)
        {
            param1=paramPassed;
```

