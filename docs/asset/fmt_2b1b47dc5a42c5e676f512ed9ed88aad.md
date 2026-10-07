
所做的。

## 14.3 递归思考

`search(a, mid + 1, last, key, found, location);`

的。如果递归调用是正确的，那么整个操作就是正确的。因此，在两种情况下，函数都执行了正确的操作（假设递归调用执行了正确的操作）。

`search` 函数通过了我们的三项测试，因此是一个良好的递归函数定义。

## 效率

与简单按顺序尝试所有数组元素的算法相比，二分搜索算法的速度极快。在二分搜索中，你从开始开始就排除了一半的数组。然后你又排除掉四分之一、八分之一，以此类推。这些节省的步骤累积起来带来了惊人的速度提升。对于一个包含 100 个元素的数组，二分搜索与键比较的次数永远不会超过 7 次。而简单的搜索可能会与键比较多达 100 个元素，且平均比较次数为 50 次。此外，数组越大，节省的效率就越显著。对于一个包含 1000 个元素的数组，二分搜索仅需键比较大约 10 次，而简单搜索算法的平均比较次数为 500 次。在某些情况下，迭代版本运行比递归版本更高效。迭代版本的算法是通过镜像递归版本推导出来的。在迭代版本中，局部变量 `first` 和 `last` 首先镜像了递归版本中参数的角色，这些参数也命名为 `first` 和 `last`。正如示例所示，即使你倾向于将其转换为迭代算法，推导递归算法也是有意义的。

迭代版本

### 显示 14.8 二分搜索的迭代版本（部分 1/2）

#### 函数声明

```
void search(const int a[], int lowEnd, int highEnd,
  int key, bool &found, int &location);
//前置条件：a[lowEnd] 到 a[highEnd] 已按升序排序。
//后置条件：如果 key 不是 a[lowEnd] 到 a[highEnd] 中的值之一，
// 则 found == false；否则，a[location] == key 且 found == true。
```

#### 函数定义

```
void search(const int a[], int lowEnd, int highEnd,
  int key, bool &found, int &location)
{
  int first = lowEnd;
  int last = highEnd;
```
（继续）

### 显示 14.8 二分搜索的迭代版本（部分 2/2）

```
int mid;
found = false; //到为止
while ( (first <= last) && !(found)
{
    mid = (first + last)/2;
    if (key == a[mid])
    {
        found = true;
        location = mid;
    } else if (key < a[mid])
    {
        last = mid - 1;
    } else if (key > a[mid])
    {
        first = mid + 1;
    }
}
```

## 编程示例 A 递归成员函数

类的成员函数可以是递归的。成员函数使用递归的方式与普通函数相同。显示 14.9 包含一个递归成员函数的示例。该显示使用的 `BankAccount` 类与显示 10.6 中的类名相同，在其中我们重载了成员函数 `update`。`update` 的第一个版本没有参数，并计算一年的单利。另一个（新）版本的 `update` 接受一个 `int` 参数，表示若干年。该成员函数通过存入相应年份的利息来更新账户。`update` 的新版本是递归的；有一个参数，名为 `years`；并使用以下算法：

如果年数为 1，则 //停止情况：
调用另一个名为 `update` 的函数（那个没有参数的）。
如果年数大于 1，则 //递归情况：
进行递归调用以存入 `years-1` 的利息，然后调用另一个名为 `update` 的函数（那个没有参数的）来存入一年的利息。

### 显示 14.9 递归成员函数（部分 1/2）

```
//演示递归成员函数 updates 的程序
#include <iostream>
using namespace std;
// 银行账户类：
class BankAccount {
public:
    BankAccount(int dollars, int cents, double rate);
    // 初始化账户余额为 $dollars.cents 并
    // 初始化利率为百分比。
    BankAccount(int dollars, double rate);
    // 初始化账户余额为 $dollars.00
    // 初始化利率为百分比。
    BankAccount();
    // 初始化账户余额为 $0.00 并
    // 初始化利率为 0.0%。
    void update();
    // 前置条件：一年的单利
    // 已添加到账户余额中。
    void update(int years);
    // 前置条件：给定年份的利息已添加到
    // 账户余额中。利息按年复合。
    double getBalance();
    // 返回当前账户余额。
    double getRate();
    // 返回以百分比表示的当前利率。
    void output(ostream &out);
    // 前置条件：如果 out 是文件输出流，则 out 已经
    // 连接到文件。
    // 后置条件：余额和利率已写入输出流 outs 中。
private:
    double balance;
    double interestRate;
    double fraction(double percent); // 将百分比转换为分数。
};
int main() {
    BankAccount yourAccount(100, 5);
    yourAccount.update(10);
    cout.setf(ios::fixed);
```

