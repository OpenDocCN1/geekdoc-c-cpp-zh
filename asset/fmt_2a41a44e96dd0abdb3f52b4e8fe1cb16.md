

这里，我假设传递第一个元素的地址是创建指向 `My_container` 第一个元素的迭代器的一种方式，并且 `My_container` 有 `size()`。

# 33.4 函数对象

许多标准算法将函数对象（或函数）作为参数来控制它们的工作方式。常见用途包括比较准则、谓词（返回 `bool` 的函数）和算术运算。在 `<functional>` 中，标准库提供了一些常见的函数对象：

# 谓词（§iso.20.8.5、§iso.20.8.6、§iso.20.8.7）

`p=equal_to<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x==y`
`p=not_equal_to<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x!=y`
`p=greater<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x>y`
`p=less<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x<y`
`p=greater_equal<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x>=y`
`p=less_equal<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x<=y`
`p=logical_and<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x&&y`
`p=logical_or<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x||y`
`p=logical_not<T>(x)` 当 `x` 为类型 `T` 时，`p(x)` 表示 `!x`
`p=bit_and<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x&y`
`p=bit_or<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x|y`
`p=bit_xor<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`p(x,y)` 表示 `x^y`

例如：

```cpp
vector<int> v;

// ...

sort(v.begin(),v.end(),greater<int>{}); // sort vinto decreasing order
```

这类谓词大致等价于简单的 lambda。例如：

```cpp
vector<int> v;

// ...

sort(v.begin(),v.end(),[](int a, int b) { return a>b; }); // sort vinto decreasing order
```

注意，`logical_and` 和 `logical_or` 总是对两个参数求值（`&&` 和 `||` 则不会）。

# 算术操作（siso.20.8.4）

`f=plus<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`f(x,y)` 表示 `x+y`
`f=minus<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`f(x,y)` 表示 `x−y`
`f=multiples<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`f(x,y)` 表示 `x*y`
`f=divides<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`f(x,y)` 表示 `x/y`
`f=modulus<T>(x,y)` 当 `x` 和 `y` 为类型 `T` 时，`f(x,y)` 表示 `x%y`
`f=negate<T>(x)` 当 `x` 为类型 `T` 时，`f(x)` 表示 `−x`

# 33.5 函数适配器

函数适配器接受一个函数作为参数，并返回一个可用于调用原函数的函数对象。

# 适配器（siso.20.8.9、Siso.20.8.10、Siso.20.8.8）

`g=bind(f,args)` `g(args2)` 等价于 `f(args3)`，其中 `args3` 是通过将 `args` 中的占位符替换为 `args2` 中的参数而得到的；可以使用诸如 `_1`、`_2` 和 `_3` 这样的占位符。

`g=mem_fn(f)` `g(p,args)` 表示：如果 `p` 是指针，则 `p->f(args)`；如果 `p` 不是指针，则 `p.mf(args)`；`args` 是（可能为空的）参数列表。

`g=not1(f)` `g(x)` 表示 `!f(x)`

`g=not2(f)` `g(x,y)` 表示 `!f(x,y)`

`bind()` 和 `mem_fn()` 适配器执行参数绑定，也称为 *柯里化* 或 *部分求值*。这些绑定器及其已废弃的前辈（如 `bind1st()`、`mem_fun()` 和 `mem_fun_ref()`）在过去被大量使用，但大多数用法似乎用 lambda（§11.4）表达更为容易。

## 33.5.1 bind()

给定一个函数和一组参数，`bind()` 会生成一个函数对象，该对象可以用函数的“剩余”参数（如果有的话）来调用。例如：

```cpp
double cube(double);

auto cube2 = bind(cube,2);
```

调用 `cube2()` 将使用参数 `2` 调用 `cube`，即 `cube(2)`。我们不必绑定函数的所有参数。例如：

```cpp
using namespace placeholders;

void f(int,const string&);

auto g = bind(f,2,_1); // bind f()’s first argument to 2

f(2,“hello”);

g(“hello”); // also calls f(2,“hello”);
```

绑定器中奇特的 `_1` 参数是一个占位符，它告诉 `bind()` 结果函数对象的参数应该放在哪里。在本例中，`g()` 的（第一个）参数被用作 `f()` 的第二个参数。这些占位符位于（子）命名空间 `std::placeholders` 中，该命名空间是 `<functional>` 的一部分。占位符机制非常灵活。考虑：

```cpp
f(2,"hello");

bind(f)(2,"hello"); // also calls f(2,"hello");

bind(f,_,_)(2,"hello"); // also calls f(2,"hello");

bind(f,_,_)("hello",2); // reverse order of arguments: also calls f(2,"hello");

auto g = [](const string& s, int i) { f(i,s); } // reverse order of arguments g("hello",2); // also calls f(2,"hello");
```

为了给重载函数绑定参数，我们必须明确指定要绑定的是函数的哪个版本：

```cpp
int pow(int,int);

double pow(double,double); // pow() is overloaded

auto pow2 = bind(pow,_,1,2); // error : which pow()?

auto pow2 = bind((double(*)(double,double))pow,_,1,2); // OK (but ugly)
```

注意，`bind()` 接受普通表达式作为参数。这意味着引用在 `bind()` 看到它们之前就会被解引用。例如：

```cpp
void incr(int& i)

{

++i; }

void user() {

int i = 1;

incr(i); // i becomes 2

auto inc = bind(incr,_,1);

inc(i); // i stays 2; inc(i) incremented a local copy of i

}
```

为了解决这个问题，标准库提供了另一对适配器：

`reference_wrapper<T>` (§iso.20.8.3) `r=ref(t)` `r` 是 `T& t` 的 `reference_wrapper`；`noexcept` `r=cref(t)` `r` 是 `const T& t` 的 `reference_wrapper`；`noexcept` 这解决了 `bind()` 的“引用问题”：

```cpp
void user()

