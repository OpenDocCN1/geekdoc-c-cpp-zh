
这也很有可能带来非常快的程序代码。与 `const` 或 `inline` 不同，如果编译器无法再在翻译期计算结果，而该计算会耗费运行期时间，它会通知你。然而，编译器是否真的按所述方式预计算结果，仍由它决定。

借助 `constexpr`，你可以定义自己的字面量数据类型，如第23章第23.7节所示。

在运行程序时实现最终最小时间消耗的最高形式，是 C++20 引入的用于*立即函数*的 `consteval` 修饰符。这确保编译器可以在翻译期计算表达式，并将其插入调用处：一如既往，它不必这样做，但很可能会这样做。你可以在第13章第13.10.8节了解更多关于 `consteval` 的内容。

### 7.12.4 删除的函数

如果你想禁止对函数的某种特定使用，可以写 `= delete` 来代替函数体：

```cpp
double add(double a, double b) { return a + b; }
double add(int, int) = delete;   // prohibit add(3,4)
```

如果没有带 `= delete` 的第二行，编译器会自动把 3 和 4 转换为 double。通过让它知道 `add(int,int)` 的声明，它随后会选择这一个。然而，通过使用 `= delete`，你告诉编译器你明确不想要这种行为，它就会发出错误消息。

### 7.12.5 类方法中的特殊之处

对于属于类的函数，你还会遇到一些额外内容；至少应在这里看到它们，以便阅读时能够识别。从第12章开始，我会更详细地讨论这些内容：

```cpp
// https://godbolt.org/z/8Gdso36zf
class Widget : public Base {
    explicit Widget(int);        // no automatic conversion from int
    ~Widget();                   // Destructor with ~ before the name
    virtual void update();      // prefixed with virtual
    void calc() override;       // suffixed with override
    void calc2() final;         // suffixed with final
    void draw() const;          // suffixed with const
    virtual void paint() = 0;   // abstract method
};
```

- 使用 `explicit`，可以阻止 `int` 被自动转换为 `Widget`。它用于构造函数（初始化器）和转换运算符之前。
- 函数名前的符号 `~`（波浪号）使该函数成为*析构函数*。当对象被销毁时，它会自动被调用。析构函数的名称必须与类名匹配。
- `virtual` 关键字使该方法准备好由派生类中的另一个实现覆盖。这常用于逻辑相关的对象层次结构中的可扩展性。
- `override` 是一种编程辅助手段，可防止在使用 `virtual` 覆盖时出现粗心错误。它保证你确实在覆盖某个方法。
- `final` 也用于派生类中的 `virtual` 方法，并防止该方法将来再次被覆盖。
- 用 `const` 标记的方法承诺不改变对象的状态。
- 一个 `virtual` 方法如果被设为 `= 0` 而不是实现，就是*纯虚函数*。为了让该类能够被实例化，该方法必须在派生类中被覆盖。在 Java 和一些其他语言中，这被称为*抽象方法*。

## 第8章

### 语句详解

**本章提要**

- **空语句**  
  由分号 `;` 组成的语句不执行任何操作。
- **块语句**  
  用花括号 `{…}` 括起来的一系列语句。
- **声明语句**  
  声明新变量，可能带有初始化。
- **表达式语句**  
  任何表达式也可以用作语句。
- **if 语句**  
  有条件地执行后续语句。
- **while 循环**  
  重复执行语句，条件位于开头。
- **do-while 循环**  
  类似 while 循环，但条件位于末尾。
- **for 循环**  
  类似 while 循环，但带有额外的初始化和推进部分。
- **基于范围的 for 循环**  
  遍历容器中所有元素的循环。
- **switch 语句**  
  在单个语句中用 case 进行多重区分。
- **break 语句**  
  退出当前循环或 switch。
- **continue 语句**  
  以下一次迭代继续当前循环。
- **return 语句**  
  退出当前函数。
- **goto 语句**  
  跳转到用标签命名的另一条语句。
- **try 块**  
  处理异常的语句块（预览）。

在本章中，你将详细了解不同类型的语句。我将主要通过一个实际示例来演示它们的用法。

在开头，我会重温前几章的一些主题，并更详细地讨论它们。这样，你会遇到一些重复，但理解会更深入，而且不必不断翻回去查阅。

### 语句

语句是一段做某事的代码；例如，它执行赋值或循环。（线程的）语句按顺序执行。

这个程序计算一个可自由确定范围内的所有质数——就程序的简短程度而言，相当高效。

```cpp
// https://godbolt.org/z/Y33TzcfST
#include <iostream>                 // cout
#include <vector>                   // container vector
#include <string>                   // stoi
int inputUpTo(int argc, const char* argv[]) {
    /* Determine number */
    int upTo = 0;                   // introduce new variable
    if(argc<1) {                    // if statement with then and else block
        std::cout << "Up to what number do you want to calculate prime numbers? ";
        if(!(std::cin >> upTo)) {   // check return value
            return -1;              // error in user input
        }
    } else {                        // else part of the if statement
        upTo = std::stoi(argv[1]);
    }
    return upTo;                    // return input
}
std::vector<int> primes{2};         // new vector<int> with initialization
bool isPrime(int n) {
    /* primes must be sorted in ascending order */
    for(int factor : primes) {      // range-based for loop
        if(factor*factor > n)       // too large to be a divisor at all?
            return true;            // then terminate the inner loop early
        if(n%factor==0)              // is divisor?
            return false;           // ... then exit
    }
    return true;                    // no divisor found
}

void calculatePrimesUpTo(int upTo) {
    /* Primes calculation */
    /* vector must contain {2} at this point */
    for(int n=3; n<upTo; n=n+2) {      // standard for loop
        if(isPrime(n)) {
            primes.push_back(n);        // is prime – mark as divisor and result
        }
    }
}

void outputPrimes() {
    for(int prime : primes) {           // range based, over all elements
        std::cout << prime << " ";
    }
    std::cout << "\n";
}

int main(int argc, const char* argv[]) {
    int upTo = inputUpTo(argc, argv);   // declares variable
    if(upTo < 2) { return 1; }          // exit main with non-okay value.
    calculatePrimesUpTo(upTo);
    outputPrimes();
    return 0;
}
```

**清单 8.1** 计算用户定义范围内的所有质数。

首先看一下这个程序的粗略结构。之后，我会详细讲解不同的语句。

除了 main()，我还定义了四个辅助函数：inputUpTo()、isPrime()、calculatePrimesUpTo() 和 outputPrimes()。inputUpTo() 函数接收与 main() 相同的参数，以便要么解析命令行，要么在控制台请求输入一个数字，如你在第4章清单4.10所见。isPrime() 将可能的质数作为参数，并返回一个 bool 值，表示该参数是否为质数。

在函数之间，定义了全局变量 primes。由于它是全局的，不在函数内，甚至不在块内，所有函数都可以访问它。

该变量的类型是 `vector<int>`；这是一种特别适合按顺序添加新元素的容器。我使用 `primes.push_back(n)` 来实现这一点。在 C++17 中，写 `vector` 就足够了，因为编译器会在初始化时从 2 推断出 `<int>`。
