
## 自测题答案

- **1.** `int primes[] = { 2, 3, 5, 7, 11 };`

- **2.** 2, 3, 5, 3, 2

- **3.** 3, 4, 6, 8, 12

- **4.**
```cpp
values[0] = 0;
values[CAPACITY - 1] = 0;
```

- **5.**
```cpp
for (int i = SIZE - 1; i >= 0; i--)
{
    cout << values[i] << endl;
}
```

- **6.** `string words[10];`

- **7.** `string words[] = { "Yes", "No" };`

- **8.** 20 <= 最大值  
  10  
  20 <= 最大值

- **9.**
```cpp
int count = 0;
for (int i = 0; i < size; i++)
{
    if (values[i] == 0)
    {
        count++;
    }
}
```

- **10.** 如果 values 的所有元素都是负数，那么结果会被错误地计算为 0。

- **11.**
```cpp
for (int i = 0; i < size; i++)
{
    cout << values[i];
    if (i < size - 1)
    {
        cout << " | ";
    }
}
```

现在你知道为什么我们换一种方式设置循环了。

- **12.** 如果序列没有元素，那么会打印一个随机值。

- **13.** 如果找到匹配项，那么 pos 会在循环退出前递增。

- **14.** 这个循环将所有元素设置为 values[pos]。

- **15.** sum 函数会将 values 数组中的所有数字以及接下来的 900 个数字相加，从而产生一个随机结果。（实际上，程序可能无权访问所有这些数字，在这种情况下，操作系统会终止它。）

- **16.**
```cpp
int numbers[5];
squares(3, numbers);
```

- **17.**
```cpp
int find_first(double values[], int size, double searched_value)
{
    for (int pos = 0; pos < size; pos++)
    {
        if (values[pos] == searched_value)
        {
            return pos;
        }
    }
    return -1;
}
```

注意，这个循环比第 6.2.6 节中的循环更简单，因为一旦找到匹配项，我们就可以直接返回位置。

- **18.**
```cpp
void read_inputs(double inputs[], int capacity, int& size)
{
    size = 0;
    double input;
    while (cin >> input)
    {
        if (size < capacity)
        {
            inputs[size] = input;
            size++;
        }
    }
}
```

- **19.**
```cpp
int append(double first[], int first_size,
        double second[], int second_size,
        double target[], int target_capacity)
```

注意以下事项：

- 必须传入第一个和第二个数组的大小，以便函数知道要复制多少个元素。
- 必须传入目标数组的容量，以便函数不会写到末尾之外。
- 目标数组是一个参数变量——函数不能返回数组。
- 返回类型是 int，以便函数可以返回目标数组的大小。（或者，你可以使用引用参数 int& target_size。）

- **20.** 使用第一种算法。计算和时元素的顺序无关紧要。

- **21.** 找到最小值。  
  计算总和。  
  减去最小值。

- **22.** 使用计数匹配项的算法（第 4.7.2 节）两次，一次用于统计正值，一次用于统计负值。

- **23.** 你需要修改第 6.2.5 节中的算法。

```cpp
bool first = true;
for (int i = 0; i < size; i++)
{
    if (values[i] > 0)
    {
        if (first) { first = false; }
        else { cout << ", "; }
        cout << values[i];
    }
}
```

注意，你不能再使用 i > 0 作为打印分隔符的条件。

- **24.** 使用该算法将所有正值收集到一个数组中，然后使用第 6.2.5 节中的算法打印匹配项数组。

- **34.** board[0][0], board[1][1], board[2][2]

- **35.**
```cpp
vector<int> primes;
primes.push_back(2);
primes.push_back(3);
primes.push_back(5);
primes.push_back(7);
primes.push_back(11);
```

- **36.**
```cpp
vector<int> primes(5);
primes[0] = 2; primes[1] = 3; primes[2] = 5; primes[3] = 7; primes[4] = 11;
```

- **37.** 安、卡尔

- **38.** 题目没有说明进行了多少次测量。如果测量持续数月或数年（在科学或工业应用中很可能如此），那么 vector 是更好的选择。如果你知道测量数据只存储固定的一段时间（例如一天），那么数组也同样适用。

