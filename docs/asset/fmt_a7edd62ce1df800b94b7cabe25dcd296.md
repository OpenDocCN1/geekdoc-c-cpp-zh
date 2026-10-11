
# 8 多态

```cpp
using namespace std;

class complex            //定义复数类
{
public:
    //外部接口
    complex(double r=0.0, double i=0.0){real=r;imag=i}//构造函数
    complex operator + (complex c2); //重载运算符 + 的成员函数
    complex operator - (complex c2); //重载运算符 - 的成员函数
    void display(); //输出复数
```

| `complex` |
| --- |
| - real : double |
| - imag : double |
| + `complex`(r : double = 0.0, i : double = 0.0) |
| + `operator +`(c2 : `complex`) : `complex` |
| + `operator -`(c2 : `complex`) : `complex` |
| + `display()` : void |

![](img/5618306d085ac1bac8275d6c4c5bbf2a_336_0.png)

```cpp
private: //私有数据
double real; //复数的实部
double imag; //复数的虚部
```

```cpp
complex complex::operator +(complex c2)
//重载函数的实现
{
  return complex(real+c2.real, imag+c2.imag);
//创建一个临时对象以返回结果
}
```

```cpp
complex complex::operator -(complex c2)
//重载函数的实现
{
  return complex(real-c2.real, imag-c2.imag);
//创建一个临时对象以返回结果
}
```

```cpp
void complex::display() {
  cout<<real<<","<<imag<<endl;
}
```

```cpp
int main() {
  complex c1(5,4),c2(2,10),c3; //声明复数对象
  cout<<"c1=";c1.display();
  cout<<"c2=";c2.display();
  c3=c1-c2; //复数减法运算
  cout<<"c3=";c3.display();
  c3=c1+c2; //复数加法运算
  cout<<"c3=";c3.display();
  return 0;
}
```

在示例中，复数的加减法被重载为复数类的成员函数。程序的输出结果为

```
c1=(5,4)
c2=(2,10)
c3=(3,-6)
c3=(7,14)
```

## 322 8 多态

```cpp
public:
    // 外部接口
    Clock(int NewH=0, int NewM=0, int NewS=0);
    void ShowTime();
    Clock& operator ++(); // 重载前置一元运算符
    Clock operator ++(int); // 重载后置一元运算符
private:
    // 私有数据成员
    int Hour, Minute, Second;
};
Clock::Clock(int NewH, int NewM, int NewS) // 构造函数
{
    if(0 <= NewH && NewH < 24 && 0 <= NewM && NewM < 60 && 0 <= NewS && NewS < 60)
    {
        Hour = NewH;
        Minute = NewM;
        Second = NewS;
    }
    else
        cout << "Time error!" << endl;
}
void Clock::ShowTime() // 显示时间的函数
{
    cout << Hour << ":" << Minute << ":" << Second << endl;
}
Clock& Clock::operator ++() // 前置
// 一元运算符重载
{
    Second++;
    if(Second >= 60)
    {
        Second = Second - 60;
        Minute++;
        if(Minute >= 60)
        {
            Minute = Minute - 60;
            Hour++;
            Hour = Hour % 24;
        }
    }
    return *this;
}
Clock Clock::operator ++(int) // 后置
// 一元运算符重载
```

```cpp
{ 
    Clock old = *this;
    ++(*this);
    return old;
}
int main() {
  Clock myClock(23,59,59);
  cout << "First time output:";
  myClock.ShowTime();
  cout << "Show myClock:";
  (myClock++).ShowTime();
  cout << "Show +myClock:";
  (+myClock).ShowTime();
}
```

在示例中，我们作为 `Clock` 类的成员重载了前置 `++` 和后置 `++` 用于时间递增。前置运算符重载与后置运算符重载之间最重要的区别在于重载函数的形式参数。根据语法，前置一元运算符的成员函数没有形式参数，而对于后置一元运算符，则需要一个整数参数。该整数参数在函数体中并不使用，它仅用于区分前置和后置。因此，参数列表可以只包含类型名而不包含参数名。程序的执行结果如下。

First time output:23:59:59
Show myClock: 23:59:59
Show+myClock: 0:0:1

## 8.2.3 作为友元函数的重载运算符

运算符也可以重载为类的友元函数。这样它就可以自由地访问类的任何数据成员。在这里，所有的操作数都需要通过形式参数列表传递。参数列表中从左到右的参数顺序即为操作数的顺序。

对于二进制运算符 `B`，如果它有一个操作数是类 `A` 的对象，那么 `B` 就可以重载为类 `A` 的友元函数。该函数有两个参数，其中一个参数的类型是类 `A`。重载后，表达式 `oprd1 B oprd2` 等同于调用函数 `operator B(oprd1, oprd2)`。

