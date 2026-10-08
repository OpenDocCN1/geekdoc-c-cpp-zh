

因此，这次对 `expression()` 的调用拥有自己的**激活记录**，与第一次调用 `expression()` 不同。这是好事，否则局面将非常混乱，因为在这两次调用中，`left` 和 `t` 的值是不同的。一个直接或间接（如此处）调用自身的函数被称为*递归*函数。正如你所见，递归函数是自然地从我们用于函数调用和返回的实现技术中衍生出来的（反之亦然）。

因此，每次调用一个函数时，*激活记录栈*（通常简称为*栈*）都会增加一条记录。相反地，当函数返回时，其记录将不再被使用。例如，当最后一次调用 `expression()` 返回到 `primary()` 时，栈将恢复为如下状态：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_321_0.png)

当该次调用 `primary()` 返回到 `term()` 时，我们回到

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_321_1.png)

以此类推。栈，也称为*调用栈*，是一种数据结构，它在根据“后进先出”规则在某一端增长和收缩。

请记住，调用栈如何实现和使用，细节因 C++ 实现而异，但基本原理如前所述。你需要了解函数调用是如何实现的才能使用它们吗？当然不需要；在这个实现小节之前，你已经做得足够好了。但许多程序员希望了解这些细节，并且许多人会使用“激活记录”和“调用栈”这样的短语，所以了解它们的含义会更好。

### 8.5.9 constexpr 函数

函数代表一种计算，有时我们希望在编译时执行计算。希望编译器评估计算的原因通常是避免在运行时对同一计算进行数百万次重复。我们使用函数使我们的计算更易懂，因此自然有时希望在常量表达式中使用函数。我们通过声明函数为 `constexpr` 来表达我们意图让编译器在编译时评估该函数。如果给定常量表达式作为参数，`constexpr` 函数可以由编译器评估。例如：

```cpp
constexpr double xscale = 10;   // scaling factors
constexpr double yscale = 0.8;

constexpr Point scale(Point p) { return {xscale*p.x, yscale*p.y}; };
```

假设 `Point` 是一个简单的结构体，成员 `x` 和 `y` 代表 2D 坐标。现在，当我们给 `scale()` 一个 `Point` 参数时，它返回一个 `Point`，其坐标根据因子 `xscale` 和 `yscale` 进行缩放。例如：

```cpp
void user(Point p1)
{
    constexpr Point p2 {10,10};

    Point p3 = scale(p1);    // OK: p3 == {100,8}; run-time evaluation is fine
    constexpr Point p4 = scale(p2);  // p4 == {100,8}

    constexpr Point p5 = scale(p1);  // error: scale(p1) is not a constant
                                     // expression
    constexpr Point p6 = scale(p2);  // p6 == {100,8}

    // ...
}
```

一个 `constexpr` 函数的行为与普通函数完全相同，直到你在需要常量的地方使用它。然后，前提是它的参数是常量表达式（例如 `p2`），它将在编译时计算；如果参数不是常量表达式（例如 `p1`），则会产生错误。为了实现这一点，`constexpr` 函数必须足够简单，以便编译器（每个符合标准的编译器）都能评估它。在 C++11 中，这意味着 `constexpr` 函数必须有一个由单个 `return` 语句组成的函数体（如 `scale()`）；在 C++14 中，我们还可以编写简单的循环。`constexpr` 函数不能有副作用；也就是说，除了它被赋值或用于初始化的变量外，它不能改变其自身函数体之外变量的值。

这里是一个违反简洁性规则的函数示例：

```cpp
int glob = 9;

constexpr void bad(int & arg)    // error: no return value
{
    ++arg;                        // error: modifies caller through argument
    glob = 7;                     // error: modifies nonlocal variable
}
```

如果编译器无法确定一个 `constexpr` 函数“足够简单”（根据标准中的详细规则），该函数将被视为错误。

### 8.6 求值顺序

程序的求值——也称为程序的执行——根据语言规则通过语句进行。当这个“执行线程”到达变量的定义时，变量被构造；也就是说，为对象预留内存并初始化对象。当变量离开作用域时，变量被销毁；也就是说，它引用的对象原则上被移除，编译器可以将其内存用于其他用途。例如：

