
```cpp
cout << accounts[i].name << ", " << accounts[i].id << ", " << accounts[i].balance << endl;
}
}

// 交换两个账户
void swap(Account& er1, Account& er2) {
    Account temp = er1;
    er1 = er2;
    er2 = temp;
}

// 将数据库升序排序
void sort(vector<Account>& db, bool (*comp)(const Account&, const Account&)) {
    size_t size = db.size();
    for (size_t i = 0; i < size - 1; i++) {
        size_t smallest = i;
        for (size_t j = i + 1; j < size; j++) {
            if (comp(db[j], db[smallest])) {
                smallest = j;
            }
        }
        if (smallest != i) {
            swap(db[i], db[smallest]);
        }
    }
}

// 按姓名排序
bool less_than_by_name(const Account& el1, const Account& er2) {
    return el1.name < er2.name;
}

// 按 ID 排序
bool less_than_by_id(const Account& el1, const Account& er2) {
    return el1.id < er2.id;
}

// 按余额排序
bool less_than_by_balance(const Account& el1, const Account& er2) {
    return el1.balance < er2.balance;
}

// 允许用户与银行账户数据库交互
int main() {
    // 银行账户数据库
    vector<Account> customers;
    // 用户命令
    char cmd;
    // 我们结束了吗？
    bool done = false;
    do {
        cout << " [A]dd [N]ame [I]D [B]alance [Q]uit => ";
        cin >> cmd;
        switch (cmd) {
            case 'A':
            case 'a':
                // 添加账户
                add_account(customers);
                break;
            case 'P':
            case 'p':
                // 打印数据库
                print_accounts(customers);
                break;
            case 'N':
            case 'n':
                // 按姓名排序
                sort(customers, less_than_by_name);
                print_accounts(customers);
                break;
            case 'I':
            case 'i':
                // 按 ID 排序
                sort(customers, less_than_by_id);
                print_accounts(customers);
                break;
            case 'B':
            case 'b':
                // 按余额排序
                sort(customers, less_than_by_balance);
                print_accounts(customers);
                break;
            case 'Q':
                done = true;
                break;
        }
    } while (!done);
    return 0;
}
```

此外，一个银行账户对象包含一个 `string` 对象作为字段。这表明对象可以包含其他对象，意味着对象可以具有任意复杂的结构。

列表 14.2 `bankaccount.cpp` 的示例运行输出

## 14.3. 方法

该程序允许用户使用比较函数以不同的方式对账户数据库进行排序。注意，`less_than_by_name` 和类似的比较函数使用了常量引用参数以提高效率（见 11.4）。

观察发现 `add_count` 函数有一个名为 `name` 的局部变量。所有的 `Account` 对象都有一个字段 `name`。`add_count` 函数在两种情况下使用 `name` 标识符都没有问题。编译器可以区分这两种标识符的使用，因为其中一个通过点 `.` 运算符限定了，而另一个没有。

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

* withdraw(acct, amt)
* 如果可能，则从账户 acct 中扣除金额。
* 如果成功则返回 true；否则返回 false。
* 如果取款会导致余额
* 降至零，则调用可能会失败。
* acct:一个银行账户对象
* amt: 要取出的资金
* 作者：Sam Coder
* 日期：2012年9月3日

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

* 糟糕的客户端代码
* ----------------
* 一个简单的银行客户数据库
`vector<Account> accountDB;`

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

## 14.3. 方法

```cpp
* deposit (amt)
* 将金额 amt 添加到账户余额中。
*
* 作者: Sam Coder
* 日期: 2012年9月3日
****************************************************************/
void deposit(double amt) {
    balance += amt;
}
```

```cpp
****************************************************************/
* withdraw (amt)
* 从账户余额中扣除金额 amt，
* 如果可能的话。
* 如果成功则返回 true；否则返回 false。
* 如果取款会导致
* 余额降至零以下，则该调用可能会失败。
*
* amt: 要取出的资金
*
* 作者: Sam Coder
* 日期: 2012年9月3日
****************************************************************/
bool withdraw(double amt) {
    bool result = false; // 默认失败
    if (balance - amt >= 0) {
        balance -= amt;
        result = true; // 成功
    }
    return result;
}
```

在 `Account` 类的这个新定义中，命名为 `deposit` 和 `withdraw` 的成员并不是字段；它们是方法定义。方法定义看起来像函数定义，但它出现在类定义内部。由于由于，方法也被称为成员函数。

客户端通过点 `.` 运算符访问方法：

```cpp
// 从名为 acct 的 Account 对象中取钱
acct.withdraw(100.0);
```

方法定义使用了三个变量：`amt`、`result` 和 `balance`。变量 `amt` 和 `result` 是 `withdraw-amt` 方法的局部变量，而 `balance` 在 `withdraw` 的体内部声明。`balance` 在哪里声明的呢？它是在类私有 `private` 部分声明的字段。`withdraw` 方法会影响被调用的对象的 `balance` 字段：

```cpp
// 影响 acct1 对象的 balance 字段
acct1.withdraw(100.0);
// 影响 acct2 对象的 balance 字段
acct2.withdraw(25.0);
```

方法可以像全局函数一样重载（见第 10.3 ）。这意味着同一类中的多个方法可以有相同的名称，但它们的签名必须不同。记住，函数的签名由名称和参数类型组成；方法的签名由其名称和参数类型组成。

我们在第 14.2 节中看到每个对象都为其自己的数据字段提供了存储。对象不需要为它的方法分配任何空间。这意味着执行程序必须管理的关于对象的唯一内容就是对象的字段。操作系统之间内存的精确组织图 F.10 显示了典型的布局。程序处理的所有数据都出现在三个部分之一：栈 `stack`、堆 `heap` 或静态 `static`。对于像 `int` 等简单数据类型，声明为函数局部的对象字段位于被称为栈的内存段中。同样像简单数据类型，用 `new` 分配的对象的字段出现在堆上。全局和静态对象中的字段位于执行程序内存的静态部分。

考虑以下简单类：

```cpp
class Counter {
    int count;
    public:
        // 允许将计数器重置为零
        void clear() {
            count = 0;
        }
        // 允许增加计数器
        void inc() {
            count++;
```