{

int i = 1;

incr(i); // i becomes 2

auto inc = bind(incr,_,1);

inc(ref(i)); // i becomes 3

}
```

这个 `ref()` 是必要的，以便将引用作为参数传递给线程，因为线程构造函数是可变参数模板（§42.2.2）。

到目前为止，我要么立即使用 `bind()` 的结果，要么将其赋值给用 `auto` 声明的变量。这省去了指定 `bind()` 调用返回类型的麻烦。这可能很有用，因为 `bind()` 的返回类型随要调用的函数类型和存储的参数值而变化。特别是，当返回的函数对象必须保存绑定参数的值时，它会更大。然而，有时我们希望对所需参数的类型和返回的结果类型进行具体指定。如果是这样，我们可以为函数指定它们（§33.5.3）。

## 33.5.2 mem_fn()

函数适配器 `mem_fn(mf)` 产生一个可以作为非成员函数调用的函数对象。例如：

```cpp
void user(Shape * p)

{

p->draw();

auto draw = mem_fn(&Shape::draw);

draw(p);

}
```

`mem_fn()` 的主要用途是当算法要求以非成员函数方式调用某个操作时。例如：

```cpp
void draw_all(vector<Shape*>& v)

{

for_each(v.begin(),v.end(),mem_fn(&Shape::draw));

}
```

因此，`mem_fn()` 可以看作是从面向对象调用风格到函数式调用风格的一种映射。

通常，lambda 为绑定器提供了一种简单而通用的替代方案。例如：

```cpp
void draw_all(vector<Shape*>& v)

{

for_each(v.begin(),v.end(),[](Shape* p) { p->draw(); });

}
```

## 33.5.3 function

`bind()` 可以直接使用，也可以用来初始化 `自动变量`。在这方面，`bind()` 类似于 lambda。

如果我们想把 `bind()` 的结果赋给一个具有特定类型的变量，可以使用标准库类型 `function`。`function` 通过特定的返回类型和特定的参数类型来指定。

```cpp
function f {};

function f {nullptr}; function f {g};

```

```cpp
function f {allocator_arg_t,a}; function f {allocator_arg_t,a,nullptr_t}; function f {allocator_arg_t,a,g}; function<R(Argtypes...)> (§iso.20.8.11.2) (continues)
```

`f` is an empty `function`; noexcept

`f` is an empty `function`; noexcept

`f` is a `function` holding `g`; `g` can be anything that can be invoked with `f`’s argument types `f`

is an empty function; use allocator a; noexcept f is an empty function; use allocator a; noexcept f is a function holding g; use allocator a; noexcept

`f2=f` `f2` is a copy of `f` `f=nullptr` `f` becomes empty

## function<R(Argtypes...)> (续)(§iso.20.8.11.2)

`f.swap(f2)` 交换 `f` 和 `f2` 的内容；
`f` 和 `f2` 必须是相同的函数类型；noexcept
`f.assign(f2,a)` `f` 获得 `f2` 的副本和分配器 `a`
`bool b {f};` 将 `f` 转换为 `bool`；
如果 `f` 非空则 `b` 为 `true`；explicit；noexcept
`r=f(args)` 用 `args` 调用包含的函数；参数类型必须与 `f` 的匹配
`ti=f.target_type()` `ti` 是 `f` 的 `type_info`；如果 `f` 不包含可调用对象，则
`ti==typeid(void)`；noexcept
`p=f.target<F>()` 如果 `f.target_type()==typeid(F)`，则 `p` 指向包含的对象，否则 `p==nullptr`；noexcept
`f==nullptr` `f` 是否为空？noexcept
`nullptr==f` 等价于 `f==nullptr`
`f!=nullptr` 等价于 `!(f==nullptr)`
`nullptr!=f` 等价于 `!(f==nullptr)`
`swap(f,f2)` 等价于 `f.swap(f2)`

例如：

```cpp
int f(double);

function<int(double)> fct {f}; // initialize to f int g(int);

```

```cpp
void user() {

fct = [](double d) { return round(d); }; fct = f;

fct = g;

}
```

// 将 lambda 赋给 `fct`
// 将函数赋给 `fct` // 错误：返回类型不正确

目标函数（target functions）是为某些罕见情况提供的，即有人想要检查一个函数，而不是像通常预期的那样简单地调用它。

标准库的 `function` 是一种类型，可以持有任何你能使用调用运算符 `()` 调用的对象（§2.2.1, §3.4.3, §11.4, §19.2.2）。也就是说，`function` 类型的对象是一个函数对象。例如：

```cpp
int round(double x) { return static_cast<double>(floor(x+0.5)); } // conventional 4/5 rounding

function<int(double)> f; // f can hold anything that can be called with a double and return an int

enum class Round_style { truncate, round };

```

```cpp
struct Round { // function object carrying a state

Round_style s;

Round(Round_style ss) :s(ss) { }

int operator()(double x) const { return (s==Round_style::round) ? (x+0.5) : x; };

```

### 第 33.5.3 节 function 971

```cpp
void t1() {

f = round;

cout << f(7.6) << '\n'; // call through f to the function round

f = Round(Round_style::truncate);

cout << f(7.6) << '\n'; // call the function object

Round_style style = Round_style::round;

f = [style] (double x){ return (style==Round_style::round) ? x+0.5 : x; };

cout << f(7.6) << '\n'; // call the lambda

vector<double> v {7.6};

f = Round(Round_style::round);

std::transform(v.begin(),v.end(),v.begin(),f); // pass to algorithm

cout << v[0] << '\n'; // transformed by the lambda }
```

