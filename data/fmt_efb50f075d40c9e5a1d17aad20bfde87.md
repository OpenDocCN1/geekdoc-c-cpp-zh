
我们比较了这两种方法，发现它们在做相同的事情。在迭代版本中，需要一个隐式或显式的条件来从函数返回。在迭代版本中，我们使用语句 `n--;` 将变量 `n` 的值减 1；而在递归版本中，我们在每次函数调用中 `n-1` 通过递归执行来调用该函数。

在迭代版本中，语句 `(cout << "*")` 被调用了 `n` 次，每次都是循环的一次迭代。在递归版本中，相同的语句在每次函数调用中执行。

在迭代版本中，我们只有一个函数调用；在递归版本中，我们有 `n-1` 次调用。在每次调用退出时，我们打印一个星号；在最后一次什么都不打印。前三次调用被称为通用情况 `general case`；最后一次调用被称为基础情况 `base case`。通用情况与执行操作的调用有关；基础情况与终止递归的情况有关。

![](img/ce9c99d45f71111839bc062830bd19fd_795_0.png)

| 图例 | |

|---|---|

| 函数调用 | |

| 递归函数，通用情况 | |

| 递归函数，基础情况 | |

| 迭代函数 | |

| main 函数 | |

| 调用 cout | |

**图 17.1** void 函数迭代调用与递归调用的对比

## 返回值的递归函数

假设我们需要找到从 0 到 `n` 的所有数字之和（通常称为求和）。我们可以编写两个函数，一个是迭代的，另一个递归的。然而，这些函数不是 void 函数；每个函数都必须返回和的值。

我们并列展示这两个函数，以观察迭代版本和递归版本之间的区别。我们再次使用 `while` 循环，这使得比较更加容易。

```cpp
// Iterative
int sum (int n) {
    int result = 0;
    while (n > 0) {
        result += n;
    }
    return result;
}
// Recursive
int sum (int n) {
    if (n <= 0) {
        return 0;
    }
    return sum (n - 1) + n;
}
```

在我们反向从 `n` 到 0 求数字和的情况下。换句话说，我们正在寻找 `sum = n + n-1 + n-2 + ... + 1`。在迭代情况下，如果 `n < 0`（终止情况），循环将跳过。在递归中，函数会显式地从函数返回。迭代函数在每次迭代中减少 `n` 的值；递归函数在每次函数调用中使用值 `n - 1` 调用同一个函数。图 17.2 形象地展示了每个字符的行为。

## 比较

当我们比较递归 `line` 函数（图 17.1）和递归 `sum` 函数（图 17.2）时，我们可以推导出 void 递归函数和返回值递归函数之间的区别。

![](img/ce9c99d45f71111839bc062830bd19fd_796_0.png)

在 void 函数的情况下，通用情况被连续调用直到到达基础情况；通用情况不持有任何信息。在返回值的函数的情况下，通用情况被调用直到到达基础情况。每个通用情况都必须持有某些信息 `n` 的值，直到对下一步的调用返回。基础情况将 `sum(0)` 的值返回给上一个情况，上一个情况将 `sum(1)` 的值返回给上一个通用情况，依此类推。

## 17.1.2 递归算法

在本节中，我们解决递归算法。

## 求和与阶乘

我们讨论了如何递归解决 `sum(n)` 问题。`sum(n)` 函数的兄弟函数是 `factorial(n)` 函数（也称为积）。我们必须加上从 `n` 到 0 的数字；在阶乘函数中，我们必须相乘从 `n` 到 1 的数字。

```cpp
// Sum function
int sum(int n) {
    if (n < 0)
        return 0;
    return sum(n - 1);
}

// Factorial function
int factorial(int n) {
    if (n <= 1)
        return 1;
    return factorial(n - 1);
}
```

注意 `sum(0)` 是 0，而 `factorial(1)` 是 1。在 `sum` 函数中，我们使用加法运算符；在 `factorial` 函数中，我们使用乘法运算符。注意在 `sum` 函数中，`sum(n-1)` 是下次调用返回的值，而在 `factorial` 函数中，`factorial(n-1)` 是下一次调用返回的值。可以看到 `sum` 增长缓慢，而 `factorial` 增长迅速。

## 17.1 求整数的和和阶乘的程序

| 1 | * 求整数的和和阶乘的程序 * |

| 2 | ************************************* |

