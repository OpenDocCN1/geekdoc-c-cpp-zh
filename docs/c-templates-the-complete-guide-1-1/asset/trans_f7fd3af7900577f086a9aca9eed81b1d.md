
```cpp
// constructor for C, 2, 3, or 4 arguments:
C(int x1, int y1, int x2 = T1);

C c1(22, 44, 3);  // OK for C++17: T1 is int, T2 is
                  // double, T3 is char*
C c2(22, 44, 3);  // OK for C++17: T1 is int, T2 and
                  // T3 are double
C c3("hi", "you");
```

注意，所有参数都必须通过推导过程或默认实参来确定。不能显式指定一部分实参而推导其余实参。例如：

**单击此处查看代码图像**

```cpp
template<typename T>
class S {
private:
  T a;
public:
  S(T b = a) { }
};
```

### 15.12.1 推导指引

首先考虑我们对第288页15.8.2节中较早例子的一个小改动：

**单击此处查看代码图像**

```cpp
template<typename T>
class S {
private:
  T a;
public:
  S(T b = a) { }
};

template<typename T> S(T) -> S<T>; // deduction guide

S x(12);       // S<int>
S y(12);       // S<int>
S z(12);       // or, since C++17, same as S<int>
S w = S(12);   // or, since C++17, same as S<int>
S<int> z{12};
```

特别要注意，这里添加了一种新的类似模板的结构，称为*推导指引*（deduction guide）。它看起来有点像函数模板，但在语法上与函数模板有几个不同之处：

-   看起来像尾置返回类型的部分不能写成传统的返回类型。我们将其指定的类型（本例中的`S<T>`）称为被引导类型（guided type）。
-   没有前导的`auto`关键字来指示后面跟着尾置返回类型。
-   推导指引的“名字”必须是在同一作用域中先前声明的类模板的非限定名称。
-   指引的被引导类型必须是一个模板标识（template-id），且其模板名与指引的名字对应。
-   它可以用`explicit`说明符声明。

在声明`S x(12);`中，限定符`S`被称为*占位类类型*（placeholder class type）。当使用这样的占位符时，正在声明的变量名必须紧随其后，并且其后必须跟有初始化器。因此以下是无效的：

**单击此处查看代码图像**

```cpp
S* p = ...; // ERROR: syntax not permitted
```

使用示例中编写的指引，声明`S x(12);`通过将与类`S`关联的推导指引视为一个重载集合，并尝试使用初始化器实参进行重载解析，来推导变量的类型。此时，注意集合中只有一个指引，它成功将`T`推导为`int`，并将指引的被引导类型推导为`S<int>`。因此该被引导类型被选为变量`x`的类型。

注意，如果在类模板名后跟有多个需要进行推导的声明，那么每个声明的初始化器都必须产生相同的类型。例如，对于上面的声明：

**单击此处查看代码图像**

```cpp
template<typename T> A(T) -> A<T>; // deduction guide
```

没有该推导指引时，我们总是（即使在C++17中）需要指定显式的模板实参：

单击此处查看代码图像

```cpp
A<int> a1(42);      // OK
A<int> a2(42);      // ERROR: not aggregate initialization
A<int> a3 = {42};   // OK
A<int> a4 = 42;     // ERROR: can't deduce type
```

但如果使用上面编写的指引，我们可以写

```cpp
A a = {42}; // OK
```

不过，这类情况中的一个微妙之处在于，初始化器仍然必须是一个有效的聚合初始化器；也就是说，它必须使用花括号初始化器列表。因此下面的替代写法是不允许的：

单击此处查看代码图像

```cpp
A a(42);  // ERROR: not aggregate initialization
A a = 42;  // ERROR: not aggregate initialization
```

### 15.12.2 隐式推导指引

很多时候，类模板中的每个构造函数都需要有一个推导指引。类模板参数推导的设计者决定引入一种隐式推导机制。这相当于为主类模板的每个构造函数和构造函数模板引入一个“隐式推导指引”，如下所示：

-   隐式指引的模板参数列表由类模板的模板参数和构造函数模板参数组成，按构造函数自身的模板参数列表中的顺序排列。
-   指引的“函数式”参数从构造函数或构造函数模板复制而来。
-   指引的被引导类型是模板的名字，其实参是取自类模板的模板参数。

让我们将其应用于最初的简单类模板：

单击此处查看代码图像

```cpp
template<typename T>
class A {
private:
    T t;
public:
    A(T t): t(t) {}
};
```

隐式指引的模板参数列表是`<typename T>`，函数式参数列表变为`(T t)`，被引导类型则是`A<T>`。这样，我们就得到了一个等价于之前我们用户声明的指引。因此，要实现我们期望的效果，并不需要这个指引。这就是为什么，对于最初编写的简单类模板（且没有推导指引），我们可以合法地写`A{42};`并期望`t`具有类型`int`。

