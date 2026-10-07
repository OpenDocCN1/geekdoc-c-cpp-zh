
```c
else {
    rewind(readPtr); // 将指针置到文件开头
    fprintf(writePtr, "%-6s%%-6s%%-11s%%-10s\n", "Acct", "Last Name", "First Name", "Balance");

    // 将随机访问文件中的所有记录复制到文本文件
    while (!feof(readPtr)) {
        struct clientData client = {0, "", "", 0.0};
        size_t size = fread(&client, sizeof(struct clientData), 1, readPtr);
        // 将记录写入文本文件
        if (result != 0 && client.account != 0) {
            fprintf(writePtr, "%-6s%%-6s%%-11s%%-10.2f\n", client.account, client.firstName, client.balance);
        }
    }
    fclose(writePtr); // 关闭文件
}

// 更新记录中的余额
void updateRecord(FILE *fPtr) {
    // 获取要更新的账户
    printf("%s", "输入要更新的账户 (1 - 100):\n");
    int account = 0; // 账户号码
    scanf("%d", &account);

    // 将文件指针移动到文件中正确的记录
    fseek(fPtr, (account-1) * sizeof(struct clientData), SEEK_SET);
    // 从文件中读取记录
    struct clientData client = {0, "", "", 0.0};
    fread(&client, sizeof(struct clientData), 1, fPtr);
    if (client.account == 0) {
        printf("账户 #%d 无信息.\n", account);
    } else { // 更新记录
        printf("%-6s%%-6s%%-11s%%-10.2f\n", client.account, client.firstName, client.balance);

        // 向用户请求事务金额
        printf("%s", "输入费用 (+) 或还款 (-):\n");
        double transaction = 0.0; // 事务金额
        scanf("%lf", &transaction);
        client.balance += transaction; // 更新记录余额
    }
```

图 11.7 — 事务处理程序。（5 部分第 3 部分）

```c
printf("%-6s%%-6s%%-11s%%-10.2f\n", client.account, client.firstName, client.balance);
```

```c
printf("%-6s%%-6s%%-11s%%-10.2f\n", client.account, client.firstName, client.balance);
```

```c
// 将文件指针移动到文件中正确的记录
fseek(fPtr, (account-1) * sizeof(struct clientData), SEEK_SET);
```

```c
// 在文件中写入记录
write(client, sizeof(clientData), 1);
```

```c
// 创建记录
void newRecord(FILE *fPtr) {
    // 获取要创建的账户
    printf("%s", "输入账户号码 (1 - 100):\n");
    int account = 0; // 账户号码
    scanf("%d", &account);
```

```c
// 将文件指针移动到文件中正确的记录
fseek(fPtr, (account-1) * sizeof(struct clientData), SEEK_SET);
```

```c
// 从文件中读取记录
struct clientData client = {0, "", "", 0.0};
```

```c
read(client, sizeof(clientData), 1, fPtr);
```

```c
// 如果记录已包含信息
if (client.account != 0) {
    printf("记录已包含信息\n");
}
```

```c
// 输入姓、名、余额
printf("%s", "输入姓、名、余额");
```

```c
// 在文件中写入记录
write(client, sizeof(clientData), 1);
```

```c
// 删除现有记录
void deleteRecord(FILE *fptr) {
    // 获取要删除的账户
    printf("%s", "输入要删除的账户 (1 - 100):\n");
    int account = 0; // 账户号码
    scanf("%d", &account);
```

```c
// 将文件指针移动到文件中正确的记录
fseek(fptr, (account-1) * sizeof(struct clientData), SEEK_SET);
```

```c
// 从文件中读取记录
struct clientData client = {0, "", "", 0.0};
```

```c
read(client, sizeof(clientData), 1, fptr);
```

```c
// 如果账户不存在
if (client.account == 0) {
    printf("%d 不存在\n", client.account);
}
```

```c
// 将文件指针移动到文件中正确的记录
fseek(fptr, (account-1) * sizeof(struct clientData), SEEK_SET);
```

```c
struct clientData blankClient = {0, "", "", 0}; // 空记录
// 用空记录替换现有记录
fwrite(&blankClient, sizeof(struct clientData), 1, fptr);
```

```c
// 允许用户输入菜单
int enterChoice(void) {
    // 显示可用选项
    printf("\输入你的选择\n")
        "1 - 存储名为 accounts 的格式化文本文件\n"
        "2 - 更新账户\n"
        "3 - 添加新账户\n"
        "4 - 删除账户\n"
        "5 - 结束程序\n");
```

```c
int menuChoice = 0; // 存储用户的变量
scanf("%d", &menuChoice); // 用户的选择
return menuChoice;
}
```

图 11.7 | 事务处理程序。（5 部分第 5 部分。）

# 相关练习

此事务处理系统案例由练习 11.11（硬件库存）和练习 11.17（修改后的事务处理系统）支持。

## 自测

（讨论）在以下代码中，`if` 语句的条件测试了什么？

```
if ((cffptr = fopen("accounts.dat", "rb+")) == NULL)
```

