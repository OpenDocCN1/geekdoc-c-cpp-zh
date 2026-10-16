

+   - 容器的初始化列表构造函数可以是 **explicit** 的，也可以不是。
+   - 初始化列表元素类型的构造函数可以是 **explicit** 的，也可以不是。对于 **vector<vector<double>>**，我们可以看到直接初始化与拷贝初始化在元素上的区别。例如：

```
vector<vector<double>> vs = {
{10,11,12,13,14}, // OK: vector of five elements
{10}, // OK: vector of one element
10, // error : vector<double>(int) is explicit
vector<double>{10,11,12,13}, // OK: vector of five elements
vector<double>{10}, // OK: vector of one element with value 10.0
vector<double>(10), // OK: vector of 10 elements with value 0.0
};
```

一个容器可以有一些构造函数是 explicit 的，而另一些不是。标准库中的 **vector** 就是一个例子。例如，**std::vector<int>(int)** 是 **explicit** 的，但 **std::vector<int>(initializer_list<int>)** 不是：

```
vector<double> v1(7); vector<double> v2 = 9;
// OK: v1 has 7 elements; note: uses () rather than {} // error : no conversion from int to vector
void f(const vector<double>&); void g()
{
v1 = 9; // error : no conversion from int to vector f(9); // error : no conversion from int to vector }
```

将 **()** 替换为 **{}** 后，我们得到：

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

## 17.4 成员与基类初始化

构造函数可以建立不变量并获取资源。通常，它们通过初始化类的成员和基类来实现这一点。

### 17.4.1 成员初始化

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

Club 的构造函数将俱乐部名称和成立日期作为参数。成员的构造函数的参数在包含类的构造函数定义中的成员初始化列表中指定。例如：

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

这个构造函数与前一个版本等价。在每种情况下，Club::officers 和 Club::members 都被初始化为没有元素的 vector。

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

引用成员或 const 成员必须被初始化（§7.5、§7.7、§17.3.3）。

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

这里，name 用 n 的副本初始化。另一方面，address 首先被初始化为空字符串，然后被赋值为 a 的副本。

### 17.4.2 基类初始化器

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

### 17.4.3 委托构造函数

如果你希望两个构造函数执行相同操作，可以重复代码，或者定义“一个 init() 函数”来执行公共操作。这两种“解决方案”都很常见（因为旧版 C++ 没有提供更好的方式）。例如：

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

X{42} 只是创建一个新的未命名对象（临时对象），并且不对其进行任何操作。这种用法往往是个 bug。希望编译器给出警告。

一个对象在其构造函数完成之前不被视为已构造（§6.4.2）。当

