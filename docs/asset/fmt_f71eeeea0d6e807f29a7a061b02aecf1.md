
```
v1 = 9; // error : no conversion from int to vector f(9); // error : no conversion from int to vector }
```

将`()`替换为`{}`后，我们得到：

```
vector<double> v1 {7};

vector<double> v2 = {9};

// OK: v1 has one element (with the value 7) // OK: v2 has one element (with the value 9)

void f(const vector<double>&); void g()

{

v1 = {9}; // OK: v1 now has one element (with the value 9)

f({9}); // OK: f is called with the list {9}

}
```

显然，结果截然不同。
这个例子经过精心设计，给出了最令人困惑的情况示例。请注意，明显的歧义（在人看来而不是编译器）在较长列表的情况下不会出现。例如：

```
vector<double> v1 {7,8,9}; vector<double> v2 = {9,8,7};

// OK: v1 has three elements with values {7,8,9} // OK: v2 has three elements with values {9,8,7}
```

```
void f(const vector<double>&); void g()

{

v1 = {9,10,11}; // OK: v1 now has three elements with values {9,10,11} f({9,8,7,6,5,4}); // OK: f is called with the list {9,8,7,6,5,4}

}
```

类似地，对于非整数类型的元素列表，潜在的歧义也不会出现：

```
vector<string> v1 { “Anya”}; // OK: v1 has one element (with the value “Anya”)

vector<string> v2 = {“Courtney”}; // OK: v2 has one element (with the value “Courtney”)
```

```
void f(const vector<string>&); void g()

{

v1 = {“Gavin”}; // OK: v1 now has one element (with the value “Gavin”) f({“Norah”}); // OK: f is called with the list {“Norah”}

}
```

# 17.4 成员与基类初始化

构造函数可以建立不变量并获取资源。通常，它们通过初始化类的成员和基类来实现这一点。

## 17.4.1 成员初始化

考虑一个可能用于保存小型组织信息的类：

```
class Club {

string name;

vector<string> members;

vector<string> officers;

Date founded;

// ...

Club(const string& n, Date fd);

};
```

`Club`的构造函数将俱乐部名称和成立日期作为参数。成员的构造函数的参数在包含类的构造函数定义中的成员初始化列表中指定。例如：

```
Club::Club(const string& n, Date fd)

: name{n}, members{}, officers{}, founded{fd}

{

// ...

}
```

成员初始化列表以冒号开头，各个成员初始化器用逗号分隔。

成员构造函数在包含类自身构造函数体执行之前被调用（§17.2.3）。构造函数按照成员在类中声明的顺序调用，而不是按照它们在初始化列表中出现的顺序。为避免混淆，最好按成员声明顺序指定初始化器。如果你没弄对顺序，希望编译器给出警告。成员析构函数在类自身析构函数体执行之后，按照构造顺序的逆序调用。

如果成员构造函数不需要参数，则无需在成员初始化列表中提及该成员。例如：

```
Club::Club(const string& n, Date fd)

: name{n}, founded{fd}

{

//...

}
```

这个构造函数与前一个版本等价。在每种情况下，`Club::officers` 和 `Club::members` 都被初始化为没有元素的`vector`。

通常最好明确初始化成员。注意，内置类型的“隐式初始化”成员会被保留为未初始化状态（§17.3.1）。

构造函数可以初始化其类的成员和基类，但不能初始化其成员或基类的成员或基类。例如：

```
struct B { B(int); /*...*/};

struct BB : B { /*...*/ };

struct BBB : BB {

BBB(int i) : B(i) {}; // error : trying to initialize base’s base

//...

};
```

### 17.4.1.1 成员初始化与赋值

对于初始化与赋值含义不同的类型，成员初始化器至关重要。例如：

```
class X {

const int i;

Club cl;

Club& rc;

//...

X(int ii, const string& n, Date d, Club& c) : i{ii}, cl{n,d}, rc{c} { }

};
```

引用成员或`const`成员必须被初始化（§7.5、§7.7、§17.3.3）。

然而，对于大多数类型，程序员可以选择使用初始化器还是使用赋值。在这种情况下，我通常倾向于使用成员初始化器语法，以明确正在进行初始化。通常，使用初始化器语法（与使用赋值相比）还有效率优势。例如：

```
class Person {

string name;

string address;

// ...

Person(const Person&);

Person(const string& n, const string& a);

};

Person::Person(const string& n, const string& a) : name{n}

{

address = a;

}
```

