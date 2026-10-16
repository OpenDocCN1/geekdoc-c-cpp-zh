
很少有程序不用循环就能写成。例如，我们可能希望给用户几次机会来输入可接受的输入：

```
bool accept3()
{
int tries = 1;
while (tries<4) {
cout << "Do you want to proceed (y or n)?\n"; char answer = 0;
cin >> answer;

// writequestion
// read answer
switch (answer) {
case 'y':
return true;

case 'n':
return false;
default:
cout << "Sorry, I don't understand that.\n"; ++tries; // increment
}
}
cout << "I'll take that for a no.\n";
return false;
}
```

while语句会一直执行，直到其条件变为false。

## 2.2.5 指针、数组和循环

可以这样声明一个元素类型为char的数组：

```
char v[6]; // array of 6 characters
```

类似地，可以这样声明一个指针：

```
char*p; // pointer to character
```

在声明中，[]表示“……的数组”，*表示“指向……的指针”。所有数组的下界都是0，因此v有6个元素，v[0]到v[5]。数组的大小必须是常量表达式（§2.2.3）。指针变量可以保存适当类型对象的地址：

```
char*p = &v[3]; // p points to v's fourth element
```

```
char x = *p; // *p is the object that p points to
```

在表达式中，前缀一元*表示“……的内容”，前缀一元&表示“……的地址”。我们可以用图形表示上述初始化定义的结果：

p:

0: 1: 2: 3: 4: 5: v:

考虑将十个元素从一个数组复制到另一个数组：

```
void copy_fct()
{
int v1[10] = {0,1,2,3,4,5,6,7,8,9};
int v2[10]; // to become a copy of v1
for (auto i=0; i!=10; ++i) // copy elements
v2[i]=v1[i];
// ...
}
```

这个for语句可以读作“将i设为0；当i不等于10时，复制第i个元素并递增i”。应用于整型变量时，递增运算符++只会加1。C++还提供了一种更简单的for语句，称为基于范围的for语句，用于以最简单的方式遍历序列：

```
void print()
{
int v[] = {0,1,2,3,4,5,6,7,8,9};
for (auto x : v) // foreach x in v
cout << x << '\n';
for (auto x : {10,21,32,43,54,65})
cout << x << '\n';
// ...
}
```

第一个基于范围的for语句可以读作“对于v的每一个元素，从第一个到最后一个，将其副本放入x并打印”。注意，当我们用列表初始化数组时，不必指定数组边界。基于范围的for语句可用于任何元素序列（§3.4.1）。

如果我们不想将v中的值复制到变量x中，而只是让x引用某个元素，可以这样写：

```
void increment() {
int v[] = {0,1,2,3,4,5,6,7,8,9};
for (auto& x : v)
++x;
// ...
}
```

在声明中，一元后缀&表示“引用”。引用与指针类似，不同之处在于你不需要使用前缀*来访问引用所引用的值。此外，引用在初始化后不能再引用另一个对象。当运算符（如&、*和[]）用于声明时，被称为声明符运算符：

```
T a[n]; // T[n]: array of n Ts (§7.3)
T* p; // T*: pointer to T (§7.2)
T& r; // T&: reference to T (§7.7)
T f(A); // T(A): function taking an argument of type A returning a result of type T (§2.2.1)
```

我们努力确保指针始终指向某个对象，这样解引用它才是有效的。当我们没有对象可指向，或者需要表示“没有可用对象”的概念（例如，列表的末尾）时，我们给指针赋值为**nullptr**（“空指针”）。所有指针类型共享唯一的**nullptr**：

```
double * pd = nullptr;
Link<Record>* lst = nullptr; // pointer to a Link to a Record
int x = nullptr; // error: nullptr is a pointer not an integer
```

通常明智的做法是检查一个本应指向某对象的指针参数确实指向了某对象：

```
int count_x(char * p, char x)
// count the number of occurrences of x in p[]
// p is assumed to point to a zero-terminated array of char (or to nothing)
{
if (p==nullptr) return 0; int count = 0;
for (; *p!=0; ++p)
if (*p==x)
++count; return count;
}
```

注意，我们可以使用**++**将指针移动到数组的下一个元素，而且如果不需要初始化器，可以省略**for**语句中的初始化器。**count_x()**的定义假定**char***是C风格字符串，即该指针指向一个以空字符结尾的**char**数组。在老代码中，通常使用**0**或**NULL**而不是**nullptr**（§7.2.2）。然而，使用**nullptr**可以消除整数（如**0**或**NULL**）与指针（如**nullptr**）之间可能出现的混淆。

第2.3节 用户自定义类型 47

