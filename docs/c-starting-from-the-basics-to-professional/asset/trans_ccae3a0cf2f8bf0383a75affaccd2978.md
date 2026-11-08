
现在毫无疑问，比较会先被求值。不过，大多数有经验的程序员可能不会在这里加上这些额外的括号。

### 逻辑或

逻辑或运算符 || 适用于当两个操作数中有一个或两个都为 true 时希望结果为 true 的情况。只有当两个操作数都为 false 时，结果才为 false。

例如，如果你的年收入至少为 $100,000，或者你有 $1,000,000 现金，那么你可能会被认为信用足够好，可以获得银行贷款。可以这样测试：

```cpp
if (income >= 100'000.00 || capital >= 1'000'000.00)
{
    std::cout << "Of course, how much do you want to borrow?" << std::endl;
}
```

当两个条件中有一个或两个都为 true 时，就会输出这个响应。（更好的响应可能是“你为什么要借钱？”很奇怪，银行只会在你不需要钱的时候才借钱给你。）

还要注意，我们使用了数字分隔符来提高数字字面量的可读性：1'000'000.00 等于一百万，这比 1000000.00 明显得多。如果没有分隔符，你甚至能看出 1'000'000.00 和 1000000.00 之间的区别吗？（如果银行在填写这两个数字中的任何一个时犯了错误，你肯定希望错误对你有利！）

### 逻辑非

第三个逻辑运算符 ! 作用于单个 bool 操作数，并反转其值。因此，如果 bool 变量 test 的值为 true，那么 !test 为 false；如果 test 为 false，那么 !test 的结果为 true。

与所有逻辑运算符一样，你可以将逻辑非应用于任何求值为 true 或 false 的表达式。操作数可以是任何内容，从单个 bool 变量到比较和 bool 变量的复杂组合。例如，假设 x 的值为 10。那么表达式 !(x > 5) 的求值结果为 false，因为 x > 5 为 true。当然，在这种特定情况下，你也许最好直接写 x <= 5。后一个表达式是等价的，但由于它不包含逻辑非，可能更易读。

**注意** 设 foo、bar 和 xyzzy 是 bool 类型的变量（如果你愿意，也可以是任意表达式）。那么，像你这样的 C++ 初学者经常写出这样的语句：

```cpp
if (foo == true) ...
if (bar == false) ...
if (xyzzy != true) ...
```

虽然从技术上讲是正确的，但人们普遍认为，你应该改用下面这些等价但更短的 if 语句：

```cpp
if (foo) ...
if (!bar) ...
if (!xyzzy) ...
```

### 组合逻辑运算符

你可以按自己觉得舒服的程度任意组合条件表达式和逻辑运算符。这个示例实现了一个问卷，用来判断一个人是否是良好的贷款风险对象：

```cpp
// Ex4_06.cpp
// Combining logical operators for loan approval
import <iostream>;

int main()
{
    int age {};              // Age of the prospective borrower
    int income {};           // Income of the prospective borrower
    int balance {};          // Current bank balance

    // Get the basic data for assessing the loan
    std::cout << "Please enter your age in years: ";
    std::cin >> age;
    std::cout << "Please enter your annual income in dollars: ";
    std::cin >> income;
    std::cout << "What is your current account balance in dollars: ";
    std::cin >> balance;

    // We only lend to people who are at least 21 years of age,
    // who make over $25,000 per year,
    // or have over $100,000 in their account, or both.
    if (age >= 21 && (income > 25'000 || balance > 100'000))
    {
        // OK, you are good for the loan - but how much?
        // This will be the lesser of twice income and half balance
        int loan {};         // Stores maximum loan amount
        if (2*income < balance/2)
        {
            loan = 2*income;
        }
        else
        {
            loan = balance/2;
        }
        std::cout << "\nYou can borrow up to $" << loan << std::endl;
    }
    else    // No loan for you...
    {
        std::cout << "\nUnfortunately, you don't qualify for a loan." << std::endl;
    }
}
```

以下是一些示例输出：

```
Please enter your age in years: 25
Please enter your annual income in dollars: 28000
What is your current account balance in dollars: 185000

You can borrow up to $56000
```

有趣的部分是决定是否批准贷款的 if 语句。if 条件如下：

```
age >= 21 && (income > 25'000 || balance > 100'000)
```

