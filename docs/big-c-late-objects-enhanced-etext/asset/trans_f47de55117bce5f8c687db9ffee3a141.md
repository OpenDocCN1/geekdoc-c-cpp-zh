

**步骤6** 测试你的函数。

提供一个仅测试此函数的程序：

```cpp
int main()
{
    srand(time(0));
    for (int i = 1; i <= 10; i++)
    {
        cout << random_character("abcdef");
    }
    cout << endl;
    return 0;
}
```

运行此程序时，你可能会得到类似以下的输出：

```text
acfdfeefac
```

这确认了函数工作正常。

## 重复第二个辅助函数的过程

最后，我们实现第二个辅助函数，它将在字符串的随机位置插入一个包含单个字符的字符串。

**步骤1** 描述函数应该做什么。

假设我们有一个字符串 "arxcsw" 和一个字符串 "8"。那么第二个字符串应该被插入到字符串中的随机位置，例如 "ar8xcsw" 或 "arxcsw8"。实际上，第二个字符串长度为 1 并不重要，因此我们只需规定我们的函数应将任意字符串插入到给定字符串中。

**步骤2** 确定函数的“输入”。

第一个输入是另一个字符串将被插入进去的字符串。第二个输入是要插入的字符串。

**步骤3** 确定参数变量和返回值的类型。

两个输入的类型都是 `string`。返回值也是一个字符串。我们现在可以完整地描述我们的函数：

```cpp
/**
    Inserts one string into another at a random position.
    @param str the string into which another string is inserted
    @param to_insert the string to be inserted
    @return the result of inserting to_insert into str
*/
string insert_at_random(string str, string to_insert)
```

**步骤4** 编写获取所需结果的伪代码。

没有预定义的函数可以将一个字符串插入另一个字符串。相反，我们需要找到插入位置，然后通过提取两个子字符串来“拆分”第一个字符串：插入位置之前的字符，以及其后的字符。

插入位置有多少种选择？如果 `str` 的长度为 6，则有七种选择：

1. `|arxcsw`
2. `a|rxcsw`
3. `ar|xcsw`
4. `arx|csw`
5. `arxc|sw`
6. `arxcs|w`
7. `arxcsw|`

```cpp
using namespace std;

/**
Returns a string containing one character randomly chosen from a given string.
@param characters the string from which to randomly choose a character
@return a substring of length 1, taken at a random index
*/
string random_character(string characters)
{
    int n = characters.length();
    int r = rand() % n;
    return characters.substr(r, 1);
}

/**
Inserts one string into another at a random position.
@param str the string into which another string is inserted
@param to_insert the string to be inserted
@return the result of inserting to_insert into str
*/
string insert_at_random(string str, string to_insert)
{
    int n = str.length();
    int r = rand() % (n + 1);
    return str.substr(0, r) + to_insert + str.substr(r);
}

/**
Generates a random password.
@param length the length of the password
@return a password of the given length with one digit and one
special symbol
*/
string make_password(int length)
{
    string password = "";

    // Pick random letters
    for (int i = 0; i < length - 2; i++)
    {
        password = password + random_character("abcdefghijklmnopqrstuvwxyz");
    }

    // Insert two random digits
    string random_digit = random_character("0123456789");
    password = insert_at_random(password, random_digit);
    string random_symbol = random_character("+-*?!@#$%");
    password = insert_at_random(password, random_symbol);
    return password;
}

int main()
{
    srand(time(0));
    string result = make_password(8);
    cout << result << endl;
    return 0;
}
```

## 完整示例 5.2

### 使用调试器

![](img/d61019b035dd82beb581604273c0ee6b_296_0.png)

毫无疑问，到目前为止你已经意识到，计算机程序很少能在第一次运行时完美无缺。有时，找出错误（程序员所称的 bug）可能会令人非常沮丧。当然，你可以在代码中插入打印语句，以显示程序流程和关键变量的值。然后运行程序并尝试分析输出。但如果输出没有明确指向问题所在，你就需要添加和删除打印语句，然后再次运行程序。这可能是一个耗时的过程。