## 2.3 用户自定义类型

我们把可以从基本类型（§2.2.2）、**const**修饰符（§2.2.3）和声明符运算符（§2.2.5）构建的类型称为*内置类型*。C++的内置类型和操作集合非常丰富，但有意保持在低层次。它们直接而高效地反映了传统计算机硬件的能力。然而，它们并没有为程序员提供方便编写高级应用的高层设施。相反，C++通过一套精密的*抽象机制*增强了内置类型和操作，程序员可以从中构建这样的高层设施。C++的抽象机制主要是为了让程序员设计和实现自己的类型，并配有合适的表示和操作，同时也为了让程序员能简单而优雅地使用这些类型。使用C++抽象机制从内置类型构建出的类型称为*用户自定义类型*。它们被称为类和枚举。本书的大部分内容专门讨论用户自定义类型的设计、实现和使用。本章其余部分介绍用于此目的的最简单、最基本的设施。第3章更完整地描述抽象机制及其支持的编程风格。第4章和第5章概述标准库；由于标准库主要由用户自定义类型组成，它们给出了使用第2章和第3章介绍的语言设施和编程技术可以构建出什么的示例。

### 2.3.1 结构体

构建新类型的第一步通常是将它所需的元素组织成一个数据结构，即结构体（struct）：

```
struct Vector {
int sz; // number of elements
double* elem; // pointer to elements
};
```

这个Vector的第一版由一个int和一个double*组成。可以这样定义Vector类型的变量：

```
Vector v;
```

然而，它本身并没有多大用处，因为v的elem指针没有指向任何东西。为了有用，我们必须给v一些元素来指向。例如，我们可以这样构造一个Vector：

```
void vector_init(Vector& v, int s)
{
v.elem = new double[s]; // allocate an array of s doubles
v.sz = s;
}
```

也就是说，v的elem成员获得由new运算符产生的指针，v的size成员获得元素个数。Vector&中的&表示我们通过非常量引用（§2.2.5，§7.7）传递v；这样，vector_init()就可以修改传递给它的vector。new运算符从称为自由存储区（也称为动态内存和堆；§11.2）的区域分配内存。

Vector的一个简单用法如下：

```
double read_and_sum(int s)
// read s integers from cin and return their sum; s is assumed to be positive
{
Vector v;
vector_init(v,s); // allocate s elements for v
for (int i=0; i!=s; ++i)
cin>>v.elem[i]; // read into elements

double sum = 0;
for (int i=0; i!=s; ++i)
sum+=v.elem[i]; // take the sum of the elements
return sum;
}
```

要让我们的Vector像标准库中的vector一样优雅和灵活，还有很长的路要走。特别是，Vector的使用者必须了解Vector表示的每一个细节。本章剩余部分和下一章将逐步改进Vector，以此作为语言特性和技术的示例。第4章介绍标准库vector，其中包含许多很好的改进；第31章将结合其他标准库设施介绍完整的vector。

我将vector和其他标准库组件用作示例
- 用于说明语言特性和设计技术，
- 以及帮助你学习和使用标准库组件。

不要重新发明标准库组件，如vector和string；直接使用它们。我们使用.（点）通过名字（以及通过引用）访问结构体成员，而通过指针访问结构体成员时使用->。例如：

```
void f(Vector v, Vector& rv, Vector * pv)
{ int i1 = v.sz; int i2 = rv.sz; int i4 = pv->sz;
}
```
 // access through name // access through reference // access through pointer

第2.3.2节 类 49

### 2.3.2 类

将数据与对数据的操作分开定义有其优点，例如可以任意方式使用数据。然而，要让用户自定义类型具备“真正类型”所期望的所有属性，就需要在表示和操作之间建立更紧密的联系。特别是，我们常常希望将表示对用户隐藏，以简化使用、保证数据使用的一致性，并允许我们日后改进表示。要做到这一点，我们必须区分类型的接口（供所有人使用）和其实现（实现可以访问原本不可访问的数据）。支持这一点的语言机制称为类。类被定义为一组成员，这些成员可以是数据、函数或类型成员。接口由类的公有成员定义，私有成员只能通过该接口访问。例如：

```
class Vector {
public:
Vector(int s) :elem{new double[s]}, sz{s} { } // construct a Vector
double& operator[](int i) { return elem[i]; } // element access: subscripting
int size() { return sz; }
private:
double*elem; // pointer to the elements
int sz; // the number of elements
};
```

有了这些，我们就可以定义新类型Vector的变量：

```
Vector v(6); // a Vector with 6 elements
```

我们可以用图形说明Vector对象：
