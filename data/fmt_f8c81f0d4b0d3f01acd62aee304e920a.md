
`repositions the file-position pointer to the beginning of the file (location 0) attached to InClientFile`. The `seek` argument is an integer. A second argument can be specified to indicate the seek direction, which is `ios::beg` (the default) for positioning relative to the beginning of a stream, or `ios::cur` for positioning relative to the current position in a stream or `end`. The file-position pointer is an integer value that specifies the location in the file as a number of bytes from the starting location (this is also referred to as the offset from the beginning of the file). examples of positioning the get-position pointer are

```
// the nth byte of fileObject assumes ios::beg
fileObject.seekg(n);
// n bytes back in fileObject
fileObject.seekg(n, ios::cur);
// n bytes back from end of fileObject
fileObject.seekg(n, ios::end);
// at end of fileObject
fileObject.seekg(0, ios::end);
```

the operations can be performed using `ostream` member function `seekp`. member functions `tellg` and `tellp` are provided to return the current locations of the get and put pointers, the following statement assigns the file-position pointer to variable `location` of type:

```
location = fileObject.tellg();
```

## 14.4.4 Case Study: Credit Inquiry Program

Figure 14.6 enables a credit manager to manage the account information for those customers with zero balances (i.e., customers who do not owe the company money), credit (negative) balances (i.e., customers who owe the company money), and deposit (positive) balances (i.e., customers who owe the company money for goods and services received in the past). The program displays a menu and allows the credit manager to enter one of three options to obtain credit information. Option 1 produces a list of accounts with zero balances. Option 2 produces a list of accounts with debit balances. Option 4 terminates program execution. Entering an invalid option prompts the prompt to enter another. Lines 61–62 enable the program to read from the beginning of the file after end-of-file has been read.

```
// Fig. 14.6: Fig14_06.cpp
// Credit inquiry program.
#include <iostream>
```

Fig. 14.6 | Credit inquiry program. (Part I of 4)

# 第14章 文件处理

```
4 #include <fstream>
5 #include <iostream>
6 #include <string>
7 #include <cctype>
8 using namespace std;
10 enum class RequestType {
11 ZERO_BALANCE = 1, CREDIT_BALANCE, DEBIT_BALANCE, END};
12 RequestType getRequest();
13 bool shouldDisplay(RequestType, double);
14 void outline(int, const string&, double);
16 int main() {
17 // ifstream constructor opens the file
18 ifstream inClientFile("clients.txt", ios::in);
20 // exit program if ifstream could not open file
21 if (inClientFile)
22 cerr << "File could not be opened" << endl;
23 exit(EXIT_FAILURE);
25
26 // get user's request (e.g., zero, credit or debit balance)
27 RequestType request(getRequest());
29 // process user's request
30 while (request != RequestType::END) {
31 switch (request) {
32 case RequestType::ZERO_BALANCE:
33 cout << "\nAccounts with zero balances:\n";
34 break;
35 case RequestType::CREDIT_BALANCE:
36 cout << "\nAccounts with credit balances:\n";
37 break;
38 case RequestType::DEBIT_BALANCE:
39 cout << "\nAccounts with debit balances:\n";
40 break;
41 }
43 int account; // the account number
44 string name; // the account owner's name
45 double balance; // the account balance
47 // read account, name and balance from
48 inClientFile >> name >> balance;
50 // display file contents (until eof)
51 while (!inClientFile.eof()) {
52 // display record
53 if (shouldDisplay(request, balance)) {
54 outline(account, name, balance);
55 }
56 }
```

图 14.6 | 信用查询程序。 （第 2 部分，共 4 部分。）

## 14.4 从顺序文件中读取数据

```
// read account, name and balance from file
inClientFile >> account >> name >> balance;
}
```

```
inClientFile.clear(); // reset eof for next input
inClientFile.seekg(0); // reposition to beginning of file
request = getRequest(); // get additional request from user
out << "End of run." << endl;
```

```
// obtain request from user
RequestType getRequest() {
    cout << "\nEnter request\n"
    // 1 List accounts with zero balances\n
    // 2 List accounts with credit balances\n
    // 3 List accounts with debit balances\n
    // 4 End of run << fixed << showpoint;
    int type;
```

