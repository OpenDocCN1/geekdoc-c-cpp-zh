

### 问题描述

考虑以下问题描述：

> 创建一个能够存储多达 100 条定长记录的事务处理系统。每条记录应包含账号（记录键）、姓氏、名字和余额。程序应使用随机访问文件，并能够更新账户、插入新账户、删除账户，以及将所有记录以格式化的文本文件形式列出以供打印。

接下来的几节将介绍我们用于创建事务处理程序的技术。图 11.4 展示了如何打开随机访问文件、使用 struct 定义记录格式、向文件写入数据以及关闭文件。该程序使用函数 `fwrite` 将文件 `"accounts.dat"` 的所有 100 条记录初始化为空结构体。每个空结构体包含账号 0、姓氏和名字的空字符串（`""`）以及余额 0.0。我们初始化所有记录以创建文件存储所需的空间，并使其能够判断记录是否包含数据。

```c
// fig11_04.c
// Creating a random-access file sequentially
#include <stdio.h>

// clientData structure definition
struct clientData {
   int account;
   char lastName[15];
   char firstName[10];
   double balance;
};

int main(void) {
   FILE *cfPtr = NULL; // accounts.dat file pointer

   // fopen opens the file; exits if file cannot be opened
   if ((cfPtr = fopen("accounts.dat", "wb")) == NULL) {
      puts("File could not be opened.");
   }
   else {
      // create clientData with default information
      struct clientData blankClient = {0, "", "", 0.0};

      // output 100 blank records to file
      for (int i = 1; i <= 100; ++i) {
         fwrite(&blankClient, sizeof(struct clientData), 1, cfPtr);
      }

      fclose(cfPtr); // fclose closes the file
   }
}
```

图 11.4 | 顺序创建随机访问文件。

第 17 行以二进制模式（`"wb"`）打开文件 `"accounts.dat"` 以供写入。函数 `fwrite`（第 26 行）向文件写入一块字节。其参数为：

- `&blankClient`——要写入对象的地址，
- `sizeof(struct clientData)`——要写入对象的大小（以字节为单位），
- `1`——要写入的该大小对象的数量，
- `cfPtr`——一个 `FILE *`，表示存储这些字节的文件。

回顾一下，`sizeof` 返回其操作数 `struct clientData` 的大小（以字节为单位）。

### 写入对象数组

在第 26 行，`fwrite` 写入一个非数组元素的对象。要写入数组，请将数组作为第一个参数传入，并指定第三个参数为要输出的元素数量。

### 自测

- 1. （判断正误）对于一个四字节的 `int` 变量 `number`，即使该数字的文本表示可能多达 11 位，以下语句也总是写入四个字节：
  fwrite(&number, sizeof(int), 1, fPtr);
  答案：正确。
- 2. （填空）函数 `fread` 和 `fwrite` 以“原始数据”格式读写数据——即作为数据的______。
  答案：字节。
- 3. （填空）函数 `fwrite` 可以写入多个数组元素。在调用 `fwrite` 时，指定一个指向数组的指针和______分别作为第一和第三个参数。
  答案：要写入的元素数量。

## 11.7 向随机访问文件随机写入数据

[注意：图 11.5、11.6 和 11.7 使用图 11.4 中创建的数据文件，因此你必须在运行图 11.5、11.6 和 11.7 之前先运行图 11.4。]

图 11.5 将数据写入文件 `"accounts.dat"`。它使用 `fseek` 和 `fwrite` 将数据存储到文件中的特定位置。函数 `fseek` 将文件位置指针设置为特定的字节位置，然后 `fwrite` 将数据写入该位置。

```c
// fig11_05.c
// Writing data randomly to a random-access file
#include <stdio.h>

// clientData structure definition
struct clientData {
    int account;
    char lastName[15];
    char firstName[10];
    double balance;
}; // end structure clientData

int main(void) {
    FILE *cfPtr = NULL; // accounts.dat file pointer

    // fopen opens the file; exits if file cannot be opened
    if ((cfPtr = fopen("accounts.dat", "rb+")) == NULL) {
        puts("File could not be opened.");
    }
    else {
        // create clientData with default information
        struct clientData client = {0, "", "", 0.0};

        // require user to specify account number
        printf("%s", "Enter account number (1 to 100, 0 to end input): ");
        scanf("%d", &client.account);

        // user enters information, which is copied into file
        while (client.account != 0) {
            // user enters last name, first name and balance
            printf("%s", "Enter lastname, firstname, balance: ");

            // set record lastName, firstName and balance value
            fscanf(stdin, "%14s%9s%lf", client.lastName,
                client.firstName, &client.balance);

            // seek position in file to user-specified record
            fseek(cfPtr, (client.account - 1) *
                sizeof(struct clientData), SEEK_SET);

            // write user-specified information in file
            fwrite(&client, sizeof(struct clientData), 1, cfPtr);

            // enable user to input another account number
            printf("%s", "\nEnter account number: ");
            scanf("%d", &client.account);
        }

        fclose(cfPtr); // fclose closes the file
    }
}
```

图 11.5 | 向随机访问文件随机写入数据。（第 1 部分，共 3 部分）

Enter account number (1 to 100, 0 to end input): 37
Enter lastname, firstname, balance: Barker Doug 0.00

Enter account number: 29
Enter lastname, firstname, balance: Brown Nancy -24.54

其中 offset 是从 whence 指定的位置开始计算的字节数，whence 位于 stream 指向的文件中。正偏移向前搜索，负偏移向后搜索。参数 whence 可以是 `SEEK_SET`、`SEEK_CUR` 或 `SEEK_END`（都在 `<stdio.h>` 中定义），它们指示搜索开始的位置：

- `SEEK_SET` 表示搜索从文件的*开头*开始计算。
- `SEEK_CUR` 表示搜索从文件中的*当前位置*开始计算。
- `SEEK_END` 表示搜索从文件的*末尾*开始计算。

使用 `SEEK_SET` 时应该只用正偏移，使用 `SEEK_END` 时应该只用负偏移。

### 11.7.2 错误检查

为简单起见，本章中的程序并*不*执行错误检查。工业级程序应通过检查返回值来确定 `fscanf`（图 11.5 中的第 34-35 行）、`fseek`（第 38-39 行）和 `fwrite`（第 42 行）等函数是否正常运行。函数 `fscanf` 返回成功读取的数据项数量；如果读取数据时出现问题，则返回 `EOF`。如果无法执行搜索操作（例如试图搜索到文件开头之前的位置），函数 `fseek` 返回非零值。函数 `fwrite` 返回成功输出的项数。如果该数量小于函数调用中的*第三个参数*，则发生了写入错误。

### 自测

- 1. （填空）函数______将文件位置指针设置为文件中的特定字节位置。
  答案：fseek。
- 2. （填空）符号常量______指示文件位置指针应相对于文件开头定位。
  答案：SEEK_SET。

## 11.8 从随机访问文件读取数据

函数 `fread` 从文件中读取指定数量的字节到内存中。例如，

```c
fread(&client, sizeof(struct clientData), 1, cfPtr);
```

从 `cfPtr` 引用的文件中读取由 `sizeof(struct clientData)` 确定的字节数，将数据存储在 `client` 中，并返回读取的字节数。它从文件位置指针指定的位置读取字节。

函数 `fread` 可以读取多个固定大小的数组元素，方法是提供一个指向将存储元素的数组的指针，并指示要读取的元素数量。上述语句读取一个元素。要读取多个元素，请将要读取的元素数量指定为 `fread` 的第三个参数。函数 `fread`