```cpp
string program_name = "silly";
vector<string> v;                    // v is global

void f()
{
    string s;                            // s is local to f
    while (cin>>s && s!="quit") {
        string stripped;                 // stripped is local to the loop
        string not_letters;
        for (int i=0; i<s.size(); ++i)    // i has statement scope
            if (isalpha(s[i]))
                stripped += s[i];
            else
                not_letters += s[i];
        v.push_back(stripped);
        // ...
    }
    // ...
}
```

全局变量，如 `program_name` 和 `v`，在 `main()` 的第一条语句执行之前初始化。它们“存活”直到程序终止，然后被销毁。它们按照定义顺序构造（即 `program_name` 在 `v` 之前），并按照相反顺序销毁（即 `v` 在 `program_name` 之前）。

当有人调用 `f()` 时，首先构造 `s`；也就是说，`s` 被初始化为空字符串。它将存活直到我们从 `f()` 返回。

每次进入作为 `while` 语句主体的块时，`stripped` 和 `not_letters` 被构造。由于 `stripped` 定义在 `not_letters` 之前，`stripped` 在 `not_letters` 之前构造。它们存活到循环结束，在重新评估条件之前，按照与构造相反的顺序销毁（即 `not_letters` 在 `stripped` 之前）。因此，如果在我们遇到字符串 `quit` 之前看到十个字符串，`stripped` 和 `not_letters` 将各自被构造和销毁十次。

每次到达 `for` 语句时，`i` 被构造。每次退出 `for` 语句时，在到达 `v.push_back(stripped);` 语句之前，`i` 被销毁。

请注意，编译器（和链接器）是聪明的野兽，它们被允许——并且确实——只要结果与我们在此描述的结果等价，就对代码进行优化。特别是，编译器非常擅长避免比实际必要的更频繁地分配和释放内存。

### 8.6.1 表达式求值

子表达式的求值顺序由旨在取悦优化器而非为程序员简化生活的规则所控制。这是不幸的，但无论如何，你都应该避免复杂的表达式，并且有一条简单的规则可以让你免于麻烦：如果在表达式中改变变量的值，不要在同一表达式中两次读取或写入它。例如：

```cpp
v[i] = ++i;            // don’t: undefined order of evaluation
v[++i] = i;            // don’t: undefined order of evaluation
int x = ++i + ++i;     // don't: undefined order of evaluation
cout << ++i << i << i << '\n'; // don't: undefined order of evaluation
f(++i,++i);            // don't: undefined order of evaluation
```

不幸的是，并非所有编译器在你编写这样的坏代码时都会发出警告；这是坏的，因为如果你将代码移动到另一台计算机，使用不同的编译器，或使用不同的优化器设置，你不能依赖结果相同。编译器在这种代码上确实存在差异；只要别这样做。

特别要注意，`=`（赋值）在表达式中仅被视为另一个运算符，因此不保证赋值的左侧在右侧之前求值。这就是为什么 `v[++i] = i` 是未定义的。

### 8.6.2 全局初始化

单个翻译单元中的全局变量（和命名空间变量；见 §8.7）按照它们出现的顺序初始化。例如：

```cpp
// file f1.cpp
int x1 = 1;
int y1 = x1+2;               // y1 becomes 3
```

从逻辑上讲，此初始化发生在“main() 中的代码执行之前”。

除最有限的环境外，使用全局变量通常不是一个好主意。我们已经提到过程序员没有真正有效的方法来知道大型程序中哪些部分读取和/或写入全局变量的问题（§8.4）。另一个问题是，不同翻译单元中全局变量的初始化顺序未定义。例如：

```cpp
// file f2.cpp
extern int y1;
int y2 = y1+2;               // y2 becomes 2 or 5
```

由于多种原因，应避免此类代码：它使用全局变量，它给全局变量取短名，并且它使用全局变量的复杂初始化。如果文件 `f1.cpp` 中的全局变量先于文件 `f2.cpp` 中的全局变量初始化，`y2` 将被初始化为 5（这是程序员可能天真且合理地预期的）。然而，如果文件 `f2.cpp` 中的全局变量先于文件 `f1.cpp` 中的全局变量初始化，`y2` 将被初始化为 2（因为用于全局变量的内存在进行复杂初始化尝试之前被初始化为 0）。避免此类代码，并在看到具有非平凡初始值的全局变量时要非常警惕；认为任何不是常量表达式的初始值都是复杂的。

