
（续）

```cpp
// 确定文件是否打开
if (inFile.is_open())
{
    // 读取商店 1 的销售额
    inFile >> store1Sales;
    inFile.ignore();

    while (!inFile.eof())
    {
        // 读取商店 2 的销售额
        inFile >> store2Sales;
        inFile.ignore();

        // 累加每个商店的销售额
        storeTotal += store1Sales;
        storeTotal += store2Sales;

        // 读取商店 1 的销售额
        inFile >> store1Sales;
        inFile.ignore();
    } // 文件结束
    // 关闭文件
    inFile.close();

    // 显示每个商店的总销售额
    cout << "商店 1 总销售额: " << storeTotal << endl;
    cout << "商店 2 总销售额: " << storeTotal << endl;
}
else
    cout << "无法打开文件。" << endl;
// if 结束
system("pause");
return 0;
} // main 函数结束
```

图 14-22 练习 14 的代码

![](img/d64a28a6849d61137bf2f3170ac40ad_633_0.png)

图 14-23 顺序访问文件 Lab14.txt 内容

# 第 14 章

 顺序访问文件

# 14-5 练习

按照启动 C++ 和打开 Lab14-5.cpp 文件的说明进行操作。调试程序。

# 总结

- 顺序访问文件可以是输入文件或输出文件。输入文件是程序读取的文件；输出文件是程序写入数据的文件。

- 为了在程序中创建文件对象，程序必须包含 `#include <fstream>` 指令。

- 使用 `ifstream` 和 `ofstream` 类（定义在 `fstream` 文件中）分别创建输入和输出对象。文件对象用于表示存储计算机磁盘上的实际文件。

- 创建文件对象后，使用 `open` 函数打开输入或输出文件。

- 你可以使用 `is_open` 函数来确定 `open` 函数是否成功。如果打开操作成功，返回布尔值 `true`；否则返回 `false`。

- 为了在顺序访问文件中区分一条记录和另一个记录，程序员通常会在写入记录的语句末尾另起一行。这是通过包含 `endl` 操纵符实现的如果记录包含多个字段，则使用字符（如 `'#'`）来分隔不同字段的数据。

- 从文件中读取数据时，使用 `eof` 函数确定指针是否到达文件末尾。如果文件指针位于文件的最后一个字符之后，`eof` 函数返回布尔值 `true`；否则返回 `false`。

- 当程序完成文件后，应该使用 `close` 函数将其关闭。未关闭打开的文件会导致数据丢失。

# 术语

- `!` 逻辑运算符

- `close` 函数：在程序中关闭顺序访问文件。

- `eof` 函数：确定整个文件是否已读取；当文件指针位于顺序访问文件的最后一个字符之后时，返回 `true`；否则返回 `false`。

- 字段（Field）：关于人、地点或事物的单条信息。

- 输入文件：程序作为输入的文件。

- `is_open` 函数：在程序中确定顺序访问文件是否成功打开；如果打开成功，返回 `true`；否则返回 `false`。

- 非逻辑运算符：反转条件的真值。

- `open` 函数：用于在程序中打开输入和输出文件。

- 输出文件：存储程序产生的输出的文件。

- 记录（Record）：一个或多个相关字段的集合，包含关于人、地点或事物的所有数据。

- 顺序访问文件：由文本行组成的文件；也称为文本文件。

- 文本文件：顺序访问文件的另一种名称。

# 复习题

1. `______` 是关于人或事物的单条信息。
   a 字段
   b 文件
   c 记录
   d 以上都不是

2. 特定特定、地点或事物的所有数据的相关字段组被称为 `______`
   a 字段
   b 文件
   c 记录
   d 以上都不是

3. 程序为了创建文件对象，必须包含 `______` 文件。
   a ifstream
   b ifstream
   c outFile
   d sequential

5. 下列哪条语句创建名为 `outPayroll` 的代表程序中输出文件的对象？
   a `fstream outPayroll;`
   b `ofstream outPayroll;`
   c `outPayroll as ofstream;`
   d `outPayroll as outstream;`

