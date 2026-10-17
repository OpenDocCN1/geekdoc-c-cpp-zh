
```cpp
bookl1(title, price, pages);

// Tape details

cout << "\n ENTER TAPE DETAILS\n";

cout << "\n Title: "; cin >> title;

cout << "\n Price: "; cin >> price;

cout << "\n Play time (mins): "; cin >> time;

tape tape1(title, price, time);

media* list[2];

list[0] = &bookl1;

list[1] = &tape1;

cout << "\n MEDIA DETAILS\n";

list[0] -> display(); // display book details

cout << "\n ...... TAPE ......\n";

list[1] -> display(); // display tape details

return 0;

}
```

程序 9.13 的输出为：

ENTER BOOK DETAILS
Title:Programming_in_ANSI_C
Price: 88
Pages: 400

ENTER TAPE DETAILS

Title: Computing_Concepts
Price: 90
Play time (mins): 55

MEDIA DETAILS

BOOK
....
Title:Programming_in_ANSI_C
Pages: 400
Price: 88

....
TAPE
....
Title: Computing_Concepts
Play time: 55mins
Price: 90

## 虚函数的规则

当为实现后期绑定而创建虚函数时，我们应遵守满足编译器要求的某些基本规则：

1. 虚函数必须是某个类的成员。
2. 它们不能是静态成员。
3. 它们是通过对象指针访问的。
4. 虚函数可以是另一个类的友元。
5. 基类中的虚函数必须被定义，即使它可能未被使用。
6. 基类版本的原型是它对虚函数，并且所有派生类版本必须相同。如果两个同名函数具有不同的原型，C++ 将它们视为重载函数，并且会忽略虚机制。
7. 我们不能有虚构造函数，但可以有虚析构函数。
8. 虽然基指针可以指向任何类型的派生对象，但反之则不行。也就是说，我们不能使用指向派生类的指针来访问基类型的对象。
9. 当基指针指向派生类时，增加或减少它并不会使其指向派生类的下一个对象。它仅相对于其基类型进行增加或减少。因此，我们不应使用此方法将指针移动到下一个对象。
10. 如果虚函数在基类中定义，则不必一定在派生类中重新定义。在这种情况下，调用将调用基函数。

### 9.8 纯虚函数

通常在基类内部声明一个函数为 `virtual`，并在派生类中重新定义它。基类内部的函数很少用于执行任何任务。它充当占位符。例如，我们没有定义 `class media` 的任何对象，因此基类中的 `display()` 函数被定义为空。这样的函数称为“do-nothing”函数。

“do-nothing”函数可定义如下：

```cpp
virtual void display() = 0;
```

这样的函数称为纯虚函数。纯虚函数是在基类中声明但相对于基类没有定义的函数。在这种情况下，编译器要求每个派生类要么定义它，要么将其重新声明为虚函数。请记住，包含纯虚函数的类不能用于声明其自身的对象。如前所述，这样的类是抽象基类。主要目的是为派生类提供一些特征并创建实现运行时多态所需的基指针。

程序 9.14 演示了纯虚函数的使用：

## 程序 9.14 纯虚函数

```cpp
#include <iostream>

using namespace std;

class Balagurasyamy { //base class
public:
    virtual void example()=0; //Notes pure virtual Function Definition
};

class C:public Balagurasyamy { //derived class 1
public:
    void example() {
        cout<<"C text Book written by Balagurasyamy";
    }
};

class coops:public Balagurasyamy { //derived class 2
public:
    void example() {
        cout<<"C++ text Book written by Balagurasyamy";
    }
};

int main() {
nExforsys* arra[2];
 C el;
coops e2;
arra[0]=&e1;
arra[1]=&e2;
arra[0]->example();
arra[1]->example();
return 0;
}
```

### 9.9 虚构造函数和析构函数

“构造函数不能是虚的”。有几个有效理由可以证明这一说法。首先，要创建构造函数的对象，构造函数类必须与类类型相同。但这对于虚拟实现的构造函数是不可能的。其次，在调用构造函数时，虚表尚未创建以解析任何虚函数调用。因此，虚构造函数本身将无处可查。结果，构造函数不能声明为虚。

