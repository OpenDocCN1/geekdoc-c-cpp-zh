

# 单次递归调递归

如果一个递归函数调用自身，那么新调用的函数会再次调用自身，以此类推，无限循环，除非代码中包含了终止调用的内容。通常的方法是将递归函数调用作为 `if` 语句的一部分。例如，一个名为 `recurs()` 的类型递归函数可能如下所示：

```cpp
void recurs(argumentlist)
{
    statements1
    if (test)
        recurs(arguments)
    statements2
}
```

由于运气或远见，`test` 最终变为假，调用链就会被中断。递归调用产生了一个有趣的事件链。只要 `if` 语句为真，每次调用 `recurs()` 都会执行 `statements1` 并调用一个新的 `recurs()` 实例，而不会到达 `statements2`。当 `if` 语句结束时，当前调用将执行 `statements2`。然后当前调用调用了它。接着，该版本的 `recurs()` 执行它的 `statements2` 部分并终止，返回到之前的调用，依此类推。因此，如果 `recurs()` 经历了五次递归调用，第一个 `statements1` 部分将按照函数调用的顺序执行五次，而 `statements2` 部分将按照调用顺序的相反顺序执行五次。进入五层递归后，程序必须通过这相同的五层退回。列表 7.16 说明了这种行为。

# 列表 7.16 recurs.cpp

```cpp
// 使用递归的 recurs.cpp
#include <iostream>
void countdown(int n);

int main()
{
    countdown(4);       调用递归函数
    return 0;
}

void countdown(int n)
{
    using namespace std;
    cout << "Counting down ... " << n << endl;
    if (n > 0)
    {
        countdown(n-1);   // 函数调用自身
        cout << n << ": Kaboom!\n";
    }
```

这里是列表 7.16 中程序的注释输出：

- Counting down ... 4 <level 1; 增加递归深度
- Counting down ... 3 <level 2
- Counting down ... 2 <level 3
- Counting down ... 1 <level 4
- Counting down ... 0 <level 5; 最后一次递归调用
- 0: Kaboom! <level 5; 开始退回
- 1: Kaboom! <level 4
- 2: Kaboom! <level 3
- 3: Kaboom! <level 2
- 4: Kaboom! <level 1

注意，每个递归调用都会创建自己的一组变量 `n`，每个变量都有不同的值。当程序到达悬崖时，它已经有了五个独立的变量。你可以通过修改列表 7.16，使其显示 `n` 的输出及其值来亲自验证这一点：

```cpp
cout << "Counting down ... " << n << " (at n " << &n << ")" << endl;
...
cout << n << " : Kaboom!" << (at n " << &n << ")" << endl;
```

这样做会产生如下所示输出：

- Counting down ... 4 (n at 0012FE0C)
- Counting down ... 3 (n at 0012FD34)
- Counting down ... 2 (n at 0012FCSC)
- Counting down ... 1 (n at 0012FB84)
- Counting down ... 0 (n at 0012FAAC)
- 0: Kaboom! (n at 0012FAAC)
- 1: Kaboom! (n at 0012FB84)
- 2: Kaboom! (n at 0012FCSC)
- 3: Kaboom! (n at 0012FD34)
- 4: Kaboom! (n at 0012FE0C)

注意值为 4 的 `n` 存储在一个位置（内存地址 0012FE0C），值为 3 的 `n` 存储在第二个位置（内存地址 0012FD34），依此类推。此外，注意“倒计时”阶段特定层级的 `n` 地址与“Kaboom!”阶段相同层级的地址是相同的。

# 多次递归调用

递归对于可以通过将一个任务拆分为两个相似任务来重复的任务特别有用。例如，考虑这种画尺子的方法：标记两端，找到中点并进行标记。然后将此相同过程应用于尺子的左半部分和右半部分。如果你需要更多拆分，则对每个拆分应用相同的过程。这种递归方法有时被称为分治策略。列表 7.17 使用递归函数 `subdivide()` 说明了这种方法。它使用一个除了两端有 `|` 外的字符串。主程序使用循环调用 `subdivide` 六次，每次增加递归深度并打印结果字符串。因此，每次输出代表额外的递归层。为了提醒你这是一个选项，程序使用了递归而不是循环。