| 3 | #include <iostream> |

| 4 | using namespace std; |

| 5 | |

| 6 | // sum 函数声明 |

| 7 | int sum(int n); |

| 8 | |

| 9 | // 阶乘函数的声明 |

| 10 | int factorial(int n); |

| 11 | |

| 12 | int main() { |

```cpp
13 {
14   // 测试 (0) 和 1
15   cout << "sum(0) = " << sum(0) << endl;
16   cout << "factorial(1) = " << factorial(1) << endl;
17   // 测试 3
18   cout << "sum(3) = " << sum(3) << endl;
19   cout << "factorial(3) = " << factorial(3) << endl;
20   // 测试 7
21   cout << "sum(7) = " << sum(7) << endl;
22   cout << "factorial(7) = " << factorial(7) << endl;
23   return 0;
24 }
```

```cpp
25 int sum(int n) {
26   if (n <= 0)
27     return 0;
28   return n + sum(n - 1);
29 }
30 
31 int factorial(int n) {
32   if (n <= 1)
33     return 1;
34   return n * factorial(n - 1);
35 }
```

```
运行:
sum(0) = 0
factorial(1) = 1

sum(3) = 6
factorial(3) = 6

sum(7) = 28
factorial(7) = 5040
```

## 公约数

数学和计算机科学中需要的一个函数是两个正整数的最大公约数，`gcd`。如果 `x % y = 0`，则整数 `y` 是 `x` 的除数。正整数可能有许多公约数，但只有一个最大公约数。

# 程序 17.2 最大公约数（继续）

```cpp
7 // gcd 函数的声明
8 int gcd(int first, int sec);
9
10 int main () {
11 // 检查五对数字的 gcd 
12 cout << "gcd(8, 6) = " << gcd(8, 6) << endl;
13 cout << "gcd(9, 12) = " << gcd(9, 12) << endl;
14 cout << "gcd(7, 11) = " << gcd(7, 11) << endl;
15 cout << "gcd(21, 35) = " << gcd(21, 35) << endl;
16 cout << "gcd(140, 12) = " << gcd(140, 12) << endl;
17 return 0;
18 }
19 // 最大公约数的递归定义
20 int gcd(int first, int sec) {
21 if (sec == 0) {
22     return first;
23 }
24 else {
25     return gcd(sec, first % sec);
26 }
27 }
```

```
运行:
gcd(8, 6) = 2
gcd(9, 12) = 3
gcd(7, 11) = 1
gcd(21, 35) = 7
gcd(140, 12) = 4
```

# 斐波那契数列

以一位意大利数学家的名字命名，斐波那契数列是一个序列，其中每个数字都是前两个数字之和。与递归问题不同，这个问题有两个基准情况，如表 17.2 所示。

图 17.5 显示了我们如何使用递归调用计算 `fib(n)`。注意，在找到 `fib(3)` 和 `fib(2)` 的返回值之前，我们无法找到 `fib(4)` 的返回值。

| 表 17.2 斐波那契数列的基准情况和一般情况 |

| 基准情况 | 一般情况 |

| fib (0) = 0, fib (1) = 1 | fib (n) = fib (n-1) + fib (n-2) |

# 17.1 引言 783

![](img/ce9c99d45f71111839bc062830bd19fd_801_0.png)

图 17.5 斐波那契数 `fib(4)` 的递归追踪

在找到 `fib(2)` 和 `fib(1)` 之前，我们无法找到 `fib(3)`。在找到 `fib(1)` 和 `fib(0)` 之前，我们无法找到 `fib(2)`。最后，我们找到了 `fib(0)` 和 `fib(1)` 的答案，它们就是基准情况。根据表 17.2 中斐波那契数列的定义，我们编写了一个递归函数来计算其中任何数字，如项目 17.3 所示。

# 项目 17.3 斐波那契数列的递归解

```cpp
****************************************
* 求斐波那契值的程序
****************************************/
#include <iostream>
using namespace std;
// 函数声明
long long fib(int n);
int main ()
{
    // 测试 0 到 10 的斐波那契数
    cout << "Fibonacci numbers from 0 to 10" << endl;
    for (int i = 0; i <= 10; i++) {
        cout << "fib " << i << " = " << fib(i) << endl;
    }
    return 0;
}
```

（继续）

# 程序 17.3 斐波那契数列的递归解（继续）

```cpp
10 // 测试 35 和 36 的斐波那契数
20 cout << "Fibonacci numbers of 35 and 36" << endl;
21 cout << "fib (35) = " << fib(36) << endl;
22 cout << "fib (36) = " << fib(36) << endl;
23 return 0;
24 }
25 // 函数定义
26 long long fib (int n)
27 {
28 if (n == 0 || n==1)
29 {
30 return n;
31 }
32 else
33 {
34 return fib (n - 2) + fib (n - 1);
35 }
36 }
```

运行:

Fibonacci numbers from 0 to 10

fib (0) = 0

fib (1) = 1

fib (2) = 1

fib (3) = 2

fib (4) = 3

fib (5) = 5

fib (6) = 8

fib (7) = 13

fib (8) = 21

fib (9) = 34

fib (10) = 55

Fibonacci numbers of 35 and 36

fib (35) = 9227465

fib (36) = 14930352

我们可以看到每个斐波那契数都是前两个数字之和。

# 反转字符串

另一个可以用递归解决的问题是反转字符串。我们可以像表 17.3 所示定义基准字符和一般情况。换句话说，如果字符串由零或一个字符组成，则反转字符串就是它本身。否则，我们需要找到子字符串的反转。

| 表 17.3 反转字符串的基准情况和一般情况 |

| 基准情况 | 一般情况 |

| if (length <= 1), return str | return reverse (substr(1, length - 1)) + substr (0, 1) |

```cpp
int main () {
    reverse("ABCD");
    reverse("BCD");
    reverse("CD");
    reverse("D");
}
```

图 17.6 调用 `reverse ("ABCD")` 的步骤

图 17.6 显示了我们如何递归地找到字符串的反转。每次调用都是另一个一般情况（去掉第一个字符）。换句话说，给定字符串 `"ABCD"`，第一次调用保留 `"A"` 作为子字符串并将 `"BCD"` 传递给下次调用。当返回 `"DC"` 时，它与 `"D"` 拼接形成 `"ABCD"`。17.4 显示了该问题的递归解。

# 程序 17.4 递归反转字符串

```cpp
/* 递归反转字符串的程序 */
#include <iostream>
#include <string>
using namespace std;

// 递归函数的声明
string reverse(string str);
```

# 程序 17.4 递归反转字符串（继续）

```cpp
int main () {
    // 使用一些字符串调用函数
    cout << "Reverse of 'ABCD': " << reverse("ABCD") << endl;
    cout << "Reverse of 'Hello': " << reverse("Hello") << endl;
    cout << "Reverse of 'Bye': " << reverse("Bye") << endl;
    return 0;
}

string reverse(string str) {
    if (str.length() <= 1) {
        return str;
    } else {
        return reverse(str.substr(1, str.length() - 1)) + str.substr(0, 1);
    }
}
```

运行:

Reverse of 'ABCD': DCBA

Reverse of 'Hello': olleh

Reverse of 'Bye': eyeB

检查回文

如果一个字符串正反读都是一样的，那么它就是回文。我们可以使用一个有两个基准情况和一个一般情况的递归函数来解决这个问题，如表 17.4 所示。第一种情况与空字符串或单字符字符串有关，这显然是回文。第二种情况与首尾字符不同的字符串有关，这显然不是回文。图 17.7 显示了我们如何使用基准情况和一般情况判断字符串是否为回文。程序 17.5 显示了递归函数 `isPalindrome` 的代码。

| 表 17.4 isPalindrome 函数的基准情况和一般情况 |

| --- | --- |

| 基准情况 | if (length <= 1) return true; else if (str[0] != str[str.size() - 1]) return false; |

| 一般情况 | return isPalindrome(str.substr(1, str.size() - 2)); |

# 17.1 引言 787

```cpp
int main () {
    isPalindrome("A");
    bool isPalindrome(string str); // true base case
```

```cpp
int main () {
    isPalindrome("ABC");
    bool isPalindrome(string str);
    isPalindrome("BCB");
    isPalindrome("ABA");
    isPalindrome("CC");
    isPalindrome(string str); // true case
```

+ 图例:

- 一般情况函数调用

- 基准情况返回值

- main 函数

> 注意：

> 我们有两种情况：

> 一个返回 true，

> 另一个返回 false。

图 17.7 `isPalindrome` 函数的情况。

# 程序 17.5 使用递归 isPalindrome 函数