6. 下列哪条语句为输出打开 `payroll.txt` 文件？该文件与 `outPayroll` 对象关联。
   a `outPayroll.open("payroll.txt");`
   b `outPayroll.open("payroll.txt", ios::out);`
   c `outPayroll.open("payroll.txt", ios::output);`
   d a 和 b

7. 要向现有输出文件的末尾添加记录，你使用 `open` 函数中的模式。
   a add
   b `ios::add`
   c `ios::app`
   d `ios::out`

8. 你使用 `________` 来关闭顺序访问文件。
   a close
   b end
   c exit
   d finish

9. 你可以使用 `______` 来确定 `open` 函数是否成功。
   a is_open
   b isopen
   c isOpen
   d isOpen

10. 下列哪条语句将每个商店的总销售额写入输出文件？该文件与 `outFile` 对象关联。
    a `cout << "商店 1 总销售额: " << storeTotal << endl;`
    b `cout << "商店 2 总销售额: " << storeTotal << endl;`
    c `outFile << "商店 1 总销售额: " << storeTotal << endl;`
    d `outFile << "商店 2 总销售额: " << storeTotal << endl;`

11. 下列哪条语句从输入文件 `managers.txt` 读取数字？该文件与 `inFile` 对象关联。
    a `inFile >> salary;`
    b `ifstream << salary;`
    c `inFile << salary;`
    d 以上都不是

12. 下列哪条语句将 `state` 变量写入输出文件 `address.txt`？该文件与 `outFile` 对象关联。
    a `address.txt << state << endl;`
    b `ofstream << state << endl;`
    c `outFile << state << endl;`
    d `outfile << state << endl;`

13. 下列哪条语句使用循环直到文件末尾？该文件与 `inFile` 对象关联。
    a `while (inFile.eof())`
    b `while (!ifstream.eof())`
    c `while (!inFile.eof())`
    d `while (!ifstream.fail())`

14. 下列哪条语句创建一个名为 `inPayroll` 的代表程序中输入文件的对象？
    a `instream inPayroll;`
    b `ifstream inPayroll;`
    c `inPayroll as ifstream;`
    d `inPayroll as ifstream;`

15. 下列哪条语句为输入打开 `payroll.txt` 文件？该文件与 `inFile` 对象关联。
    a `inFile.open("payroll.txt", ios::app);`
    b `inFile.open("payroll.txt");`
    c `inFile.open("payroll.txt", ios::in);`
    d 都 b 和 c

# 练习

![](img/d64a28a6849d61137bf2f3170ac40ad_633_0.png)

# 笔算

1. 写一条语句声明名为 `inSales` 的输入文件。（复习题答案位于章节末尾。）

2. 写一条语句打开一个顺序访问文件 `jans.txt` 用于输出。该文件与 `outJan` 对象关联。（复习题答案位于章节末尾。）

3. 重写笔算练习 2 中的语句，使其以追加模式打开 `jans.txt`。

4. 写一条语句打开一个名为 `inventory.txt` 的顺序访问文件用于输入。该文件与 `inInventory` 对象关联。

5. 写一条语句打开一个顺序访问文件 `firstQtr.txt` 用于追加。该文件与 `outSales` 对象关联。

6. 写一条语句打开一个顺序访问文件 `febales.txt` 用于输出。该文件与 `outFeb` 对象关联。

7. 写一个 `if` 子句来确定输出文件是否成功打开。

8. 写一条语句从与 `inFile` 对象关联的顺序文件中读取一个字符串。将字符串赋值给 `textLine` 变量。

9. 写一条语句从与 `inFile` 对象关联的顺序文件中读取一个数字。将数字赋值给 `number` 变量。

10. 写一条语句关闭与 `outFile` 对象关联的 `jans.txt` 文件。

11. 程序需要向与 `outFile` 对象关联的顺序访问文件中写入字符串 "Employee" 和字符串 "Name"。每个字符串应出现在文件的单独行。编写代码完成此任务。

