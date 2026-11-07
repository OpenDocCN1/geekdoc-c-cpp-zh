
例如，函数 A 调用函数 B，而函数 B 又回调函数 A。这仍然是递归，因为对函数 A 的第二次调用是在对函数 A 的第一次调用仍处于活动状态时进行的。也就是说，对函数 A 的第一次调用尚未执行完毕（因为它正在等待函数 B 向它返回结果），并且尚未返回给函数 A 的原始调用者。

## 栈溢出与无限递归

计算机中的内存量是有限的，因此只有一定量的内存可用于在函数调用栈上存储活动记录。如果发生的递归函数调用多到其活动记录无法全部存储在栈上，就会发生一种称为栈溢出的致命错误。这通常由无限递归引起，而无限递归可能是由于遗漏基本情况或错误地编写递归步骤，使其无法收敛到基本情况而造成的。无限递归类似于迭代解法中的无限循环。

## 递归与函数调用栈

在第 5.10 节中，我们在理解 C++ 如何执行函数调用的背景下介绍了栈数据结构。我们讨论了**函数调用栈**和**栈帧**。那部分讨论也适用于递归函数调用。每个递归函数调用都会在函数调用栈上获得自己的栈帧。当某个调用完成时，系统会从栈中弹出该函数的栈帧，控制权返回给调用者，这个调用者可能是同一函数的另一个副本。

## 检查点

- 1. *（对/错）* 为了使递归可行，递归解法中的递归步骤必须类似于原始问题，但要是它的一个稍大的版本。

**答案：** 错误。为了使递归可行，递归解法中的递归步骤必须类似于原始问题，但要是它的一个稍小或更简单的版本。

- 2. *（代码）* 下面的代码应递归计算从 0 到参数值 `number` 的整数之和。找出以下函数中的错误并改正代码：

```cpp
int sum(int number) {  // assume n is nonnegative
    if (number == 0)
        return 0;
    else
        number + sum(number - 1);
}
```

**答案：** 递归步骤应返回 `number + sum(number - 1)` 的结果：

```cpp
int sum(int number) {  // assume n is nonnegative
    if (number == 0)
        return 0;
    else
        return number + sum(number - 1);
}
```

25. 网站 stackoverflow.com 就是这样得名的。这是一个获取编程问题答案的极好网站。

- 3. **（代码）** 重写下面的迭代阶乘计算代码，使循环向上计数而不是向下计数：

```cpp
using boost::multiprecision::cpp_int;
cpp_int factorial{1};
for (int counter{number}; counter >= 1; --counter) {
    factorial *= counter;
}
```

**答案：**

```cpp
using boost::multiprecision::cpp_int;
cpp_int factorial{1};
for (int counter{1}; counter <= number; ++counter) {
    factorial *= counter;
}
```

## 5.16.3 递归斐波那契数列示例

斐波那契数列，

0, 1, 1, 2, 3, 5, 8, 13, 21, …

以 0 和 1 开始，并且具有这样的性质：随后的每个斐波那契数都是前两个数之和。这个数列在自然界中出现，并描述了一种螺旋形态。

相邻斐波那契数之比收敛于常数 1.618…，这个数称为**黄金比例**或**黄金均值**。许多人认为黄金均值具有美感。建筑师经常按照黄金均值的比例设计窗户、房间和建筑物的长和宽。明信片通常按照黄金均值的长宽比来设计。

## 递归斐波那契定义

斐波那契数列可以递归地定义如下：

- fibonacci(0) 定义为 0
- fibonacci(1) 定义为 1
- fibonacci(*number*) 定义为 fibonacci(*number* − 1) + fibonacci(*number* − 2)

斐波那契计算有两个基本情况：

- fibonacci(0) 为 0，并且
- fibonacci(1) 为 1。

## 函数 fibonacci

图 5.15 的程序使用函数 fibonacci 递归计算第 *n* 个斐波那契数。斐波那契数会很快变大，尽管比阶乘慢得多。图 5.15 还展示了程序的执行情况，其中显示若干数字的斐波那契值。

