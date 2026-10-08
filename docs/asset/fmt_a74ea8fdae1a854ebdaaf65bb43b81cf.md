
## 2 lambda 表达式的求值产生一个临时对象（2.2）。这被称为闭包对象。lambda 表达式不应出现在等待的操作（第 5 节）、模板中、别名声明中、类型定义中，或函数体之外的默认参数中。其意图是防止 lambda 表达式出现在签名中。—— 注释 | 注意：闭包对象的行为类似于函数对象（2.9）。—— 注释

## 3 lambda 表达式的类型（也是闭包对象的类型）是一个唯一的、未命名的类——被称为闭包类型，其属性在下文中描述。该类在块作用域、类作用域或包含该 lambda 表达式的命名空间中声明。[注意：聚合（8.5）不是字面量类型（3.9）。] 与闭包类型相关的命名空间和类（3.4）。lambda 声明符的参数不影响这些命名空间和类。—— 注释

实现可以根据以下内容定义闭包类型，而不改变程序的可观测行为，除了：

+ (3.1) 闭包类型的大小和对齐，
- (3.2) 闭包类型是否可拷贝（第 9 节），
- (3.3) 闭包类型是否为标准布局类（第 9 节），
- (3.4) 闭包类型是否为 POD 类（第 9 节）。

实现不应添加 lambda 值的成员，除非 lambda 声明符为 `()`。lambda 返回类型是 `auto`，如果提供的话，或者从 7.1.6 的返回语句中推导。示例：

```cpp
auto x1 = [](){ return i; }; // OK 返回类型为 int
auto x2 = { return 1 }; // 错误：从初始化列表推导返回类型
int j;
auto x3 = []()->auto&&{ return j; }; // OK 返回类型为 int&
```

- 非通用 lambda 表达式的闭包有一个公共内联函数调用运算符（13.5.4），其参数和返回类型分别由 lambda 表达式的参数声明子和 lambda 类型描述。对于通用 lambda，闭包有一个公共内联函数调用运算符模板（14.5.2），其模板参数列表由 lambda 参数声明子中出现的每个 `auto` 对应的一个发明模板参数组成，按出现顺序排列。发明模板参数由与每个 `auto` 的参数声明子匹配的参数包组成（8.3.7）。函数调用运算符的参数和返回类型由 lambda 表达式返回类型和参数声明子，并将参数声明子中的每个 `auto` 替换为相应的发明模板参数的名字。示例：

```cpp
auto lambda = [](auto a, auto&& b){ return a < b; }; // OK
bool b = lambda(3, 3.14);
auto vtglambda = [](auto... ts){ // OK ts 是函数参数包
return [=](ts ...);
print(std::forward<decltype(ts)>(ts));
};
return [=]{
print(ts ...);
};
auto p = vtglambda({auto v1, auto v2, auto v3}); // std::cout << v1 << v2 << v3 << }; // OK 输出 13.14
q = p(1, 'a', 3.14); // OK 输出 13.14
```