- **39.** 因为工作日的数量不会改变，所以使用数组没有劣势。

- **40.**
```cpp
vector<double> append(vector<double> first, vector<double> second)
```

将此与自测题 19 的答案进行对比。

- **41.** target 必须是引用参数，source 应该是值参数。

**表 1 指针语法示例**

假设有以下声明：

```cpp
int m = 10; // Assumed to be at address 20300
int n = 20; // Assumed to be at address 20304
int* p = &m;
```

| 表达式 | 值 | 注释 |
|---|---|---|
| `p` | 20300 | `m` 的地址。 |
| `*p` | 10 | 存储在该地址的值。 |
| `&n` | 20304 | `n` 的地址。 |
| `p = &n;` |  | 将 `p` 设置为 `n` 的地址。 |
| `*p` | 20 | 存储在更改后地址的值。 |
| `m = *p;` |  | 将 20 存储到 `m` 中。 |
| ❌ `m = p;` | **错误** | `m` 是 int 值；`p` 是 `int*` 指针。这些类型不兼容。 |
| ❌ `&10` | **错误** | 只能取变量的地址。 |
| ❌ `&p` | `p` 的地址，可能是 20308 | 这是指针变量的位置，而不是整数的位置。 |
| ❌ `double x = 0;<br>p = &x;` | **错误** | `p` 的类型是 `int*`，`&x` 的类型是 `double*`。这些类型不兼容。 |

### 7.1.3 初始化指针

使用指针时，特别注意正确初始化尤为重要。

初始化指针时，请确保指针和内存地址具有相同的类型。例如，以下初始化会出错：

```cpp
int balance = 1000;
double* account_pointer = &balance; // Error!
```

地址 `&balance` 是指向 int 值的指针，也就是说，是 `int*` 类型的表达式。用 `int*` 初始化 `double*` 指针永远不合法。

使用未初始化的指针是错误的。

如果定义指针变量时没有提供初始值，该指针会包含一个随机地址。使用该随机地址是错误的。在实践中，如果使用未初始化的指针，程序很可能会崩溃或出现莫名其妙的异常行为：

```cpp
double* account_pointer;
    // Forgot to initialize
*account_pointer = 1000;
    // NO! account_pointer contains an unpredictable value
```

有一个特殊值 NULL，应使用它来表示不指向任何位置的指针。如果定义了指针变量但还不想立即初始化它，请将其设置为 NULL。

NULL 指针不指向任何对象。

```cpp
double* account_pointer = NULL;  // Will set later
```

稍后可以测试该指针是否仍为 NULL。如果是，就不要使用它。

```cpp
if (account_pointer != NULL) { cout << *account_pointer; }  // OK
```

试图通过 NULL 指针访问数据是非法的，并且会导致程序终止。

以下程序演示指针的行为。我们执行两次相同的取款语句，但 account_pointer 的值不同。每次都会修改不同的账户。

### ch07/accounts.cpp

```cpp
#include <iostream>

using namespace std;

int main()
{
   double harrys_account = 0;
   double joint_account = 2000;
   double* account_pointer = &harrys_account;

   *account_pointer = 1000;  // Initial deposit

   *account_pointer = *account_pointer - 100;  // Withdraw $100
   cout << "Balance: " << *account_pointer << endl;  // Print balance

   // Change the pointer value
   account_pointer = &joint_account;

   // The same statements affect a different account
   *account_pointer = *account_pointer - 100;  // Withdraw $100
   cout << "Balance: " << *account_pointer << endl;  // Print balance

   return 0;
}
```

### 程序运行

```cpp
Balance: 900
Balance: 1900
```

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_339_0.png)

- **1.** 考虑以下这组语句。会打印什么？

```cpp
int a = 1;
int b = 2;
int* p = &a;
cout << *p << endl;
p = &b;
cout << *p << endl;
```

- **2.** 考虑以下这组语句。会打印什么？

```cpp
int a = 1;
int b = 2;
```
