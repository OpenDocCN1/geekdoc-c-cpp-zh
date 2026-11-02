

![](img/d0d3b7423c2d9e5650be79209ea1885d_479_0.png)

**图 11.4** | FILE 指针、FILE 结构与 FCB 之间的关系。

### 11.3.6 文件打开模式

文件可以以多种模式之一打开，这些模式总结在图 11.5 中。表中前半部分每个文件打开模式都有一个对应的 *二进制* 模式（包含字母 b）用于操作二进制文件。二进制模式在第 11.5–11.9 节中使用，我们在其中介绍随机访问文件。

| 模式 | 描述 |
|---|---|
| `r` | 打开现有文件进行读取。 |
| `w` | 创建文件用于写入。如果文件已存在，则丢弃当前内容。 |
| `a` | 打开或创建文件以在文件末尾写入——即写入操作将数据追加到文件。 |
| `r+` | 打开现有文件进行更新（读取和写入）。 |
| `w+` | 创建文件用于读取和写入。如果文件已存在，则丢弃当前内容。 |
| `a+` | 打开或创建文件用于读取和更新；所有写入都在文件末尾进行——即写入操作将数据追加到文件。 |
| `rb` | 以二进制模式打开现有文件进行读取。 |
| `wb` | 以二进制模式创建文件用于写入。如果文件已存在，则丢弃当前内容。 |
| `ab` | 追加：以二进制模式打开或创建文件以在文件末尾写入。 |
| `rb+` | 以二进制模式打开现有文件进行更新（读取和写入）。 |
| `wb+` | 以二进制模式创建文件用于更新。如果文件已存在，则丢弃当前内容。 |
| `ab+` | 以二进制模式打开或创建文件用于更新；写入在文件末尾进行。 |

**图 11.5**  文件打开模式。

#### C11 排他写入模式

此外，C11 提供了排他写入模式，你可以通过在 w、w+ 或 wb+ 模式末尾添加 x 来指示。在排他写入模式下，如果文件已存在或无法创建，`fopen` 将失败。如果以排他写入模式成功打开文件并且底层系统支持排他文件访问，则只有你的程序在文件打开期间可以访问该文件。（某些编译器和平台不支持排他写入模式。）如果在任何模式下打开文件时发生错误，`fopen` 返回 `NULL`。

> **常见编程错误 11.3**
>
> *打开不存在的文件进行读取是错误。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_480_0.png)

> **常见编程错误 11.4**
>
> *在未获得文件适当访问权限的情况下打开文件进行读取或写入（这取决于操作系统）是错误。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_480_1.png)

> **常见编程错误 11.5**
>
> *在没有可用空间时打开文件进行写入是运行时错误。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_480_2.png)

> **常见编程错误 11.6**
>
> 在应以更新模式（`"r+"`）打开文件时以写入模式（`"w"`）打开文件会导致文件内容被丢弃。

> **错误预防提示 11.1**
>
> 仅当文件内容不应被修改时才以仅读取（而非更新）的方式打开文件。这可以防止文件内容被无意修改。这是最小权限原则的另一个例子。

## 11.4 从顺序访问文件读取数据

数据存储在文件中，以便在需要时检索进行处理。前一节演示了如何创建顺序访问文件。本节介绍如何从文件中顺序读取数据。

图 11.6 从图 11.2 程序创建的 "clients.txt" 文件中读取记录并打印其内容。第 7 行指出 cfPtr 是一个 *指向 FILE 的指针*。第 10 行尝试以读取模式（`"r"`）打开文件 "clients.txt"，并确定是否成功打开（即 `fopen` 不返回 `NULL`）。第 19 行从文件中读取一条“记录”。函数 `fscanf` 等同于函数 `scanf`，区别在于 `fscanf` 接收一个文件指针作为参数，用于从中读取数据的。执行此语句第一次后，account 将具有值 100，name 将具有值 "Jones"，balance 将具有值 24.98。每次执行第二个 `fscanf` 语句（第 24 行）时，程序都会从文件中读取另一条记录，account、name 和 balance 取得新值。当程序到达文件末尾时，文件被关闭（第 27 行）并且程序终止。函数 `feof` 仅在程序尝试读取最后一行之后不存在的数据时才返回 true。

