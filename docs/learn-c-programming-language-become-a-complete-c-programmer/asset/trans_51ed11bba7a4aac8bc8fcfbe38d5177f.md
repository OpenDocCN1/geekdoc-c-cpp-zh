

标准库提供了 int 到 string 的转换函数 to_string()（§36.3.5）。如果我不必模仿 C 风格，我会通过将容器作为单个参数传递来进一步简化代码：

```
void error(int severity, const vector<string>& err) // almost as before
{
for (auto& s : err)
cerr << s << ' '; cerr << '\n';
if (severity) exit(severity); }

vector<string> arguments(int argc, char * argv[]) // package arguments {
vector<string> res;
for (int i = 0; i!=argc; ++i) res.push_back(argv[i]); return res
}

int main(int argc, char * argv[]) {
auto args = arguments(argc,argv);
error((args.size()<2)?0:1,args);
// ...
}
```

辅助函数 arguments() 很简单，main() 和 error() 也很简单。main() 与 error() 之间的接口更通用，因为它现在传递了所有参数。这将允许以后改进 error()。使用 vector<string> 比使用任意数量的参数要少出错得多。

## 12.2.5 默认参数

一个通用函数通常需要比处理简单情况更多的参数。特别是，构造对象的函数（§16.2.5）通常提供多种选项以实现灵活性。考虑 §3.2.1.1 中的类 complex：

```
class complex {
double re, im;
public:
complex(double r, double i) :re{r}, im{i} {} complex(double r) :re{r}, im{0} {}
complex() :re{0}, im{0} {}
// default complex: {0,0}
// ...
};
// construct complex from two scalars // construct complex from one scalar
```

complex 的构造函数的行为相当简单，但从逻辑上讲，有三个函数（这里是构造函数）做本质上相同的任务是有些奇怪的。此外，对于许多类，构造函数做更多的工作，重复性很常见。我们可以通过将其中一个构造函数视为“真正的”并转发给它来处理重复性（§17.4.3）：

```
complex(double r, double i) :re{r}, im{i} {} complex(double r) :complex{r,0} {}
complex() :complex{0,0} {}
```

```
// construct complex from two scalars  // construct complex from one scalar  // default
complex: {0,0}
```

假设我们想为 **complex** 添加一些调试、跟踪或统计收集代码；我们现在有一个单一的位置可以这样做。然而，这可以进一步缩写：

```
complex(double r ={}, double i ={}) :re{r}, im{i} {} // construct complex from two scalars
```

这使得如果用户提供的参数少于所需的两个参数，则使用默认值变得清晰。拥有单个构造函数加上一些简写表示的意图现在是明确的。

默认参数在函数声明时进行类型检查，并在调用时求值。例如：

```
class X {
public:
static int def_arg;
void f(int =def_arg);
// ...
};

int X::def_arg = 7;

void g(X& a) {
a.f(); // maybe f(7)
a.def_arg = 9;
a.f(); // f(9)
}
```

可以改变值的默认参数最好通常避免，因为它们引入了微妙的上下文依赖。

只能为尾部参数提供默认参数。例如：

```
int f(int, int =0, char * =nullptr); // OK
int g(int =0, int =0, char*); // error
int h(int =0, int, char*=nullptr); // error
```

请注意 * 与 = 之间的空格是重要的（*= 是赋值运算符；§10.3）：**int nasty(char*=nullptr); // syntax error**

在同一作用域中，后续声明不能重复或更改默认参数。例如：

```
void f(int x = 7); void f(int = 7); void f(int = 8);

// error : cannot repeat default argument // error : different default arguments

void g() {
```

```
```cpp
void f(int x = 0); // OK: this declaration hides the outer one
// ...
}
```
```

在嵌套作用域中声明一个名称以隐藏外部作用域中相同名称的声明是容易出错的。

## 12.3 重载函数

通常，给不同的函数不同的名称是个好主意，但当不同的函数在概念上对不同类型的对象执行相同的任务时，给它们相同的名称会更方便。对不同类型使用相同名称的操作称为 *重载*。该技术已用于 C++ 中的基本操作。即，加法只有一个名称 `+`，但它可用于添加整数和浮点类型的值以及这些类型的组合。这个想法很容易扩展到程序员定义的函数。例如：

```
```cpp
void print(int);        // print an int
void print(const char*); // print a C-style string
```
```

就编译器而言，相同名称的函数唯一共同点就是该名称。 presumably，函数在某种意义上是相似的，但语言并不限制或帮助程序员。因此，重载函数名主要是一种记号上的便利。这种便利对于具有惯用名称的函数如 *sqrt*、*print* 和 *open* 来说是重要的。当名称在语义上很重要时，这种便利变得至关重要。例如，这发生在 `+`、` *` 和 `<<` 等运算符的情况下，构造函数的情形（§16.2.5，§17.1），以及泛型编程中（§4.5，第 32 章）。

模板提供了一种系统地定义重载函数集的方法（§23.5）。

### 12.3.1 自动重载解析

当函数 `fct` 被调用时，编译器必须确定要调用的名为 `fct` 的函数中的哪一个。这是通过将实际参数的类型与作用域内所有名为 `fct` 的函数的参数类型进行比较来完成的。想法是调用与参数最匹配的函数，如果没有函数是最匹配的则给出编译时错误。例如：

```
```cpp
void print(double);
void print(long);

void f() {
    print(1L); // print(long)
    print(1.0); // print(double)
    print(1); // error, ambiguous: print(long(1)) or print(double(1))?
}
```
```

为了近似我们认为合理的内容，按顺序尝试一系列标准：

```
print_int(i); // OK print_char(c); // OK print_string(p); // OK
print_int(c); // OK? calls print_int(int(c)), prints a number
print_char(i); // OK? calls print_char(char(i)), narrowing
print_string(i); // error
print_int(d); // OK? calls print_int(int(d)), narrowing
}
```

与重载的 print() 相比，我们必须记住几个名称并正确使用它们。这可能很乏味，妨碍了泛型编程（§4.5）的尝试，并且通常鼓励程序员关注相对低级的类型问题。由于没有重载，所有标准转换都适用于这些函数的参数。这也可能导致错误。在前面的示例中，这意味着只有四个语义可疑的调用中的一个被编译器捕获。特别是，两个调用依赖于容易出错的窄化（§2.2.2，§10.5）。因此，重载可以增加不合适的参数被编译器拒绝的机会。

### 12.3.2 重载与返回类型

返回类型不参与重载解析。原因是为了保持单个运算符（§18.2.1，§18.2.5）或函数调用上下文的解析与上下文无关。考虑：

```
float sqrt(float);
double sqrt(double);

void f(double da, float fla) {
float fl = sqrt(da); // call sqrt(double)
double d = sqrt(da); // call sqrt(double)
fl=sqrt(fla); // call sqrt(float)
d = sqrt(fla); // call sqrt(float)
}
```

如果考虑返回类型，就不再可能单独查看 sqrt() 的调用并确定调用了哪个函数。

### 12.3.3 重载与作用域

重载发生在重载集的成员之间。默认情况下，这意味着单个作用域的函数；声明在不同非命名空间作用域中的函数不重载。例如：

第 12.3.3 节 重载与作用域 329

```
void f(int);

void g() {
void f(double);
f(1); // call f(double)
}
```

显然，f(int) 会是 f(1) 的最佳匹配，但只有 f(double) 在作用域内。在

