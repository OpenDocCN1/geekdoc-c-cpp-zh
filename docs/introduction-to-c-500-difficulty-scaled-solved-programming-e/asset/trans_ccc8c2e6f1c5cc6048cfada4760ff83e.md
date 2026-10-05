
你可能会想，这些隐式转换（例如 t = s）难道不会让代码更难理解吗？是的，我同意。我更倾向于让临时对象的创建清晰可见，而不是使用构造函数来转换类型。也就是说，我倾向于写成：

```cpp
t = T("text");而不是 t = s.
```

隐式转换是安全的吗？不，它们是不安全的；由于它们的自动性质，无意的赋值可能会导致非预期的转换并引入改变程序行为的错误。让我们来看这样一个例子：

```cpp
#include <iostream> // Example 19.2
#include <string>
using std::string;

class Student
{
private:
    string name;
    int grd[5];
public:
    Student(int g);
    Student(string s);
    int& operator[](int i);
};

Student::Student(string s)
{
    for(int i = 0; i < 5; i++)
        grd[i] = -1;
}

Student::Student(int g)
{
    for(int i = 0; i < 5; i++)
        grd[i] = g;
}

int& Student::operator[](int i)
{
    return grd[i];
}

int main()
{
    Student s("first");

    s = 2; /* 意图是改变数组中某个元素的值，
    但程序员犯了错误，没有指定元素。
    相反，这次赋值将名称更改为 none，并将 grd
    数组的值更改为 2。 */
    return 0;
}
```

程序员的意图是改变数组中某个元素的值。例如，假设你想让第一个成绩等于 2。你没有写 `grd[0] = 2`（这会调用 `operator[]` 函数来更改 `grd[0]`），而是犯了错误设置了 `s = 2;`；然而，通过这条语句，编译器使用了 `Student (int g)` 构造函数并将值 2 转换为临时对象，然后由 `s` 拷贝。因此，`s.name` 的值从 "first" 变为 "none"，`grd` 数组的所有元素都变成了 2。

如果我们进行显式转换，即写成显式的 `Student (int g)`，编译器将不允许该转换并向程序员产生错误信息。不，到目前为止还没有犯过这样的错误。但是，因为任何事情总有第一次，我倾向于将接受单个参数的构造函数声明为显式（`explicit`），以保护自己免受潜在的无意单参数构造函数错误的影响。事实上，我更希望标准默认将单参数构造函数设为显式。

![](img/25e0e40b08b8016a58f1aab13ac2e812_612_0.png)

## 从类类型转换

由于类型可以转换为对象，对象（例如 t）也可以转换为类型。例如：

```cpp
int i = t;
```

如果在类中定义了如下转换函数，这条语句是允许的：

```cpp
operator type();
```

其中 `type` 是对象将转换的目标类型名称。如果缺少此定义，编译器会发出错误信息，因为无法将 `t` 赋值给 `int`。

声明转换函数时适用规则。例如，转换函数必须是类的成员，在声明中不指定返回类型，且不接受参数。返回类型是 `type`。例如，转换为 `int` 的函数原型为：

```cpp
operator int();
```

此外，当声明转换函数时，显式转换是允许的。例如：

```cpp
int i = static_cast<int>(t);
```

通常转换函数不会改变对象的状态，因此被声明为 `const`。

```cpp
#include <iostream> // Example 19.3
class T
{
private:
  int a;
  double d;
public:
  T(int i);
  operator int() const; // 转换为 int。
  operator double() const; // 转换为 double。
};
```

```cpp
T::T(int i)
{
    a = i;
    d = 1.2;
}

T::operator int() const /* 添加返回类型并写成 T::operator int() const */
{
    return a;
}

T::operator double() const
{
    return d+2;
}

int main()
{
    int i;
    double k;
    T t = 3; // int 类型转换为类类型。
    i = t; // 调用 t.int() 转换函数。
    k = t; // 调用 t.double() 转换函数。
    std::cout << i << ' ' << static_cast<int>(t) << '\n'; /* 程序显示 5。 */
    std::cout << k << ' ' << static_cast<double>(t) << '\n'; /* 程序显示 3.2。 */
    return 0;
}
```

尽管看起来很奇怪，我们可以看到转换函数的声明中没有指定返回类型。返回类型是目标类型。通过语句 `i = t;` 调用 int 转换函数并变为 5。通过语句 `k = t;` 调用 double 转换函数并变为 3.2。同样，通过 `static_cast<>` 调用转换函数。注意，如果不使用隐式转换而写 `t`，编译器将显示错误信息，因为它不知道使用 int 还是 double 转换。

再次有人可能会问，这些隐式转换难道不会让代码更难理解且不安全吗？是的，我同意。我倾向于让临时对象的创建清晰可见，而不是使用构造函数来转换类型。也就是说，我倾向于写成：

```
t = T("text");而不是 t = s.
```

转换函数的一种流行用法是在条件检查流的状态：

```cpp
while(cin >> i) {...}
```

正如我们所知，通过 istream 运算符读取的值存储在 i 中并返回引用。因此，为了评估条件，会调用转换函数，如果状态有效则返回 true，否则发生错误时返回 false。作为构造函数，如果我们不想允许隐式转换，可以使用 `explicit` 关键字。如果转换函数被设为显式，我们必须使用类型转换来使用它：

```cpp
class A
{
    explicit operator int() const {return10;}
}
int i;
i = a; // 错误
i = static_cast<int>(a); //正确
```

在进入下一节之前，我想说我不喜欢隐式类转换，因为我喜欢事情清晰、简单且安全。这才是重要的。

## 类成员指针

在第8章中，我们讨论了函数指针。例如，通过 `void (*ptr)(int, int);`，`ptr` 被声明为函数指针，它接受整数参数且不返回。现在让我们看看如何声明类成员函数指针。例如：

```cpp
#include <iostream> // Example 19.4
class T
{
public:
    void f(int a, int b) {std::cout << a-b << '\n';}
}
void (T::*fptr)(int a, b);

int main()
{
    T t;
    T::*fptr; // 指针声明。
    fptr = &T::f; /* 这是指针指向成员函数的语法 */
    (t.*fptr)(8, 5); // 通过 * 运算符调用函数。
    T::*r = &T::f;
    (r->fptr)(8, 5); // 通过 -> 运算符调用函数。
    return 0;
}
```

为了更容易编写指针声明和相应变量的类型，使用 `typedef` 语句为指针类型创建别名会更方便。虽然这种声明的语法看起来很复杂，但只要我们遵循第8章和本章中提到的方法，它并不复杂。正如我们所说，声明函数指针的一种简单方法是先写函数的原型，然后将函数名替换为 `(*ptr)` 形式的表达式。例如，我们使用 `typedef` 关键字创建别名。别地，我们可以使用 `using` 关键字来创建别名：

```cpp
using fptr = void (T::*) (a, b);
```

如果不使用别名，我们可以如下声明 `p` 指针：

```cpp
int main()\{
    void (T::*p)(a, b);
    ...
}
```