这里，`name`用`n`的副本初始化。另一方面，`address`首先被初始化为空字符串，然后被赋值为`a`的副本。

## 17.4.2 基类初始化器

派生类的基类以与非数据成员相同的方式初始化。也就是说，如果基类需要初始化器，则必须在构造函数中作为基类初始化器提供。如果我们愿意，可以显式指定默认构造。例如：

```
class B1 { B1(); }; // has default constructor

class B2 { B2(int); } // no default constructor

struct D1 : B1, B2 {

D1(int i) :B1{}, B2{i} {} };

struct D2 : B1, B2 {

D2(int i) :B2{i} {} // B1{} is used implicitly };

struct D1 : B1, B2 {

D1(int i) {} // error :B2 requires an int initializer

};
```

与成员一样，初始化顺序是声明顺序，建议按该顺序指定基类初始化器。基类在成员之前初始化，在成员之后销毁（§17.2.3）。

## 17.4.3 委托构造函数

如果你希望两个构造函数执行相同操作，可以重复代码，或者定义“一个`init()`函数”来执行公共操作。这两种“解决方案”都很常见（因为旧版 C++ 没有提供更好的方式）。例如：

```
class X {

int a;

validate(int x) { if (0<x && x<=max) a=x; else throw Bad_X(x); }

public:

X(int x) { validate(x); }

X() { validate(42); }

X(string s) { int x = to<int>(s); validate(x); } // §25.2.5.1

// ...

};
```

冗长妨碍可读性，重复容易出错。两者都不利于可维护性。另一种方法是用一个构造函数定义另一个构造函数：

```
class X {

int a;

public:

X(int x) { if (0<x && x<=max) a=x; else throw Bad_X(x); }

X() :X{42} { }

X(string s) :X{to<int>(s)} { } // §25.2.5.1

// ...

};
```

也就是说，使用类自身名称（其构造函数名）的成员风格初始化器在构造过程中调用另一个构造函数。这样的构造函数称为委托构造函数（偶尔也称为转发构造函数）。

你不能既委托又显式初始化成员。例如：

```
class X {

int a;

public:

X(int x) { if (0<x && x<=max) a=x; else throw Bad_X(x); }

X() :X{42}, a{56} { } // error

// ...

};
```

在构造函数的成员和基类初始化器列表中调用另一个构造函数进行委托，与在构造函数体内显式调用构造函数是非常不同的。考虑：

```
class X {

int a;

public:

X(int x) { if (0<x && x<=max) a=x; else throw Bad_X(x); }

X() { X{42}; } // likely error

// ...

};
```

`X{42}` 只是创建一个新的未命名对象（临时对象），并且不对其进行任何操作。这种用法往往是个 bug。希望编译器给出警告。

一个对象在其构造函数完成之前不被视为已构造（§6.4.2）。当使用委托构造函数时，只有在委托构造函数完成时对象才被视为构造完成——仅完成被委托的构造函数是不够的。除非其原始构造函数完成，否则不会为对象调用析构函数。

如果您只需要将成员设置为默认值（该默认值不依赖于构造函数参数），成员初始化器（§17.4.4）可能更简单。

## 17.4.4 类内初始化器

我们可以在类声明中为非静态数据成员指定初始化器。例如：

```
class A {

public:

int a {7};

int b = 77;

};
```

由于与解析和名称查找相关的一些晦涩的技术原因，`{}` 和 `=` 初始化器记法可用于类内成员初始化器，但 `()` 记法不可用。默认情况下，构造函数会使用此类内初始化器，因此该示例等价于：

```
class A {

public:

int a;

int b;

A() : a{7}, b{77} {}

};
```

此类内初始化器的使用可以节省一点输入，但真正的益处在于具有多个构造函数的更复杂类中。通常，多个构造函数对某个成员使用相同的初始化器。例如：

```
class A {

public:

A() : a{7}, b{5}, algorithm{"MD5"}, state{"Constructor run"} {}

A(int a_val) : a{a_val}, b{5}, algorithm{"MD5"}, state{"Constructor run"} {}

A(D d) : a{7}, b{g(d)}, algorithm{"MD5"}, state{"Constructor run"} {}

// ...

private:

int a, b;

HashFunction algorithm; //  cryptographic hash to be applied to all As

string state; //  string indicating state in object lifecycle

};
```