```
// input user request
do {
    cout << "?";
    cin >> type;
    while (type < static_cast<int>(RequestType::ZERO_BALANCE) ||
    type > static_cast<int>(RequestType::END));
return static_cast<RequestType>(type);
```

```
// determine whether to display given record
bool shouldDisplay(RequestType type, double balance) {
    if (type == RequestType::ZERO_BALANCE && balance == 0) {
    return true;
}
```

```
// determine whether to display credit balances
if (type == RequestType::CREDIT_BALANCE && balance < 0) {
    return true;
}
```

```
// determine whether to display debit balances
if (type == RequestType::DEBIT_BALANCE && balance > 0) {
    return true;
}
return false;
```

图 14.6 | 信用查询程序。 （第 3 部分，共 4 部分。）

## 666 第14章 文件处理

```
108 // display single record from file
109 void outline(int account, const string& name, double balance) {
110   cout << left << setw(10) << account << setw(13) << name
111   << setw(7) << setprecision(2) << right << balance << endl;
112 }
```

```
Enter request
1 - List accounts with zero balances
2 - List accounts with credit balances
3 - List accounts with debit balances
4 - End of run
? 1
Accounts with zero balances:
300   White       0.00
Enter request
1 - List accounts with zero balances
2 - List accounts with credit balances
3 - List accounts with debit balances
4 - End of run
? 2
Accounts with credit balances:
400   Stone       -42.16
Enter request
1 - List accounts with zero balances
2 - List accounts with credit balances
3 - List accounts with debit balances
4 - End of run
? 3
Accounts with debit balances:
100   Jones               24.98
200   Doe               345.67
500   Rich               224.64
Enter request
1 - List accounts with zero balances
2 - List accounts with credit balances
3 - List accounts with debit balances
4 - End of run
? 4
End of run.
```

图 14.6 | 信用查询程序。 （第 4 部分，共 4 部分。）

## 14.5 C++14：读写带引号的文本

许多文件包含带引号的文本，例如 `"C++ How to Program"`。例如，在表示 HTML5 页面的文件中，属性值用引号括起来。如果你正在构建一个用于显示此类网页内容的网络浏览器，你必须能够读取这些带引号的字符串并删除引号。

假设你需要从文本文件中读取数据，如图 14.5 所示，但每个账户的数据格式如下：

```
100 Janie Jones >> 24.98
```

请记住，流提取运算符 `>>` 将空白视为分隔符。因此，如果我们使用图 14.5 第 30 行中的表达式读取前面的数据

```
inClientFile >> account >> balance
```

第一个流提取将 `100` 读取到 `int` 变量 `account` 中，第二个读取仅 `"Janie` 到字符串变量 `name` 中（双引号将成为字符串的一部分）。第三个流提取在尝试读取 `double` 变量的值时失败，因为输入流中下一个标记（即数据片段）——`Jones—"` 不是一个 `double`。

### 读取带引号的文本

C++14 的新流操纵符——`quoted`（头文件 `<iostream>`）——使程序能够从流中读取带引号的文本，包括带引号文本中的任何空白字符，并丢弃引号定界符。如果，我们使用表达式读取带引号的数据

```
inClientFile >> account >> quoted(name) >> balance
```

第一个流提取将 `100` 读取到，第二个读取 `Janie Jones` 作为一个字符串并将其存储在 `name` 中，不带双引号定界符，第三个流提取将 `24.98` 读取到 `balance` 中。如果带引号的数据包含转义序列，则每个序列都会被读取并存储在流中作为转义序列 `"—`而不是作为 `"`。

### 写入带引号的文本

同样，你也可以向流写入带引号的文本。例如，如果 `name` 包含 `Janie Jones`，语句

```
outputStream << quoted(name);
```

将写入基于文本的 `outputStream`

```
"Janie Jones"
```

## 14.6 更新顺序文件

如第 14.3 节所示格式化和写入顺序文件的数据不能在不破坏文件中其他数据的风险下进行修改。例如，如果名称 `"White"` 需要更改为 `"Worthington"`，旧名称不能被覆盖-而不破坏文件。`white` 的记录被写入文件为

```
300 White 0.00
```

如果此记录使用较长的名称从文件中的同一位置重写，则记录将为

```
300 Worthington 0.00
```