# 列表 7.17 ruler.cpp

```cpp
// 使用递归划分尺子的 ruler.cpp
#include <iostream>
const int Len = 6;
const int Divs = 6;
void subdivide(char ar[], int low, int level);
int main() {
    char ruler[Len];
    int i;
    for (i = 1; i < Len - 2; i++)
        ruler[i] = ' ';
    ruler[Len - 1] = '|';
    int max = Len - 2;
    int min = 0;
    ruler[min] = '|';
    cout << ruler << endl;
    for (i = 1; i <= Divs; i++) {
        subdivide(ruler, min, i); i        cout <<cout << endl;
        for (int j = 1; j < Len - 2; j++)
            ruler[j] = ' '; // 重置为空
    }
    return 0;
}

void subdivide(char ar[], int low, int high, int level) {
    if (level == 0)
        return;
    int mid = (high + low) / 2;
    ar[mid] = '|';
    subdivide(ar, mid, level -  );
    subdivide(ar,,,, - 1);
}
```

这里是列表 7.17 程序的输出：
![](img/cd11a87c1db9aff4dbb183432746375.png)

# 程序注释

列表 7.17 中的 `subdivide()` 函数使用变量 `level` 控制递归。当函数调用自身时，它将 `level` 减一，`level` 为 0 的函数终止。`subdivide()` 调用自身两次，一次针对左划分，一次针对右划分。原始中点变为一次调用的右端，另一个调用的左端。注意调用次数是几何级数增长的。也就是说，一次调用产生两个，四个，八个，依此类推。6 级调用能够填充 64 个元素（2⁶=64）。调用次数（以及存储变量的数量）的持续倍增使得如果需要许多递归层，这种递归形式是一个糟糕的选择。但如果需要的递归层很少，这是一个优雅且简单的选择。

# 函数指针

讨论 C 或 C++ 函数，不提到函数指针是不完整的。我们将快速查看这个主题，并将可能的详细解释留给更高级的教材。

函数像数据一样地址。函数的地址是存储的机器代码开始的内存地址。通常，对于你或用户来说，知道这个地址并不重要，但对程序可能有用。例如，可以写一个接受另一个函数地址作为参数的函数。这使得第一个函数能够找到并运行第二个函数。这种方法比直接调用第二个函数要笨拙，但它留下了在不同时间传递不同函数地址的可能性。这意味着第一个函数可以在不同时间使用不同的函数地址。

# 函数指针基础

让我们通过示例来澄清这个过程。假设你想设计一个 `estimate()` 函数，用于估计编写指定行数代码所需的时间，并且让不同的程序员使用该函数。`estimate()` 的部分代码对所有用户都是相同的，但该函数允许每个程序员提供他们自己的估计时间算法。该机制是向 `estimate()` 传递程序员想要使用的特定算法函数的地址。要实现这一点，你需要能够：

- 获取函数的地址。
- 声明一个函数指针。
- 使用函数指针来调用函数。

# 获取函数的地址

获取函数的地址很简单：使用不带后缀括号的函数名。也就是说，如果 `think()` 是一个函数，那么 `think` 就是函数的地址。要将函数作为参数传递，只需传递函数名。务必区分传递函数的地址和传递函数的返回值：

```cpp
process(think); // 将 think 的地址传递给
thought(think()); // 将 think() 的返回值传递给
```

`process()` 允许在函数内部调用该函数。`thought()` 则先调用 `think()` 函数，将其返回值传递给 `thought()` 函数。

# 声明函数指针

要声明指向数据类型的指针，声明必须精确指定指针指向的类型。同样，指向函数的指针必须指定指针指向的函数类型。这意味着声明应该标识函数的返回类型和函数的签名（其参数列表）。也就是说，声明提供的函数信息与原型相同。例如，假设 LeCode 使用一个具有如下原型的时间估计函数：

```cpp
double pam(int); // 原型
```

> 提示
通常情况下，要声明指向特定类型函数的指针，你可以先写一个所需类型普通函数的原型，然后将函数名替换为 `(*pf)` 形式的表达式。在这种情况下，`pf` 是一个指向类型函数的指针。

```cpp
double (*pf)(int); // pf 指向一个接受
// 一个参数并
// 返回类型 double 的函数
```