`algorithm` 和 `state` 在所有构造函数中具有相同的值这一事实在代码混乱中丢失了，很容易成为维护问题。为了使公共值明确，我们可以提取数据成员的唯一初始化器：

```cpp
// that is,::count2
// that is,this->m1+::count; that is,::count2+::count // veryodd constructor
```

成员初始化按声明顺序进行（§17.2.3），因此首先 `m1` 被初始化为全局变量 `count2` 的值。全局变量的值是在为新的 `S` 对象运行构造函数时获取的，因此它可能会（并且在此示例中确实）发生变化。接下来，`m2` 通过调用全局 `f()` 进行初始化。

在成员初始化器中隐藏对全局数据的微妙依赖是不好的做法。

## 17.4.5 静态成员初始化

`static` 类成员是静态分配的，而不是每个类的对象的一部分。通常，`static` 成员声明充当类外部定义的声明。例如：

```
class Node {
// ...
static int node_count;
};
// declaration
int Node::node_count = 0; // definition
```

然而，对于少数简单特殊情况，可以在类声明中初始化 `static` 成员。`static` 成员必须是 `const` 的整型或枚举类型，或是字面量类型的 `constexpr`（§10.4.3），并且初始化器必须是 *常量表达式*。例如：

```
class Curious {
public:
static const int c1 = 7; // OK
static int c2 = 11; // error : not const
const int c3 = 13; // OK, but not static (§17.4.4)
static const int c4 = sqrt(9); // error : in-class initializer not constant
static const float c5 = 7.0; // error : in-class not integral (use constexpr rather than const)
// ...
};
```

如果（且仅当）您以需要将其存储为内存中对象的方式使用已初始化的成员时，该成员必须在某处（唯一地）定义。初始化器不得重复：

```
const int Curious::c1; // 不要在此重复初始化器
const int* p = &Curious::c1; // OK: Curious::c1 已被定义
```

成员常量的主要用途是为类声明中其他地方需要的常量提供符号名称。例如：

```
template<class T, int N>
class Fixed { // fixed-size array
public:
static constexpr int max = N;

// ...
private:
T a[max];

};
```

对于整数，枚举器（§8.4）在类声明中定义符号常量提供了另一种选择。例如：

```
class X {

enum { c1 = 7, c2 = 11, c3 = 13, c4 = 17 };
```

# 17.5 拷贝与移动

当我们需要将值从 `a` 转移到 `b` 时，通常有两个在逻辑上不同的选项：

- *拷贝* 是 `x=y` 的常规含义；也就是说，其效果是 `x` 和 `y` 的值都等于赋值前 `y` 的值。
- *移动* 使 `x` 保留 `y` 的原值，而 `y` 处于某种移后状态。对于最有趣的情况，即容器而言，该移后状态为“空”。

这种简单的逻辑区别因传统以及我们对移动和拷贝使用相同记法而变得复杂。

通常，移动不会抛出异常，而拷贝可能会（因为它可能需要获取资源），并且移动通常比拷贝更高效。当您编写移动操作时，应使源对象处于有效但未指定的状态，因为它最终会被销毁，而析构函数不能销毁处于无效状态的对象。此外，标准库算法依赖于能够对移后对象进行赋值（使用移动或拷贝）。因此，设计您的移动操作使其不抛出异常，并使源对象处于允许销毁和赋值的状态。

为了免去我们繁琐的重复工作，拷贝和移动有默认定义（§17.6.2）。

## 17.5.1 拷贝

类 `X` 的拷贝由两个操作定义：

- 拷贝构造函数：`X(const X&)`
- 拷贝赋值：`X& operator=(const X&)`

您可以用更冒险的参数类型定义这两个操作，例如 `volatile X&`，但不要这样做；您只会让自己和他人困惑。拷贝构造函数应该在不修改它的情况下复制对象。同样，您可以将 `const X&` 用作拷贝赋值的返回类型。我的观点是这样做造成的困惑多于其价值，因此我对拷贝的讨论假设这两个操作具有常规类型。

考虑一个简单的二维 `Matrix`：

```
template<class T>
class Matrix {

array<int,2> dim; // twodimensions

T*elem; // pointer to dim[0]*dim[1] elements of type T

public:

Matrix(int d1, int d2) :dim{d1,d2}, elem{new T[d1*d2]} {} // simplified (no error handling)

int size() const { return dim[0]*dim[1]; }

Matrix(const Matrix&); // copyconstructor Matrix& operator=(const Matrix&); // copyassignment
```