现代开发环境都包含一个调试器，即一个帮助你定位错误的程序，让你能够跟踪程序的执行。你可以在程序临时停止时停止、重启程序，并查看变量的内容。在每次停止时，你都可以决定运行多少步程序直到下一次停止。

### 步骤1

与编译器一样，调试器也因系统而异。大多数集成开发环境的调试器具有相似的布局——参见下面的示例。你需要弄清楚如何准备一个待调试的程序，以及如何在你的系统上启动调试器。对于许多开发环境，你可以简单地选择一条菜单命令来构建调试版本的程序并启动调试器。

![](img/d61019b035dd82beb581604273c0ee6b_296_1.png)

Visual Studio 调试器

```cpp
int main()
{
    cout << "Please enter the upper limit: ";
    int n;
    cin >> n;
    for (int i = 1; i <= n; i = i + 2)
    {
        if (isprime(i))
        {
            cout << i << endl;
        }
    }
}
```

现在我们想知道为什么程序将 1 视为素数。单步进入 isprime 函数。注意调用堆栈的显示。它表明 isprime 函数当前处于活动状态，并且它是由 main 函数调用的。

![](img/d61019b035dd82beb581604273c0ee6b_300_0.png)

检查变量 n，确认它当前为 1。

![](img/d61019b035dd82beb581604273c0ee6b_300_1.png)

执行“逐过程”（step over）命令几次。你会注意到程序跳过了两个 if 语句。这并不奇怪——1 是奇数。然后程序跳过 while 语句，准备返回 true，表示 1 是素数。

检查 k 的值。它是 3，这解释了为什么 while 循环从未进入。看起来 isprime 函数需要重写，将 1 作为特例处理。

接下来，我们想知道为什么即使 isprime 函数认为 2 是素数，程序也不打印 2 为素数。继续调试。它将在第 51 行的断点处停止。

注意 i 是 3。现在原因变得清楚了。main 函数中的 for 循环只测试奇数。要么 main 应该同时测试奇数和偶数，或者更好的是，它应该将 2 作为特例处理。

最后，我们想弄清楚为什么程序认为 9 是素数。继续调试，直到在 i = 9 时遇到断点。单步进入 isprime 函数。现在反复使用“逐过程”命令。两个 if 语句被跳过，这是正确的，因为 9 是奇数。程序再次跳过 while 循环。检查 k 以找出原因。k 是 3。查看 while 循环中的条件。它测试 k * k < n。现在 k * k 是 9，n 也是 9，因此测试失败。

在检查 n 是否为素数时，只测试不超过 √n 的因数是合理的。如果 n 可以分解为 p × q，那么这两个因数不可能都大于 √n。但实际上这并不完全正确。如果 n 是某个素数的完全平方数，那么它唯一的非平凡因数等于 √n。9 = 3 × 3 正是这种情况。我们应该测试 k * k <= n。

通过运行调试器，我们发现了程序中的三个错误：

- isprime 错误地将 1 视为素数。
- main 函数没有测试 2。
- isprime 中有一个差一错误。while 语句的条件应为 k * k <= n。

以下是改进后的程序：

```cpp
#include <iostream>

using namespace std;

/**
 * Tests if an integer is a prime.
 * @param n any positive integer
 * @return true if n is a prime, false otherwise
 */
bool isprime(int n)
{
    if (n == 1)
    {
        // 1 is not a prime
        return false;
    }
    if (n == 2)
    {
        // 2 is a prime
        return true;
    }
    if (n % 2 == 0)
    {
        // No other even number is a prime
        return false;
    }

    // Try finding a number that divides n

    int k = 3; // No need to divide by 2 since n is odd
    // Only need to try divisors up to sqrt(n)
    while (k * k <= n)
    {
        if (n % k == 0)
        {
            // n is not a prime since it is divisible by k
            return false;
        }
        // Try next odd number
        k = k + 2;
    }

    return true;
}
```