对于前置一元运算符 `U`（例如 `-`），为了实现操作 `U oprd`（其中 `oprd` 是类 `A` 的对象），`U` 可以重载为类 `A` 的函数调用。形式参数是类 `A` 的对象 `oprd`。重载后，表达式 `U oprd` 等同于调用函数 `operator U(oprd)`。

对于后置 `++` 和 `--`，为了实现表达式 `oprd++` 或 `oprd--`（其中 `oprd` 是类 `A` 的对象），这些运算符可以重载为类 `A` 的友元函数，并且有两个形式参数：第二个参数用于与前置运算符区分开。重载后，表达式 `oprd++` 和 `oprd--` 等同于调用函数 `operator++(oprd, o)` 和 `operator--(oprd, o)`。

示例 8.3：作为友元函数重载复合运算符 `=` 和 ``。在示例中，运算符 `+` 和 `-` 被重载为 `complex` 类的友元函数，用于实现加法和减法。问题如图 8.2 所示。由于两个操作数都是复杂的，因此函数有两个形式参数。在 324 8 多态节中提到，如果运算符被重载为友元函数，则所有操作数必须通过形式参数列表传递。与示例 8.1 相比，`main()` 函数没有变化。在这里我们只引入了简单的运算符重载。某些运算符（如 `[]` 和类型转换）的重载在某种程度上不同，它们在本章中省略，将在以后介绍。在示例中，所有操作数必须通过形式参数列表传递。

## 326 8 多态

## 8.3 虚函数

在 7.7 节中，我们介绍了一个员工管理系统程序。该示例留有一个待解决的问题，即如何利用迭代处理相同对象。为了实现这一点，我们将示例 7.10 中的 `main()` 修改为以下程序并观察结果。

```cpp
#include<iostream>
#include"employee.h"
using namespace std;
int main()
{
  manager m1;
  technician t1;
  salesmanager sm1;
  salesman s1;
  employee *emp[4]={&m1,&t1,&sm1,&s1};
  // 指针数组中的对象地址
  int i;
  for(i=0;i<4; i++){
    emp[i]->pay();
    cout<<"employee number"<<emp[i]->GetindividualEmpNo()"current salary"<<emp[i]->GetAccumumPay()<<endl;
  }
}
```

执行结果为：

| employee 1000 current salary 0 |
| employee number 1001 current salary 0 |
| employee number 1002 current salary 0 |
| employee number 1003 current salary 0 |

从执行结果可以看出，派生类的 `pay()` 没有执行。读者可以逐步执行程序，将发现每当基类对象指针调用派生类成员函数时，实际上调用的都是基类成员函数，而不是派生类中的新函数。基类中的 `pay()` 函数不起作用。

虚函数是动态绑定的基础。虚函数必须是非静态成员函数。重载后，虚函数可以实现类家族中的执行多态。

## 8.3 虚函数 — 327

根据类型兼容规则，我们可以使用派生类对象替换基类对象。如果基类指针指向派生类对象，那么我们就可以通过指针访问该对象。问题在于，我们访问的是继承自基类的成员。解决这一问题的方法是：如果基类指针指向派生类对象，且我们想要访问一个与基类成员同名的派生类成员，那么基类中的函数应该声明为虚函数。通过这样做，派生类的不同对象将具有不同的行为，从而实现执行多态。

### 8.3.1 普通虚函数

虚函数的声明语法如下：

```
virtual function type function name(argument list)
{
  function body
}
```

`virtual` 关键字用于限制类定义中的成员函数。虚函数的声明只能出现在类定义中的函数原型声明中，而不能出现在成员函数的实现中。

多态在执行期间必须满足三个条件。第一个条件是类之间存在兼容的赋值规则。第二个条件是虚函数的声明，第三个条件是虚函数是通过成员函数、指针或引用调用的。如果通过对象名访问虚函数，可以在编译期间完成绑定（静态编译），而不需要在执行期间完成。