### 显示 14.9 递归成员函数（部分 2/2）

```cpp
42  cout.setf(ios::showpoint);
43  cout.precision(2);
44  cout << "如果你存入 $100.00，利率为 5%，那么\n"
45      << "十年后你的账户价值为 $"
46      << yourAccount.getBalance() << endl;
47  return 0;
48  }
49  
50  void BankAccount::update()
51  {
52      balance = balance + fraction(interestRate)*balance;
53  }
54  void BankAccount::update(int years)
55  {
56      if (years == 1)
57      {
58          update();
59      }
60      else if (years > 1)
61      {
62          update(years - 1);
63          update();
64      }
65  }
```

# 自测题

15. 为以下函数编写一个递归函数定义：

```cpp
int squares(int n);
// 前提：n >= 1
// 返回从 1 到 n 的数字平方和。
```

例如，`squares(3)` 返回 14，因为 `1^2 + 2^2 + 3^2` 等于 14。

16. 为显示 14.9 中描述的单参数成员函数 `BankAccount::update(int years)` 写一个迭代版本。

# 章节总结

- 如果一个问题可以简化为相同问题的更小规模实例，那么递归解决方案可能很容易找到并实现。
- 函数的递归算法通常包含两种情况：一种或多个包含至少一次递归调用的情况，以及一个停止情况（在那种情况下，不进行任何递归调用即可解决问题）。
- 在编写递归函数定义时，务必确认该函数不会产生无限递归。
- 当定义递归函数时，使用“递归设计技术”节中的三个标准来确认函数的正确性。
- 在设计递归函数来解决某个任务时，通常需要解决一个比给定任务更通用的问题。为了允许适当的递归调用，这是必要的，因为较小的问题可能与给定任务不相同。例如，在二分查找问题中，任务是搜索整个数组，但递归解决方案是搜索数组任何部分（无论是数组本身还是其一部分）的算法。

# 自测题答案

1. Hip Hip Hurray

```cpp
void stars(int n)
{
    cout << "";
    if (n > 1)
        stars(n - 1);
}
```

# 自测题 857 答案

以下内容也是正确的，但更复杂：

```cpp
void stars(int n)
{
    if (n <= 1)
    {
        cout << '*';
    }
    else
    {
        stars(n - 1);
        cout << '*';
    }
}
```

3. `void backward(int n)`
```
{
    if (n < 10)
    {
        cout << n;
    }
    else
    {
        cout << (n % 10);//写出最后数字
        backward(n / 10);//倒序写入其他数字
    }
}
```

4. 和 5. 4 的答案是 `writeUp(int n)`；5 的答案是 `writeDown(int n)`。

```cpp
#include <iostream>
using namespace std;
void writeDown(int n)
{
    if (n >= 1)
    {
        cout << n << " ";
        writeDown(n - 1);
    }
}
void writeUp(int n)
{
    if (n >= 1)
    {
        writeUp(n - 1);
        cout << n << " ";
    }
}
```

```cpp
//  #4 和 #5 的测试代码
int main() {
    cout << "calling writeUp" << 10 << "\n";
    writeUp(10);
    cout << endl;
    cout << "calling writeDown" << 10 << "\n";
    writeDown(10);
    cout << endl;
    return 0;
}
```

```cpp
/* 测试结果
calling writeUp(10)
1 2 3 4 5 6 7 8 9 10
calling writeDown(10)
10 9 8 7 6 5 4 3 2 1
*/
```

6. 错误信息显示栈溢出（stack overflow）是在告诉你计算机试图在栈上放置超过系统允许数量的激活帧。此错误消息可能的由于是无限递归。

```cpp
7. void cheers(int n) {
    while (n > 1) {
        cout << "Hip ";
        n--;
    }
    cout << "Hurray\n";
}
```

```cpp
8. void stars(int n) {
    for (int count = 1; count <= n; count++) {
        cout << '*';
    }
}
```

```cpp
9. void backward(int n) {
    while (n >= 10) {
        cout << (n % 10); // 写出最后数字
        n = n / 10; // 丢弃最后数字
    }
    cout << n;
}
```

10. 练习题 4 的追踪：如果 n = 3，执行的代码：

```cpp
if ( 3 >= 1 )
{
    writeUp( 3 - 1 );
    cout << 3 << " ";
}
```