```c
// Fig. 11.6: fig11_06.c
// Reading and printing a sequential file
#include <stdio.h>

int main(void)
{
    FILE *cfPtr; // cfPtr = clients.txt file pointer

    // fopen opens file; exits program if file cannot be opened
    if ((cfPtr = fopen("clients.txt", "r")) == NULL) {
        puts("File could not be opened");
    }
    else { // read account, name and balance from file
        unsigned int account; // account number
        char name[30]; // account name
        double balance; // account balance

        printf("%-10s%-13s%s\n", "Account", "Name", "Balance");
        fscanf(cfPtr, "%d%29s%lf", &account, name, &balance);

        // while not end of file
        while (!feof(cfPtr)) {
            printf("%-10d%-13s%7.2f\n", account, name, balance);
            fscanf(cfPtr, "%d%29s%lf", &account, name, &balance);
        }

        fclose(cfPtr); // fclose closes the file
    }
}
```

**图 11.6** | 读取并打印顺序文件。

| 账户 | 姓名 | 余额 |
|---|---|---|
| 100 | Jones | 24.98 |
| 200 | Doe | 345.67 |
| 300 | White | 0.00 |
| 400 | Stone | -42.16 |
| 500 | Rich | 224.62 |

### 11.4.1 重置文件位置指针

为了从文件中顺序检索数据，程序通常从文件开头开始读取，并连续读取所有数据直到找到所需数据。在程序执行期间，可能需要多次（从文件开头开始）顺序处理文件中的数据。语句

`rewind(cfPtr);`

会导致程序的文件位置指针——指示文件中下一次要读取或写入的字节数——重新定位到由 cfPtr 指向的文件开头（即字节 0）。文件位置指针并不是真正的指针，而是一个整数值，指定下一次读或写要在文件中发生的字节。这有时被称为文件偏移。文件位置指针是与每个文件关联的 FILE 结构的一个成员。

### 11.4.2 信用查询程序

图 11.7 的程序允许信用经理获取零余额客户的名单（即不欠任何钱的客户）、信用余额客户的名单（即公司欠钱的客户）以及借方余额客户的名单（即欠公司商品和服务款项的客户）。信用余额为负数；借方余额为正数。

程序显示一个菜单并允许信用经理输入四个选项之一：

- 选项 1 生成零余额账户的列表。
- 选项 2 生成信用余额账户的列表。
- 选项 3 生成借方余额账户的列表。
- 选项 4 终止程序执行。

示例输出显示在图 11.8 中。

```c
// Fig. 11.7: fig11_07.c
// Credit inquiry program
#include <stdio.h>

// function main begins program execution
int main(void)
{
    FILE *cfPtr; // clients.txt file pointer

    // fopen opens the file; exits program if file cannot be opened
    if ((cfPtr = fopen("clients.txt", "r")) == NULL) {
        puts("File could not be opened");
    }
    else {

        // display request options
        printf("%s", "Enter request\n"
            " 1 - List accounts with zero balances\n"
            " 2 - List accounts with credit balances\n"
            " 3 - List accounts with debit balances\n"
            " 4 - End run\n");
        unsigned int request; // request number
        scanf("%u", &request);

        // process user's request
        while (request != 4) {
            unsigned int account; // account number
            double balance; // account balance
            char name[30]; // account name

            // read account, name and balance from file
            fscanf(cfPtr, "%d%29s%lf", &account, name, &balance);

            switch (request) {
                case 1:
                    puts("\nAccounts with zero balances:");

                    // read file contents (until eof)
                    while (!feof(cfPtr)) {
                        // output only if balance is 0
                        if (balance == 0) {
                            printf("%-10d%-13s%7.2f\n",
                                account, name, balance);
                        }

                        // read account, name and balance from file
                        fscanf(cfPtr, "%d%29s%lf",
                            &account, name, &balance);
                    }
                    break;
```

**图 11.7** | 信用查询程序。（第 1 部分，共 2 部分。）