推导指引有一个令人遗憾的歧义。再次考虑我们简单的类模板`S`以及以下初始化：

```cpp
S x(12);       // ? for x type
S s = {12};    //
S y{12};       //
```

我们已经看到`s`的类型是`S<int>`，但`x`和`y`的类型应该是什么呢？直觉上合理的两种类型是`S<int>`和`S<int>`。委员会做出了一个有争议的决定：在这两种情况下都应该是`S<int>`。为什么这有争议？考虑一个使用`vector`类型的类似例子：

单击此处查看代码图像

```cpp
std::vector<int> v1(2, 3);  // vector<int>, not surprising
std::vector<int> v2{2, 3};  // vector<int>
std::vector v3(2, 3);       // vector<int>?
```

换句话说，带一个元素的花括号初始化器与带多个元素的花括号初始化推导出的结果不同。通常情况下，单元素场景是想要的，但这种不一致性有点微妙。然而，在泛型代码中，很容易忽略这种微妙之处：

单击此处查看代码图像

```cpp
template<typename T, typename... Ts>
struct S {
    S(T t, Ts... ts);  // ... depends on pack length
};
```

这里有一个有趣的事实：如果`T`被推导为`vector`类型，那么`v`的类型将从根本上取决于参数包是空包还是非空包。

隐式模板指引的加入本身也并非没有争议。反对它们的加入的主要论点是，该特性会自动给现有库添加接口。为了理解这一点，请再次考虑上面模板实参相近的例子。（其余部分）。上面的例子因此将`T`声明为`std::string`，正如预期的那样。

### explicit关键字

推导指引可以用关键字`explicit`声明。这样它仅在直接初始化情况下被考虑，而在复制初始化情况下不会被考虑。例如：

单击此处查看代码图像

```cpp
template<typename T> struct X {
  X(T const&);
};

template<typename T> explicit X(T) -> X<T>;  // #1
```

```cpp
X x1 = 1;   // only considers #2? No, #1 is explicit; leads x1
X x2{1};    // prefers #1
```

注意`x1`的初始化是复制初始化，因此推导指引`#1`因被声明为explicit而不被考虑。

### 复制构造与初始化器列表

考虑下面的类模板：

单击此处查看代码图像

```cpp
template<typename T> struct Tuple {
  Tuple(T...);
  Tuple(T const&);
};
```

为了理解隐式指引的效果，让我们把它们写成显式声明：

单击此处查看代码图像

```cpp
template<typename T> Tuple(T) -> Tuple<T>;
template<typename T> Tuple(Tuple<T> const&) -> Tuple<T>;
```

现在考虑同样的例子：

```cpp
auto x = Tuple(1, 2);
```

这清楚地选择了第一个指引，因此选择了第一个构造函数：`x`因此是`Tuple<int, int>`。我们继续看一些使用类似复制初始化语法的例子：

```cpp
Tuple a = x;
Tuple b(x);
```

对于`a`和`b`，两个指引都匹配。第一个指引选择的类型是`Tuple<T...>`，但与复制构造函数关联的指引产生`Tuple<int, int>`。幸运的是，第二个指引是更好的匹配，因此`a`和`b`都是从`x`复制构造的。

现在，考虑一些使用花括号初始化器列表的例子：

```cpp
Tuple c{x, x};
Tuple d{x};
```

这些例子中的第一个（`c`）只能匹配第一个指引，因此产生`Tuple<Tuple<int, int>, Tuple<int, int>>`。这完全符合直觉，并不令人惊讶。然而，第二个例子（`d`）被视作`x`的副本，因为`Tuple<T> const&`是更优的选择。函数式记法转换也会出现同样的情况：

```cpp
auto z = Tuple(x);
```

在这里，`x`被声明为`Tuple<int, int>`，而不是`Tuple<Tuple<int, int>>`。

### 指引仅用于推导

推导指引不是函数模板：它们仅用于确定模板参数，而不会被调用。这意味着按引用还是按值传递实参的差异对指引声明并不重要。例如：

单击此处查看代码图像

```cpp
template<typename T> struct X {
  X(T const&);
};

template<typename T> X(T) -> X<T>;
```

注意，推导指引与`X`的构造函数并不完全对应。然而，这并不重要，因为指引仅用于推导。给定一个类型为`X<T>`的值`x`，它的值或引用将选择推导出的类型`X<T>`。然后，初始化将针对`X<T>`的构造函数执行重载解析，以决定调用哪一个（这将取决于`x`是左值还是右值）。

### 15.13 后记