- 相应的函数调用运算符或运算符模板被声明为 `const`（9.3.1），当且仅当 lambda 表达式的参数声明子后面没有跟 `mutable`。它既不是虚的也不是重载的。lambda 表达式中的任何异常规范适用于相应的函数调用运算符或运算符模板。lambda 声明符中的属性序列对应相应的函数调用运算符或运算符模板的类型。[注意：lambda 声明符引用的名称在 lambda 表达式出现的环境中查找。—— 注释

非通用 lambda 表达式的闭包有一个公共内联函数调用运算符（13.5.4），其参数和返回类型分别由 lambda 表达式的参数声明子和 lambda 类型描述。对于通用 lambda，闭包有一个公共内联函数调用运算符模板（14.5.2），其模板参数列表由 lambda 参数声明子中每个 `auto` 对应的一个发明模板参数组成，按出现顺序排列。发明模板参数由与每个 `auto` 的参数声明子匹配的参数包组成（8.3.7）。函数调用运算符的参数和返回类型源自表达式返回类型和参数声明子，并将参数声明子中的每个 `auto` 替换为相应的发明模板参数的名字。

此函数调用运算符或运算符模板被声明为 `const`（9.3.1），当且仅当 lambda 表达式的参数声明子后面没有跟 `mutable`。它既不是虚的也不是重载的。lambda 表达式中的任何异常规范适用于相应的函数调用运算符或运算符模板。lambda 声明符中的属性序列对应相应的函数调用运算符或运算符模板的类型。[注意：lambda 声明符引用的名称在 lambda 表达式出现的环境中查找。—— 注释

非通用 lambda 表达式的闭包有一个公共内联函数调用运算符（13.5.4），其参数和返回类型分别由 lambda 表达式的参数声明子和 lambda 类型描述。对于通用 lambda，闭包有一个公共内联函数调用运算符模板（14.5.2），其模板参数列表由 lambda 参数声明子中每个 `auto` 对应的一个发明模板参数组成，按出现顺序排列。发明模板参数由与每个 `auto` 的参数声明子匹配的参数包组成（8.3.7）。函数调用运算符的参数和返回类型源自 lambda 表达式返回类型和参数声明子，并将参数声明子中的每个 `auto` 替换为相应的发明模板参数的名字。

# ©ISO/IEC

# N4296

(11.1) 如果是通过拷贝捕获（见下文），则为捕获声明的非静态数据成员和变量被视为引用同一对象的两种不同方式，其生命周期为该非静态数据成员，且不执行额外的捕获和析毁。

(11.2) 如果是通过引用捕获，则变量的生命周期在闭包对象的生命周期结束结束。

> [注意：这允许内联捕获，如 `x = std::move(x)`；"x" 必须绑定到周围上下文中的声明。] [示例]:

```cpp
int x = 4;
auto y = {r, x = x1()}-int {
    r +==2;
    return x*2;
} // 更新：x 为 6，并初始化 y 为 7。
```

- 示例结束

12 一个关联了默认捕获且未显式捕获 `this` 或具有自动存储周期的 lambda 表达式，包含了任何被发现引用初始化捕获（init-capture）的非静态数据成员的任何表达式，如果复合语句：

视为隐式捕获了该实体（即 `this` 或一个变量），如果：

(12.1) ODR 使用 (3.2) 该实体，或
(12.2) 在可能求值的表达式 (3.2) 中命名该实体，其中该完整表达式取决于在 lambda 表达式可作用域内声明的通用 lambda 参数。

示例：

```cpp
void f(int, const int *(k)[2] = {}) {} //1
void f(const int, const int *(k)[1]) {} //2
void test() {
    const int x = 17;
    auto g = [](auto a) {
        f(x); // OK：调用 #1，未捕获 x
    }

    auto g2 = [&](auto a) {
        int selector[sizeof(a)] = 1 ? 2 : 0;
        f(x, selector); // OK：是一个依赖表达式，因此捕获 x
    }
}
```

- 示例结束 所有此类隐式捕获的实体都应该在 lambda 表达式的可作用域内声明。[注意：嵌套 lambda 表达式对实体的隐式捕获可能会导致包含它的 lambda 表达式对其隐式捕获（见下文）。对此的 ODR 使用可能导致隐式捕获。] -- 注意结束

§ 5.1.2

# ISO/IEC

# N4296

```cpp
void f1(int i) {
    int const N = 20;
    auto m1 = [&]{
        int const M = 30;
        auto m2 = [i]{
            int x[N][M];
            x[0][0] = i;
        }; // OK：N 和 M 未被 od 使用
           // OK：i 被 m2 显式捕获
           // 并被 m1 隐式捕获
    };

    struct s1 {
        int f;
        void work(int n) {
            int m = n;
            int j = 40;
            auto m3 = [this,m]{
                int x = n; // 错误：j 未被 m3 捕获
                           // 错误：n 被 m4 隐式捕获
                           // 但未被 m3 捕获
                           // OK：m 被 m4 隐式捕获
                           // 并被 m3 显式捕获
                           // 错误：i 在可作用域之外
                x *= m;
                x *= i;
                x *= f; // OK：this 被 m4 隐式捕获
                       // 并被 m3 显式捕获
            };
        }
    };
}
```

出现在默认参数中的 lambda 表达式不应隐式或显式地捕获任何实体。

示例：

```cpp
void f2() {
    int i = 1;
    void g1(int = ({i]{ return i; })); // 错误
    void g2(int = ({[]{ return 0;})); // 错误
    void g3(int = ({=]{ return i;})); // 错误
    void g4(int = ({[]{ return 0;})); // OK
    void g5(int = ([]{ return sizeof(i);})); // OK
}
```

- 如果实体被隐式或显式捕获，且默认捕获为 `=` 或以标识符形式显式捕获，则对于每个捕获的实体，未命名的非静态成员在闭包类型中声明。这些成员的声明顺序是不确定的。该数据成员的类型取决于被捕获的实体是否不是一个对象，否则如此。[注意：如果被捕获的实体是指向函数的，则对应的数据成员也是指向函数的引用。] -- 注意

- 如果实体被引用捕获，且它是隐式或显式捕获但未被拷贝捕获，则闭包类型中是否声明了额外的未命名非静态数据成员是不确定的。匿名联合体的成员不应被引用捕获。

§ 5.1.2

如果一个 lambda 表达式 m2 捕获了一个实体，且该实体被其包含的 lambda 表达式 m1 捕获，则 m2 的捕获转换如下：

示例：下面的嵌套 lambda 表达式和调用输出 12324。

```cpp
int a = 1, b = 2, c = 3;
auto m1 = [a, b, c]() mutable {
    std::cout << a << b << c;
};
auto m2 = [a, b, c]() mutable {
    a += 1; b += 1; c += 1;
    std::cout << a << b << c;
};
m1();
m2();
```

# ISO/IEC N4296

对于一个未展开的参数包，该表达式被称为二元左折叠。如果 e1 包含一个未展开的参数包，该表达式被称为二元右折叠。[示例]:

```cpp
template <typename ...Args>
bool f(Args ...args) {
    return (the && &&args);
}
```

```cpp
template <typename ...Args>
bool f(Args ...args) {
    return (args + ... + args); // error：两个操作数都包含未展开的参数包
}
```

-- 示例结束

## 5.2 后置表达式 [expr.post]

- 1 后置表达式从左到右分组。

  ```cpp
  postfix-expression:
  primary-expression
  postfix-expression [ expression ]
  postfix-expression [ braced-list ]
  postfix-expression [ expression-list ]
  simple-type-specifier [ expression-list ]
  typename-specifier [ expression-list ]
  simple-type-specifier braced-list
  postfix-expression . template_opt id-expression
  postfix-expression -> template_opt id-expression
  postfix-expression . pseudo-destructor-name
  postfix-expression > pseudo-destructor-name
  postfix-expression --
  dynamic_cast < type-id > ( expression )
  static_cast < type-id > ( expression )
  reinterpret_cast < type-id > ( expression )
  const_cast < type-id > ( expression )
  typeid ( type-id )
  initializer-list
  pseudo-destructor-name:
  nested-type-specifier opt_type name :: type-name
  nested-type-specifier template simple-template-id :: type-name
  type-name
  type-specifier
  ```

- 2 [注：在 dynamic_cast, static_cast, reinterpret_cast, const_cast 中的 > 可能是将一个标记 > 替换为两个标记 > (14.2) 的结果。— 结束] [expr.sub]

## 5.2.1 下标访问

- 1 后置表达式后接方括号中的表达式是一个后置表达式。其中一个表达式的类型应为“T 的数组”或“指向 T 的指针”，另一个应为完全无作用域的枚举类型或整数类型。结果的类型为“T”。类型“T”应当是一个完全定义的对象类型。

64) 如果在以下常用惯用法中使用下标运算符：k[]，则此条式为真。

表达式 E1[2]（根据定义）等同于 *⟨E1⟩⟨E2⟩* [注：* 的细节请参见 5.3 和 5.7，数组的细节请参见 8.3.4。— 注结束]；但在数组的情况下，如果操作数是左值，则结果为左值，否则为右值。

- 2 大括号初始化列表（Braced-init-list）不与内置下标运算符一起。

## 5.2 函数调用

- 1 函数调用是一个后置表达式，后接括号和一个可能为空的、逗号分隔的初始化列表，该列表包含函数的参数。后置表达式应具有函数类型或指向该类型的指针。对于对非静态函数或静态成员的调用，后置表达式应为左值或函数（在这种情况下，对后置表达式应用函数到指针的标准转换 (4.3)），或具有指向该类型的指针。通过类型语言链接属性与被调用函数类型链接属性不同的表达式来调用函数是允许的 (7.5)。对于式类访问 (5.2.5)，id-expression 是一个函数名，或是一个选择成员的指向成员的表达式 (5.5)；该调用是作为表达式所指类对象的成员调用的。在隐式类访问中，表达式转换为指向对象的指针，且 ⟨f⟩ 的成员函数调用被解释为 *⟨this⟩.f*（参见 9.3.1）。— 注结束 如果使用了函数名或成员名，该名称可能被重载（第 13 章），在这种情况下调用该表达式。如果选定的函数 id-expression 不是虚的，或者该调用是虚的，否则调用其在对象动态类型中的最终重写（final override）(10.3)；此类调用被称为虚函数调用。— 注：12.7 描述了当对象指向派生类构造时虚函数调用的行为。

> 注：如果函数名或成员名且名称查找 (3.4) 未找到该名称的声明，则程序因该调用而定义错误。— 注结束

> 如果后置调用指定一个析构函数 (12.4)，则函数调用的类型为 void；忽略静态选择函数的返回类型（即忽略虚 关键字），即使实际上选择了该类型也是如此。此返回类型应当是一个对象，或者是 void。

当函数被调用时，其参数 (8.5) 使用其对应的参数进行初始化 (8.5, 12.1, 12.8, 12.1) — 注：初始化彼此之间的可能是序化顺序是不确定的 (1.9) （— 注结束）。如果该函数是非静态成员，如果通过隐式转换 (5.2) 进行了转换，则该函数的参数 (9.3.2) 应被初始化为指向类对象的指针。

# 显式类型转换（函数符号法）

简单类型转换 (7.1.6.2) 或 typename (14.6) 后跟一个带括号的表达式列表，构造由表达式列表指定的类型的值。如果表达式是单个表达式，则该类型转换在确定性上（以及在意义上有定义的情况下）等于相应的强制类型转换 (5.4)。如果表达式是类类型，且该类型指定了多个值，则该类类型必须是声明了构造函数的类 (8.5, 12.1)，且表达式 `T(x1, x2, ...)` 在效果上等于临时变量 `t` 的声明 `T(x1, x2, ...)`，通过将结果作为 `t` 的值返回。
