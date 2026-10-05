

## 14.3. 方法

该程序允许用户使用比较函数以不同的方式对账户数据库进行排序。注意，`less_than_by_name` 和类似的比较函数使用了常量引用参数以提高效率（见 11.4）。

观察发现 `add_count` 函数有一个名为 `name` 的局部变量。所有的 `Account` 对象都有一个字段 `name`。`add_count` 函数在两种情况下使用 `name` 标识符都没有问题。编译器可以区分这两种标识符的使用，因为其中一个通过点 (.) 运算符限定了，而另一个没有。

## 14.3 方法

到目前为止看到的对象都是没有内置功能的被动实体。除了为对象定义数据结构外，类还可以定义代表对象操作的函数。

回想第 14.2 节中的账户类 `Account`：

```cpp
class Account {
```

©2014 Richard L. Halterman 草稿日期：2014年1月26日

## 14.3. 方法

```cpp
class Account {
public:
    // 表示账户持有人名称的字符串
    string name;
    // 账户号码
    int id;
    // 当前账户余额
    double balance;
```

假设将此设计交给了程序员 Sam，他编写了一个 `withdraw` 函数。Sam 是一个严谨的程序员，所以他的 `withdraw` 函数会检查透支：

- ********************************************************************
* withdraw(acct, amt)
* 如果可能，则从账户 acct 中扣除金额。
* 如果成功则返回 true；否则返回 false。
* 如果取款会导致余额
* 降至零，则调用可能会失败。
* acct:一个银行账户对象
* amt: 要取出的资金

* 作者：Sam Coder
* 日期：2012年9月3日
********************************************************************/

```cpp
bool withdraw(Account acct, double amt) {
  bool result = false; // 默认失败
  if (acct.balance - amt >= 0) {
    acct.balance -= amt;
    result = true; // 成功
  }
  return result;
}
```

以下代码片段显示了从银行取款时预期的客户端代码：

```cpp
// 良好的客户端代码
// ----------------
// 一个简单的银行客户数据库
vector<Account> accountDB;

// 通过某些函数填充数据库
accountDB = initialize_db();

// 获取交易信息
int number;
double debit;
cout << "请输入账户号码和取款金额：";
cin >> number >> debit;

// 定位账户索引
int n = accountDB.size(), i = 0;
while (i < n) {
    if (accountDB[i].id == number)
        break; // 找到账户
    i++;
}
```

```cpp
// 如果可能，执行交易
if (i < n) {
    if (withdraw(accountDB[i], debit))
        cout << "取款成功" << endl;
    else
        cout << "无法执行取款" << endl;
}
else
    cout << "账户不存在" << endl;
```

遗憾的是，没有什么能阻止客户端表现粗率：

- - 糟糕的客户端代码
- ----------------
- 一个简单的银行客户数据库
vector<Account> accountDB;

```cpp
// 通过某些函数填充数据库
accountDB = initialize_db();
```

```cpp
// 获取交易信息
int number;
double debit;
cout << "请输入账户号码和取款金额：":
cin >> number >> debit;
```

```cpp
// 定位账户索引
int n = accountDB.size(), i = 0;
while (i < n) {
    if (accountDB[i].id == number)
        break; // 找到账户
    i++;
}
```

```cpp
// 执行交易
if (i < n)
    accountDB[i] -= debit; // 如果 debit 太大了怎么办？
else
    cout << "账户不存在" << endl;
```

`Account` 对象本身中的没有任何东西可以防止透支，或防止客户端操纵 `Account` 对象的余额。

我们需要能够保护银行账户对象的内部细节，同时允许客户端以定义良好且受控的方式与它们交互。

考虑一个非编程的例子。如果我向银行存入 1,000.00 美元，银行就拥有我的钱。这仍然是我的钱，所以理论上我随时可以取回它。银行把钱存在保险箱里，我的钱也在保险箱里。假设我想从账户中取出 100 美元。由于我的账户中总共有 1,000 美元，该交易应该没有问题。以下场景有什么问题：

1. 进入银行。
2. 经过柜员进入一个可以进入保险箱的房间。
3. 保险箱门开着，进入保险箱并从一叠20美元的钞票中取出100美元。
4. 离开保险箱并告诉柜员你从账户中取了100美元。
5. 离开银行。

这不是处理取款的正常银行用法。在一个每个人诚实且会犯错误的完美世界上，一切良好。在现实中，许多客户可能不诚实，并故意取出比他们需要的钱。即使我忠实地数出了我的资金，钱包中的某些钞票也可能粘在一起，而我犯了一个诚实的错误，拿了一张20美元的钞票而不是五张。如果我把钞票放入已经有钱的钱包里，我可能永远无法发现这个错误。

到目前为止看到的对象都是没有内置功能的被动实体。除了为对象定义数据结构外，类还可以定义代表对象操作的函数。

回想第 14.2 节中的账户类 `Account`：

```cpp
class Account {
public:
    // 表示账户持有人名称的字符串
    string name;
    // 账户号码
    int id;
    // 当前账户余额
    double balance;
```

我们如何保护银行账户对象的内部细节，并允许客户端以定义良好且受控的方式与它们交互呢？诀窍在于完全隐藏对象的字段，并提供特殊的函数，称为“方法”，这些方法可以访问隐藏的字段。在以下修改后的 `Account` 中：

```cpp
class Account {
    // 表示账户持有人名称的字符串
    string name;
    // 账户号码
    int id;
    // 当前账户余额
    double balance;
public:
    // 方法将添加到这里
```

所有的字段都不再位于类的公共部分。这使得以下客户端代码变得不可能：

```cpp
Account acct;
// 设置账户余额
acct.balance = 100; // 非法
// 取出资金
acct.balance -= 20; // 非法
```

`balance` 字段位于类的私有区域。你可以使用 literal `private` 标签，如下：

```cpp
class Account {
private:
    // 表示账户持有人名称的字符串
    string name;
    // 账户号码
    int id;
    // 当前账户余额
    double balance;
public:
    // 方法将添加到这里
};
```

由于类中任何未标记的字段都是隐含私有的，因此 `private` 标签并不总是必要的，但程序员喜欢在类定义中将公共成员放在私有成员之前，如下：

```cpp
class Account {
public:
    // 方法将添加到这里
private:
    // 表示账户持有人名称的字符串
    string name;
    // 账户号码
    int id;
    // 当前账户余额
    double balance;
};
```