```cpp
// fig05_15.cpp
// Recursive function fibonacci.
#include <format>
#include <iostream>
using namespace std;

long fibonacci(long number); // function prototype

int main() {
   // calculate the fibonacci values of 0 through 10
   for (int counter{0}; counter <= 10; ++counter) {
      cout << format("fibonacci({}) = {}\n",
         counter, fibonacci(counter));
   }

   // display higher fibonacci values
   cout << format("fibonacci(20) = {}\n", fibonacci(20))
      << format("fibonacci(30) = {}\n", fibonacci(30))
      << format("fibonacci(35) = {}\n", fibonacci(35));
}

// recursive function fibonacci
long fibonacci(long number) {
   if ((0 == number) || (1 == number)) { // base cases
      return number;
   }
   else { // recursion step
      return fibonacci(number - 1) + fibonacci(number - 2);
   }
}
```

```text
fibonacci(0) = 0
fibonacci(1) = 1
fibonacci(2) = 1
fibonacci(3) = 2
fibonacci(4) = 3
fibonacci(5) = 5
fibonacci(6) = 8
fibonacci(7) = 13
fibonacci(8) = 21
fibonacci(9) = 34
fibonacci(10) = 55

fibonacci(20) = 6765
fibonacci(30) = 832040
fibonacci(35) = 9227465
```

**图 5.15** | 递归函数 fibonacci。

函数 fibonacci（第 23–30 行）递归计算第 n 个斐波那契数。从 main 对函数 fibonacci 的每次初始调用都不是递归调用。然而，随后从函数 fibonacci 的函数体中执行的所有 fibonacci 调用都是递归调用，因为此时这些调用是由该函数自身发起的。每次调用 fibonacci 都会立即测试基本情况——number 等于 0 或 number 等于 1。如果 number 匹配某个基本情况，第 25 行会返回 number，因为 `fibonacci(0)` 为 0，且 `fibonacci(1)` 为 1。有趣的是，如果 number 大于 1，递归步骤会产生两个递归调用，每个调用处理的问题都比对 `fibonacci` 的原始调用稍小。

### 测试函数 `fibonacci`

第 11–14 行中的 for 循环测试 `fibonacci`，显示 0–10 的斐波那契值。变量 counter 指示在循环的每次迭代中要计算哪个斐波那契数。第 17–19 行还计算数字 20、30 和 35 的斐波那契值。你会注意到，对于更高的斐波那契值，计算速度会显著变慢。

### 分析对函数 `fibonacci` 的调用

下图展示了函数 `fibonacci` 如何求值 `fibonacci(3)`：

- 在图的底部，我们得到值 1、0 和 1——这些是求值基本情况的结果。
- 前两个返回值（从左到右）1 和 0，分别作为调用 `fibonacci(1)` 和 `fibonacci(0)` 的值返回。
- 1 加 0 的和作为 `fibonacci(2)` 的值返回。这个值被加到最右侧对 `fibonacci(1)` 的调用结果（1）上，得到值 2。
- 然后这个最终值作为 `fibonacci(3)` 的值返回。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_294_0.png)

### 复杂度问题

对于像我们这里用来生成斐波那契数的递归程序，有必要提出一点警告。对 `fibonacci` 函数的每次调用，如果不匹配某个基本情况（0 或 1），都会导致对 `fibonacci` 函数的**另外两次递归调用**。因此，这组递归调用会迅速失控。使用递归实现计算 20 的斐波那契值需要对 `fibonacci` 函数进行 21,891 次调用；计算 30 的斐波那契值需要 2,692,537 次调用！

当你尝试计算更大的斐波那契值时，你会注意到，每计算一个后续斐波那契数，计算时间以及对 `fibonacci` 函数的调用次数都会大幅增加。例如，31 的斐波那契值需要 4,356,617 次调用，32 的斐波那契值需要 7,049,155 次调用！当你