虚析构函数在 C++ 中却是完全可行的。事实上，在某些情况下其使用也得到推广。一个情况是当我们需要确保在继承层次结构中不同的析构函数按顺序调用时，特别是当基类指针引用派生类型对象时。必须在此注意，继承层次结构中析构函数的调用顺序与构造函数的调用顺序相反。考虑以下使用析构函数的类声明：

```cpp
class A
{
public:
    ~A()
    {
        //Base class destructor
    }
}
class B : public A
{
public:
    ~B()
    {
        //Derived class destructor
    }
}
main()
{
    A *ptr = new B();
    .
    delete ptr;
}
```

在上述类声明中，类 `A` 和派生类 `B` 都有各自的析构函数。现在，一个 `A` 类指针已被分配一个 `B` 类对象。当使用 `delete` 运算符删除此对象指针时，它将触发基类析构函数，而派生类析构函数根本不会被调用。这可能导致内存泄漏情况。为了确保派生类析构函数强制调用，我们必须将基类析构函数声明为 `virtual`，如下所示。

## 摘要

- 多态简单地意味着一个名字具有多种形式。
- 多态有两种类型，即编译时多态和运行时多态。重载的成员函数是通过调用绑定参数的类型和数量来选择的。编译器在编译时就知道这些信息，因此编译器能够在此时为特定调用选择合适的函数。这称为早期绑定或静态绑定或静态链接。它的意思是对象在编译时就绑定到其函数调用。
- 在运行时多态中，合适的成员是在程序运行时选择的。C++借助虚函数支持运行时多态。它被称为晚期或动态绑定，因为合适的函数在运行时动态选择。动态绑定需要指向对象的指针，并且是 C++ 的强大特性之一。
- 对象指针在运行时创建对象时很有用。它可以与箭头一起用于访问对象的公共成员。
- 指针指向一个对象，该对象谨慎地调用成员函数。例如，函数调用 `a.show()` 将指针 `this` 设置为对象 `a` 的地址。
- 基类对象的指针与派生类对象的指针兼容。因此，我们可以使用单个基类对象指针变量来指向基类对象以及派生类对象。
- 当一个函数是虚函数时，C++ 根据基指针所指向的对象的类型，而不是指针的类型来确定在运行时调用哪个函数。通过使基指针指向不同的对象，我们可以执行虚函数的不同版本。
- 运行时多态仅在通过指向基类的指针访问虚函数时才能实现。它不能使用对象名以及点运算符来访问虚函数来实现。
- 我们可以有虚析构函数但不能有虚构造函数。
- 如果在基类中定义了虚函数，它不必一定在派生类中重新定义。在这种情况下，相应的调用将调用基类函数。
- 等同于零的虚函数是纯虚函数。它是在基类中声明但相对于基类没有定义的函数。包含此类纯函数的类称为抽象类。

## 关键术语

`abstract base classes` | `address of operator` | `argument object` | `arrays of pointers` | `arrow operator` | `base address` | `base object` | `base pointer` | `call back function` | `class hierarchy` | `compile time` | `compile polymorphism` | `dereference operator` | `derived object` | `do-nothing` | `function` | `dot operator` | `dynamic binding` | `early binding` | `function overloading` | `function pointer` | `implicit argument` | `indirect operator` | `invoking object` | `late binding` | `new operator` | `null pointers` | `object pointer` | `operator overloading` | `placeholder` | `pointers` | `pointer arithmetic` | `pointers to functions` | `polymorphism` | `pure virtual function` | `run time` | `run polymorphism` | `static binding` | `static linking` | `this pointer` | `virtual constructors` | `virtual destructors` | `virtual function` | `void pointers`

## 复习问题

### 认知领域

- 9.1 解释 C++ 语言中多态的含义。
- 9.2 说明多态是如何在 (a) 编译时和 (b) 运行时实现的。
- 9.3 讨论我们可以通过哪些方式访问对象的公共成员。
- 9.4 说明函数指针；并演示在何种情况下使用此类概念。
- 9.5 举例说明你将如何使用指针为对象数组创建空间。
- 9.6 检查 `this` 指针指向什么。
- 9.7 列出 `this` 指针的应用。
- 9.8 基类类型的指针指向派生类对象。用合适的示例证明你的答案。
- 9.9 表达关于虚函数的内容。
- 9.10 显示虚函数的必要性。
- 9.11 描述何时使虚函数“纯”。概括使函数成为虚函数的影响。
- 9.12 区分早期绑定和晚期绑定。

