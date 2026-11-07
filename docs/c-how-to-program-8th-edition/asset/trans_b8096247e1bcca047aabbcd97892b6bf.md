
Employee的Date成员对象在Employee构造函数的成员初始化列表（图10.11，第14-15行）中被初始化，此时会调用类Date的默认拷贝构造函数。由于该构造函数是由编译器隐式定义的，因此它不包含任何输出语句来演示何时调用它。

类Date和类Employee各自包含一个析构函数（分别为图10.9的第33-38行和图10.11的第33-37行），当类的对象被析构时会打印一条消息。这使我们能够在程序输出中确认：对象是*由内向外*构造的，而以*相反*顺序、*由外向内*析构的（即，Date成员对象在包含它们的Employee对象之后被销毁）。注意图10.12输出的最后四行。最后两行是Date析构函数分别对日期对象hire（第10行）和birth（第9行）运行的输出。这些输出确认，在main中创建的三个对象按照构造顺序的*相反*顺序被析构。Employee析构函数的输出位于底部起第五行。输出窗口底部起第四行和第三行显示了Employee的成员对象hireDate（图10.10，第22行）和birthDate（图10.10，第21行）的析构函数运行情况。这些输出确认Employee对象是*由外向内*析构的——即，Employee析构函数先运行（输出显示在输出窗口底部起第五行），然后成员对象按照构造时的*相反顺序*被析构。string类的析构函数不包含输出语句，因此我们看不到firstName和lastName对象的析构。同样，图10.12的输出也没有显示birthDate和hireDate成员对象的构造函数运行情况，因为这些对象是使用编译器提供的Date类默认拷贝构造函数初始化的。

## 如果不使用成员初始化列表会怎样？

如果成员对象未通过成员初始化器进行初始化，则会隐式调用该成员对象的默认构造函数。默认构造函数设置的任何值都可以通过设置函数覆盖。然而，对于复杂的初始化，这种方法可能需要大量额外的工作和时间。

> **常见编程错误10.6**
> 
> 如果成员对象没有使用成员初始化器进行初始化，并且该成员对象的类没有提供默认构造函数（即，该成员对象的类定义了一个或多个构造函数，但没有一个是默认构造函数），则会发生编译错误。

![](img/bfd978e7e9b192bab46ec2a89e481263_461_0.png)

> **性能提示10.2**
> 
> 通过成员初始化器显式地初始化成员对象。这消除了“双重初始化”成员对象的开销——一次是在调用成员对象的默认构造函数时，另一次是在构造函数体内（或之后）调用设置函数来初始化该成员对象时。

![](img/bfd978e7e9b192bab46ec2a89e481263_461_1.png)

> **软件工程观察10.6**
> 
> 如果类成员是另一个类的对象，将该成员对象设为public并不会违反该成员对象私有成员的封装和信息隐藏。但是，它确实违反了包含类的实现的封装和信息隐藏，因此类类型的成员对象应该像所有其他数据成员一样保持private。

![](img/bfd978e7e9b192bab46ec2a89e481263_461_2.png)

## 10.4 友元函数和友元类

类的**友元函数**定义在该类的作用域之外，但有权访问该类的非公有（和公有）成员。独立函数、整个类或其他类的成员函数都可以被声明为另一个类的友元。

使用友元函数可以提高性能。本节给出了一个关于友元函数如何工作的机械示例。在本书后面，友元函数将被用于重载运算符，以便用于类对象（第11章），并用于创建迭代器类（第20章，自定义模板化数据结构）。迭代器类的对象可以连续地选择容器类中的项目，或对它们执行操作。容器类的对象可以存储项目。当成员函数无法用于某些操作时，使用友元通常是合适的，我们将在第11章中看到。

要将一个函数声明为类的友元，请在类定义中的函数原型前加上关键字`friend`。要将类`ClassTwo`的所有成员函数声明为类`ClassOne`的友元，请在类`ClassOne`的定义中放置如下形式的声明：

```
friend class ClassTwo;
```

![](img/bfd978e7e9b192bab46ec2a89e481263_462_0.png)

> **软件工程观察10.7**  
> *尽管友元函数的原型出现在类定义中，但友元不是成员函数。*

![](img/bfd978e7e9b192bab46ec2a89e481263_462_1.png)

> **软件工程观察10.8**  
> *private、protected和public的成员访问概念与友元声明无关，因此友元声明可以放在类定义中的任何位置。*

![](img/bfd978e7e9b192bab46ec2a89e481263_462_2.png)

> **良好编程实践10.1**  
> *将所有友元声明放在类定义体内部的前面，并且不要在它们前面加任何访问说明符。*

友谊是授予的，而不是索取的——即，若要让类B成为类A的友元，类A必须显式声明类B是其友元。此外，友元关系既不是对称的，也不是传递的；即，如果类A是类B的友元，类B是类C的友元，那么你不能推断出类B是类A的友元（再次说明，友元关系不是对称的），不能推断出类C是类B的友元（也因为友元关系不是对称的），也不能推断出类A是类C的友元（友元关系不是传递的）。

![](img/bfd978e7e9b192bab46ec2a89e481263_462_3.png)

> **软件工程观察10.9**  
> *面向对象（OOP）社区中的一些人认为“友元”破坏了信息隐藏，并削弱了面向对象设计方法的价值。我们将提供几个合理使用友元的示例。*

### 使用友元函数修改类的私有数据

图10.13是一个机械示例，其中我们定义了友元函数`setX`来设置类`Count`的私有数据成员`x`。友元声明（第9行）按照惯例出现在类定义中的最前面，甚至先于公有成员函数的声明。同样，这个友元声明可以出现在类中的任何位置。

```cpp
// Fig. 10.13: fig10_13.cpp
// Friends can access private members of a class.
#include <iostream>
using namespace std;

// Count class definition
class Count
{
   friend void setX( Count &, int ); // friend declaration
public:
   // constructor
   Count()
      : x( 0 ) // initialize x to 0
   {
      // empty body
   } // end constructor Count

   // output x
   void print() const
   {
      cout << x << endl;
   } // end function print
private:
   int x; // data member
}; // end class Count

// function setX can modify private data of Count
// because setX is declared as a friend of Count (line 9)
void setX( Count & c, int val )
{
   c.x = val; // allowed because setX is a friend of Count
} // end function setX

int main()
{
   Count counter; // create Count object

   cout << "counter.x after instantiation: ";
   counter.print();

   setX( counter, 8 ); // set x using a friend function
   cout << "counter.x after call to setX friend function: ";
   counter.print();
} // end main
```

```
counter.x after instantiation: 0
counter.x after call to setX friend function: 8
```

图10.13 | 友元可以访问类的私有成员。

函数setX（第29-32行）是一个C风格的独立函数——它不是类Count的成员函数。因此，当setX被对象counter调用时，第41行