这个条件要求申请人的年龄至少为 21 岁，并且其收入大于 $25,000 或账户余额大于 $100,000。表达式 (income > 25'000 || balance > 100'000) 两边的括号是必要的，以确保将收入和余额条件进行或运算的结果与年龄测试的结果进行与运算。没有括号时，年龄测试会与收入测试进行与运算，然后结果再与余额测试进行或运算。这是因为 && 的优先级高于 ||，正如你在第 3 章的表中所看到的那样。有了括号，这个条件本来会允许一个账户余额超过 $100,000 的 8 岁孩子获得贷款。这不是原本的意图。银行从不贷款给未成年人和八哥。

如果条件为 true，则执行确定贷款金额的语句块。loan 变量定义在这个块内，因此在块结束时会不复存在。块内的 if 语句判断申报收入的两倍是否小于账户余额的一半。如果是，贷款金额为收入的两倍；否则为账户余额的一半。这确保贷款金额符合规则所限定的最小金额。

> **提示** 组合逻辑运算符时，建议始终添加括号以阐明代码。

为了讨论方便，假设银行允许贷款的条件如下：

```
(age < 30 && income > 25'000) || (age >= 30 && balance > 100'000)
```

也就是说，对于较年轻的客户，决定完全取决于他们的年薪——是的，甚至幼儿也能获得贷款，当然，只要他们能提供足够收入的证明——而更成熟的客户必须已经拥有足够的储蓄。那么你也可以把这个条件写成如下形式：

```
age < 30 && income > 25'000 || age >= 30 && balance > 100'000
```

虽然两个表达式完全等价，但你肯定会同意，带括号的那个比不带括号的更容易阅读。因此，在组合 && 和 || 时，建议始终通过添加括号来阐明逻辑表达式的含义，即使严格来说并不需要这样做。

### 整数操作数上的逻辑运算符

在某种程度上，逻辑运算符可以——而且实际上相当频繁地——应用于整数操作数，而不是布尔操作数。例如，前面你看到过，可以用下面的代码测试 int 变量 value 是否不等于零：

```cpp
    if (value)
        std::cout << "You have entered a value that is different from zero." << std::endl;
```

同样常见的是，你会遇到以下形式的测试：

```cpp
    if (!value)
        std::cout << "You have entered a value that equals zero." << std::endl;
```

这里，逻辑非应用于整数操作数——而不是像通常那样应用于布尔操作数。类似地，假设你定义了两个 int 变量 value1 和 value2；那么你可以这样写：

```cpp
    if (value1 && value2)
        std::cout << "Both values are non-zero." << std::endl;
```

因为这些表达式非常简短，所以它们在 C++ 程序员中很流行。这种模式的典型用例出现在这些整数值表示例如对象集合中元素数量的情况下。因此，理解它们如何工作很重要：在此类表达式中，逻辑运算符的每个数值操作数都会先使用熟悉的规则转换为 bool：零转换为 false，其他所有数字转换为 true。不过，即使所有操作数都是整数，逻辑表达式仍然会求值为 bool。

### 逻辑运算符与按位运算符

重要的是，不要把作用于可转换为 bool 的操作数的逻辑运算符 &&、|| 和 ! 与作用于整型操作数内部各位的按位运算符 &、| 和 ^ 混淆。

从上一小节你会记得，逻辑运算符总是求值为 bool 类型的值，即使其操作数是整数。按位运算符则相反：它们总是求值为一个整数，即使两个操作数都是 bool 类型。然而，由于按位运算符的整数结果总是会转换回 bool，所以常常看起来逻辑运算符和按位运算符可以互换使用。例如，Ex4_06 中用于测试贷款是否可批准的核心测试，原则上可以这样写：

```cpp
    if (age >= 21 && (income > 25'000 | balance > 100'000))
    {
        ...
    }
```

这样写可以编译，并且最终结果与之前仍然使用 && 和 || 时相同。简而言之，发生的情况是：比较产生的 bool 值被转换为 int，然后使用按位运算符按位组合成一个单独的 int，之后这个单独的 int 又会为 if 语句转换回 bool。感到困惑？别担心，这并不那么重要。这种在 bool 和整数之间来回转换的情况很少会引起担忧。

然而，重要的是这两组运算符之间第二个更根本的区别；即，与按位运算符不同，二元逻辑运算符是所谓的短路运算符。