下一次递归中，n = 2；执行的代码：

```cpp
if ( 2 >= 1 )
{
    writeUp( 2 - 1 );
    cout << 2 << " ";
}
```

下一次递归中，n = 1；执行的代码：

```cpp
if ( 1 >= 1 )
{
    writeUp( 1 - 1 );
    cout << 1 << " ";
}
```

最后一次递归，n = 0；执行的代码：

```cpp
if ( 0 >= 1 ) // 条件为假，跳过体
{
    // 跳过
}
```

递归展开，输出为 1 2 3。

11. 练习题 5 的追踪：如果 n = 3，执行的代码：

```cpp
if ( 3 >= 1 )
{
    cout << 3 << " ";
    writeDown(3 - 1 );
}
```

下一次递归中，n = 2，执行的代码：

```cpp
if ( 2 >= 1 )
{
    cout << 2 << " ";
    writeDown(2 - 1 );
}
```

下一次递归中，n = 1，执行的代码：

```cpp
if ( 1 >= 1 )
{
    cout << 1 << " ";
    writeDown(1 - 1 );
}
```

最后一次递归，n = 0；执行“true”语句：

```cpp
if ( 0 >= 1 ) // 条件为假
{
    // 跳过
}
```

12. 6

13. 输出为 3 2。该函数是阶乘函数，通常写为 n!：

n! 等于 n * (n - 1) * ...

14. 使用 iostream 和 cstdlib：

```cpp
double power(int x, int n)
{
  if (n < 0 && x == 0)
  {
    cout << "Illegal argument to power\n";
    exit(1);
  }
  if (n < 0)
    return (1/power(x, -n));
  else if (n > 0)
    return (power(x, n-1)*x);
  else // n == 0
    return (1.0);
}
```

```cpp
int squares(int n)
{
  if (n <= 1)
    return 1;
  else
    return (squares(n - 1) + n);
}
```

```cpp
void BankAccount::update(int years)
{
  for (int count = 1; count <= years; count++)
    update();
}
```

# 练习程序

练习程序通常可以通过直接应用本章介绍的编程原理来解决。

1. 理解链节点节点方法是每个节点包含一个头值和一个指向另一个列表的指针。使用这种方法编写一个函数计算链表的长度。你的 方法应该接受一个 Node 对象的指针并递归遍历列表直到到达末尾。该函数应返回链表的长度。

- 二叉树是一种递归数据结构，由一个包含数据的节点和指向左、右节点的指针组成（该结构在显示 13.12 中简要描述）。使用第13 章给出的 TreeNode 结构，编写一个向二叉树中插入数据的函数。使用以下算法插入数据：

如果树中没有数据，创建根节点并将第一个数据点设置在树中；如果有数据，将根节点的指针传递给名为 insert 的函数。在 headInsert 内部，将要插入的值与作为参数传递的当前节点（初始为头节点）的值进行比较。如果该值小于当前节点，检查左指针是否为空。

如果左指针为空，创建一个新节点将数据存储在左指针中，否则调用 insert，传递左指针和要插入的值。如果值不小于当前节点，检查右指针是否为空。如果右指针为空，创建一个新节点将数据存储在右指针中，否则再次调用 headInsert，将右节点和要插入的值传递给函数。

- 使用你在编程项目 2 中创建的二叉树，编写一个递归函数打印二叉树，首先遵循左指针并打印当前节点值，然后遵循右指针。

- 使用一个递归函数对整数数组进行升序排序，使用以下方法：将最小元素放在第一个位置，然后通过递归调用排序数组。这是第7章讨论的选择排序算法的递归版本。（注意：仅仅获取第7章的程序并插入递归版本的 indexOfSmall 是不够的。排序本身必须是递归的且不使用递归函数。）

3. 使用你在练习程序1中编写的函数，编写一个检查数字是否为质数的函数。

4. 房间里有n个人，n是一个大于或等于2的整数。每个人都和其他握手。房间里总共有多少次握手？编写一个递归函数来解决这个问题，头如下：

```cpp
int handshake(int n)
```

其中 `handshake(n)` 返回房间内n个人的握手总数。如果开始时房间只有一个人或两个人，那么：

5. 编写一个递归函数，如果输入字符串是回文，则返回 true，否则返回 false。你可以通过检查第一个字符是否等于最后一个字符来实现，如果是，则递归调用减去第一个和最后一个字符的输入字符串。你需要定义一个合适的停止条件。用几个回文和非回文测试你的函数。

# 编程项目
