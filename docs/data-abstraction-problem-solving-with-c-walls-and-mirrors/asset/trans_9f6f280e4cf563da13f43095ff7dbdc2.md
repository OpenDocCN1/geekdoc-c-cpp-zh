

- 3. 编写一个递归函数，计算一个至少包含 $n$ 个整数的数组中前 $n$ 个整数的和。
  提示：从第 $n$ 个整数开始。

- 4. 给定两个整数 *start* 和 *end*，其中 *end* 大于 *start*，编写一个递归 C++ 函数，返回从 *start* 到 *end* 的所有整数之和（包含边界）。

- 5. a. 修改 2.3.1 节中讨论的递归函数 *writeBackward*，使其基准情况为长度为 1 的字符串。
  b. 编写一个 C++ 函数，实现 2.3.1 节给出的伪代码函数 *writeBackward*。

- 6. 描述以下递归函数存在的问题：

```cpp
void printNum(int n)
{
    cout << n << endl;
    printNum(n - 1);
}
```

- 7. 给定一个整数 $n > 0$，编写一个递归 C++ 函数，输出整数 1, 2, . . , $n$。

- 8. 给定一个整数 $n = 0$，编写一个递归 C++ 函数，输出 $n$ 的平方和。

- 9. 编写一个递归 C++ 函数，按反序输出一个正整数的各个数字。

- 10. a. 编写一个递归 C++ 函数 *writeLine*，通过重复某个字符形成一个包含 $n$ 个字符的行。例如，*writeLine('*', 5)* 生成行 *****。
  b. 编写一个递归 C++ 函数 *writeBlock*，使用 *writeLine* 输出 $m$ 行每行 $n$ 个字符的内容。例如，*writeBlock('*', 5, 3)* 输出：

```
*****
*****
*****
```

- 11. 下面程序会产生什么输出？

```cpp
int getValue(int a, int b, int n);

int main()
{
    cout << getValue(1, 7, 7) << endl;
    return 0;
    // end main

int getValue(int a, int b, int n)
{
    int returnValue = 0;
    cout << "Enter: a = " << a << " b = " << b << endl;
    int c = (a + b)/2;
    if (c * c < n)
        returnValue = c;
    else
        returnValue = getValue(a, c-1, n);

    cout << "Leave: a = " << a << " b = " << b << endl;
    return returnValue;
}
// end getValue
```

- 12. 下面程序会产生什么输出？

```cpp
int search(int first, int last, int n);
int mystery(int n);

int main()
{
    cout << mystery(30) << endl;
    return 0;
} // end main
int search(int first, int last, int n)
{
    int returnValue = 0;
    cout << "Enter: first = " << first << " last = " << last << endl;
    int mid = (first + last) / 2;
    if (mid == n) && (n < (mid+1))
        returnValue = mid;
    else if (mid > n)
        returnValue = search(first, mid-1, n);
    else
        returnValue = search(mid+1, last, n);

    cout << "Leave: first = " << first << " last = " << last << endl;
    return returnValue;
} // end search
int mystery(int n)
{
    return search(n, n, n);
} // end mystery
```

- 13. 考虑以下函数，它将十进制数转换为八进制并显示结果。

```cpp
void displayOctal(int n)
{
    if (n > 0)
    {
        if (n / 8 > 0)
            displayOctal(n / 8);
        cout << n % 8;
    } // end if
} // end displayOctal
```
描述该算法的工作原理。使用 $n = 100$ 对函数进行执行追踪。

- 14. 考虑以下程序：

```cpp
int f(int n)
int main()
{
    cout << "The value of f(8) is " << f(8) << endl;
    return 0;
} // end main
/* pre n >= 0. */
int f(int n)
{
    cout << "Function entered with n = " << n << endl;
    switch (n)
{
  case 0: case 1: case 2:
    return n + 1;
  default:
    return f(n-2) * f(n-4);
} // end switch
} end f
```
显示程序的精确输出。向函数 $f$ 传递什么参数（如果有）会导致程序无限运行？

- 15. 考虑以下函数：

```cpp
void recurse(int x, int y)
{
  if (y > 0)
  {
    x++;
    y--;
    cout << x << " " << y << endl;
    recurse(x, y);
    cout << x << " " << y << endl;
  } // end if
} end recurse
```
使用 $x = 5$ 和 $y = 3$ 执行该函数。输出会受到影响吗？

- 16. 对以下递归函数执行追踪，使用 $x = 5$ 和 $y = 3$：
  a. 5
  b. 13

- 17. 假设你有 101 个整数，且没有相同的数字。你创建一个 101 的数组；第一个整数是，第二个是，以此类推。你的朋友想知道是否存在 99。
  a. 如果你使用二分查找 99，你会先做什么？
  b. 二分查找将进行多少次比较？
  c. 如果大于 99，二分查找找到的索引是多少？

- 18. 考虑以下关系：
f(1) = 1; f(2) = 1; f(3) = 2; f(4) = 3; f(5) = 5; 对于所有 $n > 5$。
  a. 为 $n = 6, 7, 12, 15$ 计算 $f(n)$。
  b. 如果你仔细地计算 $f(n)$，你将避免重复计算相同的值。（回顾本章末尾的递归函数。）

利用这些观察结果，编写一个计算任意 $f(n)$ 的 C++ 函数。

- 19. 写递归函数 fact、writeBinary 和 binarySearch 的迭代版本。

- 20. 使用不变性证明 2.7 节中的迭代函数是正确的。（关于不变性的讨论见附录 F。）

- 21. 考虑寻找两个正整数 $a$ 和 $b$ 的最大公约数 (gcd) 问题。这里介绍的算法是欧几里得算法的一个版本，它基于：
**定理。** 如果 $a, b$ 是正整数且 $a > b$，则 $gcd(a, b) = gcd(b, a \bmod b)$。

$gcd(a, b)$ 与 $b, a \bmod b$ 之间的关系是递归解的核心。它规定了如何通过相同类型的问题来求解 $gcd(a, b)$。此外，如果 $b$ 整除 $a$，则 $b = gcd(a, b)$，因此合适的基准情况是 $(a \bmod b) = 0$。

- 22. 修改递归函数以便于理解。不要只打印“进入”和“退出”消息，而是通过缩进追踪来显示当前调用的“深度”。例如，递归调用 rabbit(4) 应该产生：

```
Enter: n = 4
  Enter: n = 3
    Enter: n = 2
      Enter: n = 1
      Leave: n = 1 value 1
    Leave: n = 2 value 1
  Leave: n = 3 value 2
Leave: n = 4 value 3
```
注意这如何对应图 2-19。

- 23. power2 和 power3 在计算 $3^2$ 时执行多少次乘法？
- 24. power2 和 power3 在计算 $3^2$ 时会有多少次递归调用？

本书使用作为数学运算的缩写。在 C++ 中，取模运算符是 %.

