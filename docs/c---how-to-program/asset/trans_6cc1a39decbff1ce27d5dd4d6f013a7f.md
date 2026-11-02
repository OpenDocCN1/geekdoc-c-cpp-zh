
```c
// clientData structure definition
struct clientData {
    unsigned int acctNum; // account number
    char lastName[15]; // account last name
    char firstName[10]; // account first name
    double balance; // account balance
};

int main(void)
{
    FILE *cfPtr; // accounts.dat file pointer

    // fopen opens the file; exits if file cannot be opened
    if ((cfPtr = fopen("accounts.dat", "wb")) == NULL) {
        puts("File could not be opened.");
    }
    else {
        // create clientData with default information
        struct clientData blankClient = {0, "", "", 0.0};

        // output 100 blank records to file
        for (unsigned int i = 1; i <= 100; ++i) {
            fwrite(&blankClient, sizeof(struct clientData), 1, cfPtr);
        }

        fclose(cfPtr); // fclose closes the file
    }
}
```

图 11.10 | 顺序创建随机存取文件。（第 2 部分，共 2 部分。）

函数 fwrite 将字节块写入文件。第 27 行使大小为 sizeof(struct clientData) 的结构体 blankClient 写入 cfPtr 所指向的文件。运算符 sizeof 返回其括号内操作数的字节大小（此处为 struct clientData）。

函数 fwrite 实际上可用于写入对象数组的多个元素。为此，在调用 fwrite 时，将指向数组的指针作为第一个实参提供，并将要写入的元素数量作为第三个实参提供。在前面的语句中，fwrite 用于写入一个不是数组元素的单个对象。写入单个对象等价于写入数组的一个元素，因此 fwrite 调用中为 1。

> [注意：图 11.11、11.14 和 11.15 使用图 11.10 中创建的数据文件，因此必须先运行图 11.10，再运行图 11.11、11.14 和 11.15。]

## 11.7 将数据随机写入随机存取文件

图 11.11 将数据写入文件 "accounts.dat"。它使用 fseek 和 fwrite 的组合将数据存储到文件中的特定位置。函数 fseek 将文件位置指针设置到文件中的特定位置，然后 fwrite 写入数据。示例执行如图 11.12 所示。

```c
// Fig. 11.11: fig11_11.c
// Writing data randomly to a random-access file
#include <stdio.h>

// clientData structure definition
struct clientData {
    unsigned int acctNum; // account number
    char lastName[15]; // account last name
    char firstName[10]; // account first name
    double balance; // account balance
}; // end structure clientData

int main(void)
{
    FILE *cfPtr; // accounts.dat file pointer

    // fopen opens the file; exits if file cannot be opened
    if ((cfPtr = fopen("accounts.dat", "rb+")) == NULL) {
        puts("File could not be opened.");
    }
    else {
        // create clientData with default information
        struct clientData client = {0, "", "", 0.0};

        // require user to specify account number
        printf("%s", "Enter account number"
            " (1 to 100, 0 to end input): ");
        scanf("%d", &client.acctNum);

        // user enters information, which is copied into file
        while (client.acctNum != 0) {
            // user enters last name, first name and balance
            printf("%s", "\nEnter lastname, firstname, balance: ");

            // set record lastName, firstName and balance value
            fscanf(stdin, "%14s%9s%lf", client.lastName,
                client.firstName, &client.balance);

            // seek position in file to user-specified record
            fseek(cfPtr, (client.acctNum - 1) *
                sizeof(struct clientData), SEEK_SET);

            // write user-specified information in file
            fwrite(&client, sizeof(struct clientData), 1, cfPtr);

            // enable user to input another account number
            printf("%s", "\nEnter account number: ");
            scanf("%d", &client.acctNum);
        }

        fclose(cfPtr); // fclose closes the file
    }
}
```

图 11.11 | 将数据随机写入随机存取文件。