### 情感领域

- 9.13 为以下陈述的正确性辩护：
  (a) 虚函数用于创建指向基类的指针。
  (b) 虚函数允许我们使用相同的函数调用来调用不同类对象的成员函数。
  (c) 指向基类的指针不能指向派生类对象。
  (d) `this` 指针指向当前用于调用函数的对象。
  (e) `this` 指针可以像其他指针一样使用来访问其指向的对象的成员。
  (f) `this` 指针可以通过分配对象的地址来指向任何对象。
  (g) 纯虚函数强制程序员在派生类内部重新定义虚函数。

## 图例

Precision Valuing/Responding/Organizing Applying Remembering Understanding

## 调试练习

### 9.1 找出以下程序中的错误。

```cpp
#include <iostream>
using namespace std;
class GST
{
    float price;
    float percent;
public:
    void input(float a, float b)
    {
        price = a;
        percent= b;
    }
    void print()
    {
        cout << "price: " << price << "\n";
        cout << "percent: " << percent << "\n";
    }
};
int main()
{
    GST *p[3];
    GST *q=p;
    int i;
    float s,t,f;
    for(i=0; i<3; i++)
    {
        cout<<"Provide the price and percent"<<"
";
        cin>>s>>t;
        p->input(s, t);
        cout<<"you have entered"<<"
";
        q->print();
        f=s*t;
        cout<<"Price after GST: "<<<<f<<"\n";
    }
}
276
Object-Oriented Programming with C++
return 0;
}
```

### 9.2 找出以下程序中的错误。

```cpp
#include <iostream>
using namespace std;
int main ()\
{
    int p=10;
    double q=20.33;
    int *x=&p;
    double *y=&q;
    y=&p;
    x=&q;
    cout << "value 1 :" << p << endl;
    cout << "value 2 :" << q << endl;
    return 0;
}
```

## 试运行练习

### 9.1 当运行以下程序时会发生什么？

```cpp
#include <iostream>
using namespace std;
class B
{
    float b;
public:
    B()
    {
        b = 5.0; 
    }
    void show()
    {
        cout << b << endl;
    }
};
class D : public B
{
    float d;
    float d1;
public:
    D()
    {
        B::B();
        d = 10.0;
    }
    int d = 20.0;
    void show() {
        cout << d << endl;
    }
int main() {
    B ob, *ptr;
    D ob1;
    ptr = &ob1;
    ptr->show();
    cout << ptr << endl;
    ptr++;
    cout << ptr;
    return 0;
}
```

### 9.2 当运行以下程序时会发生什么？

```cpp
#include <iostream>
using namespace std;
int main() {
    int ar[6]={22,5,23,43,54,65};
    int *p;
    p=ar;
    i=p++ - *p--;
    cout << i;
    return 0;
}
```

### 9.3 当运行以下程序时会发生什么？

```cpp
#include <iostream>
using namespace std;
void square(int *snum) {
    cout << "Square of 10 is ";
    *snum *= *snum;
}
int main() {
    int num = 10;
    square(&num);
    cout << num << endl;
    return 0;
}
```

278
Object-Oriented Programming with C++

### 9.4 以下程序的输出是什么？

```cpp
#include <iostream>
using namespace std;
class p
{
public:
    virtual void print()
    {
        cout<<"it is base class \n";
    }
};
class q: public p
{
public:
    void print()
    {
        cout<<"it is Derived class \n";
    }
};
int main()
{
    p *b = new q;
    b->print();
    return 0;
}
```

### 9.5 如果从 `original_base` 类的 `print` 函数中删除 `virtual` 关键字，输出会有什么变化？

```cpp
#include <iostream>
using namespace std;
class original_base
{
public:
    virtual void print()
    {
        cout<<"print version of base class" <<endl;
    }
    void show()
    {
        cout<<"show version of base class" <<endl;
    }
}
class derived_from :public original_base
{
public:
    void print()
    {
        cout<<"print version of derived class" <<endl;
```