答案：该条件测试了文件 `accounts.dat` 是否已以二进制读写模式成功打开。

620 文件处理

（讨论）在图 11.7 的程序中，以下语句的作用是什么？

`fseek(fPtr, (account - 1) * sizeof(struct clientData), SEEK_SET);`

答案：该语句将 `fPtr` 所代表的文件指针位置移动到 `clientData` 结构体第 `account` 条记录所在的位置。

## 11.10 安全 C 语言编程

### _s 和 scanf_s

11.3–11.4 节示例使用了 `printf` 和 `scanf` 函数分别向文件写入文本和从文件中读取。C 标准的附录 K 提供了这些版本，名为 `printf_s` 和 `scanf_s`，它们与我们之前介绍的 `printf_s` 和 `scanf_s` 函数相同，不同之处在于还需要指定一个 `FILE` 指针参数，用以指示要操作的文件。如果你的编译器的标准库包含这些函数，你应该使用它们代替 `printf`。与 `scanf_s` 和 `printf_s` 不同，微软版本的 `printf_s` 和 `scanf_s` 与附录 K 中的不同。

## SEI CERT C 编码标准第 9 章

SEI CERT C 编码标准第 9 章专门介绍输入输出命令和规则——许多规则适用于通用文件处理，其中若干条适用于本章介绍的文件处理函数。有关每个条目的的更多信息，请访问 `https://wiki.sei.cmu.edu/`

- FIO03-C. 使用本章中的非独占文件打开模式以写模式打开文件时，如果文件存在，`opens` 函数将打开它并截断其内容，且不指示在调用打开之前文件是否存在。为了确保现有文件不被打开并截断，你可以使用 C11 的独占写模式（在第 11.3 节中讨论），它允许在文件不存在时打开文件。

- FIO04-C. 在工业级代码中，你应该始终检查返回错误指示的文件处理函数的返回值，以确保这些函数已完成其任务。

- FIO07-C. `rewind` 函数不返回值，因此你无法测试操作是否成功。建议改用 `fseek` 函数，因为它在失败时会返回非零值。

- FIO09-C. 我们在本章中演示了文本文件和二进制文件。由于不同平台之间二进制数据表示的差异，以二进制格式写入的文件通常是不可移植的。为了更具移植性的文件表示，请考虑使用文本文件或能够处理平台间二进制文件表示的函数库。

- FIO14-C. 某些函数在文本文件和二进制文件上的操作并不相同。特别是，如果从 `SEEK_END` 寻址，不能保证 `fseek` 函数在二进制文件上正常工作，因此应该使用 `SEEK_SET`。

- FIO42-C. 在平台上，你同时打开的文件数量是有限的。因此，一旦你的程序不再需要某个文件，就应该立即关闭它。

## 自测

**（填空题）** 当你以写模式打开一个文件时，你可以使用______ 来确保现有文件不被截断，这允许 `fopen` 在文件不存在时打开它。

**答案：** 独占写模式。

**2（真/假）** `rewind` 函数不返回值，因此你无法测试操作是否成功。相反，请使用 `fseek`，因为它在失败时会返回一个非零值。

**答案：** *真。*

**3（真/假）** 许多平台允许同时打开的文件数量有限，因此一旦不再需要某个文件，就应该立即关闭它。

**答案：** *真。*

## 总结

## 第 11.1 节介绍

- 文件（第 594 页）用于永久保留大量数据。

- 将文件存储在次级存储设备上，如固态硬盘、闪存器和硬盘。

## 第 11.2 节 文件与流

- 我们将每个文件视为一个字节流（p. 594）。打开文件时，会自动关联一个流。

- 三种流是：标准输入（`stdin`）、标准输出（`stdout`）和标准错误（`stderr`）。

- 流提供了文件与程序之间的通信通道。

- 标准输入流允许从键盘读取数据，标准输出流允许在屏幕上打印。

- 打开文件时会关联一个 `FILE` 结构（p. 595）。该结构（FCB）被操作系统用于访问文件。

- 文件指针（p. 595）指定了文件中下一次读取或写入的字节位置。

- 顺序文件包含一个 `FILE` 结构。

- `fgets`（p. 595）从文件中读取一行。

- `fput`（p. 595）向文件中写入字符。

- `fgets` 和 `fputs` 分别从文件中读取一行或向文件中写入一行。

## 第 11.3 节 创建顺序文件

- 每个随机访问文件使用 `FILE` 结构。

- 每个随机访问文件必须具有一个 `FILE` 结构。

- `fopen`（p. 597）接收文件名和打开模式并返回一个 `FILE` 结构指针，失败则返回 `NULL`。

- 如果文件不存在，`fopen` 会创建它；如果文件存在，内容会被截断。

- `feof`（p. 598）在文件结束指示设置时返回非零值（真）；否则返回零。

- `fprintf`（p. 598）接收指向写入数据的文件的指针。

- `fclose`（p. 598）接收文件作为参数并关闭文件。打开文件时，控制块（FCB）会被复制到内存中。

- 为了读取现有文件，使用读取模式（"r"）。