在 UML 表示中，普通虚函数通过在成员函数前添加 <<virtual>>` 来表示。

示例 8.4：虚成员函数。

该程序是第7章示例 7.4“兼容类型规则”的修改版本。成员函数 `display()` 在基类 `BO` 中被声明为 `virtual`。其他部分没有修改。该程序与示例 7.4 程序的区别在于，基类指针指向的派生类对象的虚成员函数可以通过基类指针访问。派生关系如图 8.3 所示的 UML 表示，其中类 `BO` 有一个虚函数 `display()`。

```cpp
//8_4.cpp
#include <iostream>
using namespace std;
```

## 328 — 8 多态性

| B0 |
| :--- |
| <<virtual>> + display() : void |
| B1 |
| + display() : void |
| D1 |
| + display() : void |

图 8.3：带有虚函数的类 B0 的派生关系 UML 图。

```cpp
//定义基类 B0
class B0 {
public:
    virtual void display() {cout<<"B0::display()"<<endl;}
    //虚成员函数
}
class B1: public B0 //公有派生
{
public:
    void display(){cout<<"B1::display()"<<endl;}
    //虚成员函数
}
class D1: public B1 //公有派生
{
public:
    void display(){cout<<"D1::display()"<<endl;}
    //虚成员函数
}
void fun(B0 *ptr) //普通函数
{
    ptr->display();
}
int main() //main()
{
    B0 b0,*ptr;//声明基类对象和指针
    B1 b1;//声明派生类对象
}
```

```cpp
D1 d1; //声明派生类对象
p=&b0;
fun(p); //调用类 B0 的成员函数
p=&b1;
fun(p); //调用派生类 B1 的成员函数
p=&d1;
fun(p); //调用派生类 D1 的成员函数
}
```

类 `BO`、`B1` 和 `D1` 属于同一个类族。它们以公有的方式派生，因此符合兼容类型规则。同时，基类 `BO` 中的成员函数 `display()` 被声明为 `virtual`。在程序中通过对象指针访问该成员函数，因此绑定在执行时完成，从而实现了多态。我们可以使用基类指针访问所指向对象的成员，这允许对同类族的对象进行统一处理。程序更加简洁高效。程序的执行结果如下：

| BO::display() |
| :--- |
| B1::display() |
| D1::display() |

在程序中，派生类没有显式地声明虚函数。系统将遵循以下规则判断派生类成员函数是否为虚函数。

- 如果该函数与某个基类虚函数同名。
- 如果该函数的名称、参数个数相同，且参数类型与基类虚函数对应。
- 如果该函数的返回值相同，或者指针和引用的返回值与基类虚函数相同，且满足赋值规则。

在检查了名称、参数和返回值后，如果派生类满足上述所有条件，则被识别为虚函数。在这里，派生类的虚函数覆盖了基类的虚函数。而且，派生类的虚函数还会隐藏通过同名函数进行其他形式的重载。

当基类构造函数调用虚函数时，不会调用派生类中的虚函数。假设有一个基类 `Base` 和一个派生类 `Derived`。它们都拥有虚函数 `virt()`。如果 `Base::Base()` 调用虚函数 `virt()`，则调用的是 `Base::virt()`。

347

同样，当基类析构函数调用虚函数时，不会调用派生类中的虚函数。假设有一个基类 `Base` 和一个派生类 `Derived`。它们都拥有虚函数 `virt()`。如果 `Base::~Base()` 调用虚函数 `virt()`，则调用的是 `Base::~virt()`。

C++ 不允许声明虚构造函数，但允许声明虚析构函数。

### 8.3.2 虚析构函数

虚析构函数的语法如下：

```
virtual ~name();
```

如果类的析构函数是虚的，那么该类所有的析构函数都是虚的。将析构函数设置为虚后，指针和引用将动态绑定以实现多态。总结来说，如果可能通过基类指针调用对象的析构函数，且要析构的对象是一个具有析构函数的类对象，那么基类的析构函数应该是虚函数。

示例 8.5：虚析构函数的示例。

注意，以下程序没有虚析构函数。

```cpp
//8_5.cpp
#include <iostream>
using namespace std;
class Base
(
348
## 8.3 虚函数
public:
```cpp
~Base(){ cout<<"Base destructor\n";
};
```

```cpp
class Derived : public Base
{
public:
  Derived();
  ~Derived();
private:
  int *i_pointer;
};
```

```cpp
Derived::Derived()
{  i_pointer=new int(0); 
}
```

```cpp
Derived::~Derived()
{
  cout<<"Derived destructor\n"
  delete i_pointer;
}
```

```cpp
void fun(Base* b)
{ delete b; }
```

```cpp
int main()
{
  Base *b=new Derived();
  fun(b);
}
```

执行期间的输出信息为：

Base destructor

这说明当通过基类指针删除派生类对象时，调用的是基类析构函数而不是派生类析构函数。动态分配的派生类对象内存没有被释放，导致了内存泄漏。也就是说，`i_pointer` 指向的内存对象对象消失后没有使用或释放。对于需要大量内存且运行时间较长的程序，重复这种错误是危险的。它最终会导致内存不足错误并导致程序终止。

避免这种错误的有效方法是将析构函数声明为虚函数：

```cpp
class Base {
public:
    virtual ~Base(){ cout<< "Base destructor\n";}
};
```

执行期间的输出信息为：

| Derived destructor |

| Base destructor |