```text
Enter account number (1 to 100, 0 to end input): 37
Enter lastname, firstname, balance: Barker Doug 0.00
Enter account number: 29
Enter lastname, firstname, balance: Brown Nancy -24.54
Enter account number: 96
Enter lastname, firstname, balance: Stone Sam 34.98
Enter account number: 88
Enter lastname, firstname, balance: Smith Dave 258.34
Enter account number: 33
Enter lastname, firstname, balance: Dunn Stacey 314.33
Enter account number: 0
```

**图 11.12** | 图 11.11 中程序的示例执行。

### 11.7.1 使用 fseek 定位文件位置指针

第 40–41 行将 `cfPtr` 所引用文件的文件位置指针定位到由 (`client.acctNum - 1`) * `sizeof(struct clientData)` 计算出的字节位置。该表达式的值称为偏移量或位移量。由于账号介于 1 到 100 之间，而文件中的字节位置从 0 开始，因此在计算记录的字节位置时要从账号中减去 1。因此，对于记录 1，文件位置指针被设置为文件的字节 0。符号常量 `SEEK_SET` 表示文件位置指针相对于文件开头按偏移量定位。如上述语句所示，在文件中查找账号 1 会将文件位置指针设置到文件开头，因为计算出的字节位置为 0。

图 11.13 展示了指向内存中 `FILE` 结构的文件指针。此图中的文件位置指针表明，下一个要读取或写入的字节位于距文件开头 5 个字节处。

#### fseek 函数原型

fseek 的函数原型为

```c
int fseek(FILE *stream, long int offset, int whence);
```

其中 `offset` 是在 `stream` 所指向的文件中从 `whence` 开始要查找的字节数——正偏移量向前查找，负偏移量向后查找。参数 `whence` 是 `SEEK_SET`、`SEEK_CUR` 或 `SEEK_END` 之一（均定义在 `<stdio.h>` 中），它们指示查找开始的位置。`SEEK_SET` 表示查找从文件*开头*开始；`SEEK_CUR` 表示查找从文件中的*当前位置*开始；`SEEK_END` 表示从文件*末尾*开始度量查找。

![](img/d0d3b7423c2d9e5650be79209ea1885d_491_0.png)

**图 11.13** | 文件位置指针指示距文件开头 5 个字节的偏移量

### 11.7.2 错误检查

为简单起见，本章中的程序**不**执行错误检查。工业级程序应通过检查返回值来确定 fscanf（图 11.11，第 36–37 行）、fseek（第 40–41 行）和 fread（第 44 行）等函数是否正常运行。函数 fscanf 返回成功读取的数据项数，若读取数据时发生问题则返回值 EOF。如果无法执行查找操作（例如尝试查找到文件开头之前的位置），函数 fseek 返回非零值。函数 fwrite 返回成功输出的项数。如果该数值小于函数调用中的*第三个实参*，则发生了写入错误。

## 11.8 从随机存取文件读取数据

函数 fread 从文件读取指定数量的字节到内存中。例如，

```c
fread(&client, sizeof(struct clientData), 1, cfPtr);
```

从 cfPtr 引用的文件中读取由 sizeof(struct clientData) 确定的字节数，将数据存储到 client 中，并返回读取的字节数。这些字节从文件位置指针所指定的位置读取。函数 fread 可以通过提供指向将要存储元素的数组的指针，并指明要读取的元素数量，来读取多个固定大小的数组元素。前面的语句读取一个元素。要读取*多个*元素，请将元素数量指定为 fread 的第三个实参。函数 fread 返回成功输入的项数。如果该数值小于函数调用中的第三个实参，则发生了读取错误。

图 11.14 顺序读取 "accounts.dat" 文件中的每条记录，确定每条记录是否包含有效的显示数据，并显示包含数据的记录的格式化数据。函数 feof 确定何时到达文件末尾，fread 函数将数据从文件传输到 clientData 结构体 client 中。