- 为了在现有文件末尾添加记录，使用追加模式（"a"）。

- 为了读写打开文件，使用更新模式——r+"、w+" 或 "a+"。"r+" 以读写打开文件，但现有内容会被截断。"a+" 以读写打开文件，所有写入都在文件末尾进行。如果文件不存在，它会创建文件。

- 每个文件模式都有对应的二进制模式（b）。

- 独占写模式确保文件不被覆盖。如果你的程序成功以独占写模式打开文件且底层系统支持文件访问，那么程序就可以访问该文件。

## 第 11.4 节 从顺序文件访问数据

- `fscanf`（p. 601）等同于 `scanf` 函数，但接收指向读取数据的文件的指针。

- `rewind`（p. 602）将程序的句指针置于文件的开头（即设置为 0）。

- 顺序文件的数据通常无法在不破坏文件中其他数据的情况下进行修改。

## 第 11.5 节 随机访问文件

- 随机访问文件（p. 606）使用固定长度记录，无需遍历其他记录即可直接访问。

- 随机访问文件中的每个记录通常具有相同的长度，因此记录相对于文件开头的精确位置可以通过记录键计算出来。

- 固定长度记录允许在随机位置插入数据，而不破坏其他数据。之前存储的数据也可以更新或删除，而无需重写整个文件。

## 11.6 创建随机访问文件

- `fwrite` (p. 606) 将从内存中指定位置开始的指定数量字节传输到文件。数据被写入文件位置指针所在的位置。

- `fread` (p. 606) 从文件指针指定的文件位置将指定数量的字节传输到从指定地址开始的区域。

- `fseek` 和 `fwrite` 能够从到文件中读取和写入数据数组。`fread` 和 `fwrite` 的第三个参数是需要处理的元素个数。

- 文件处理通常一次写入一个结构体（`struct`）。

## 11.7 向随机访问文件随机写入数据

- `fseek` (p. 609) 将文件的文件指针置于特定的字节位置。它的第二个参数表示要位移跳转的字节数，第三个参数表示从哪个位置跳转。第三个参数可以是 `SEEK_SET`、`SEEK_CUR` 或 `SEEK_END`。`SEEK_SET` 表示跳转到文件开始处；`SEEK_CUR` (p. 612) 表示跳转从文件的当前位置开始；`SEEK_END` (p. 612) 表示跳转从文件末尾计算。

- 工业级程序通过检查返回值来确定如 `fscanf`、`fseek` 和 `fwrite` 等函数是否正常运行。

- `fscanf` 返回读取的项数，如果在读取数据时发生问题则返回 EOF。

- 如果无法执行跳转操作，`fseek` 返回非零值。

- `fwrite` 返回成功输出的项数。如果此数字小于函数调用中的第三个参数，则发生了错误。

## 11.8 从随机访问文件读取数据

- `fread` 从文件读取指定数量的字节到内存中。

- `fread` 可以通过提供指向将存储元素的数组的指针，并指定要读取的元素个数，来读取几个固定大小的数组元素。

- `fread` 返回成功输入的项数。如果此数字小于函数调用中的第三个参数，则发生了错误。

## 自测练习题

11.1 填空以下内容：

- a) 函数 _________ 关闭文件。

- b) _________ 以类似于 `scanf` 从 `stdin` 读取数据的方式从文件读取数据。

- c) 函数 _________ 从指定文件读取一个字符。

- d) 函数 _________ 从指定文件读取一行。

- e) 函数 _________ 打开文件。

- f) 在随机访问应用程序中从文件读取数据时，通常使用函数 _________。

- g) 函数 _________ 将文件位置指针重新置到文件中的特定位置。

11.2 说明下列哪些是正确的，哪些是错误的。如果是错误的，请解释原因。

- a) 函数 `fscanf` 不能从标准输入读取数据。

- b) 你必须显式使用 `fopen` 来打开标准输入、标准输出和错误流。

- c) 程序必须显式调用函数 `fclose` 来关闭文件。

- d) 如果文件指针指向顺序文件中除文件开头以外的位置，则必须关闭文件并从文件开头重新读取。

- e) 函数 `fprintf` 可以写入到标准输出。

- f) 顺序访问文件中的数据可以在不覆盖其他数据的情况下进行更新。

- g) 在随机访问文件中，不需要搜索所有记录来查找特定的特定记录。

- h) 随机访问文件中的记录不是统一长度的。

- i) 函数 `fseek` 只能相对于文件开头进行。

## 13 使用单条语句完成以下操作。假设这些语句都适用于同一个程序。

- a) 打开 "oldmast.dat" 用于读取，并将返回的文件指针赋值给 `ofPtr`。

- b) 打开 "trans.dat" 用于读取，并将返回的文件指针赋值给 `tPtr`。

- c) 打开 "newmast.dat" 用于写入（创建），并将返回的文件指针赋值给 `nfPtr`。

- d) 从 "oldmast.dat" 读取一条记录。记录由整数、字符串和浮点数余额组成。

- e) 从 "trans.dat" 读取一条记录。记录由整数和浮点数金额组成。
