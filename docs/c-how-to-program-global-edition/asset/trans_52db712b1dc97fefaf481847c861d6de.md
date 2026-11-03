
输入请求
1 - 列出余额为零的账户
2 - 列出贷方余额账户
3 - 列出借方余额账户
4 - 结束运行
? 1

余额为零的账户：
300    White    0.00

? 2

贷方余额账户：
400    Stone    -42.16

? 3

借方余额账户：
100    Jones    24.98
200    Doe      345.67
500    Rich     224.62

? 4
运行结束。

Fig. 11.8 | 图 11.7 的信用查询程序的示例输出。

## 更新顺序文件

此类顺序文件中的数据如果不冒破坏其他数据的风险就无法修改。例如，如果需要将姓名 "white" 改为 "Worthington"，旧姓名不能简单地被覆盖。White 的记录写入文件的方式为

```
300 White 0.00
```

如果使用新姓名从文件中的同一位置开始重写记录，记录将变为

```
300 Worthington 0.00
```

新记录更大（字符更多），比原始记录长。"Worthington" 中第二个 "o" 之外的字符将覆盖文件中下一个顺序记录的开头。这里的问题是，在使用 fprintf 和 fscanf 的格式化输入/输出模型中，字段——因此记录——大小可能不同。例如，值 7、14、-117、2074 和 27383 内部都作为 int 存储相同数量的字节，但在屏幕上显示或作为文本写入文件时，它们是不同大小的字段。

因此，通常不使用 fprintf 和 fscanf 的顺序访问来就地更新记录。相反，通常会重写整个文件。为了进行上述姓名更改，此类顺序访问文件中的 300 White 0.00 之前的记录将被复制到新文件，新记录将被写入，然后 300 White 0.00 之后的记录将被复制到新文件。这需要处理文件中的每一条记录以更新一条记录。

函数 fread 将由文件位置指针指定的文件中的数据复制到内存中从指定地址开始的区域。现在，写入一个四字节整数时，而不是使用

```
fprintf(fPtr, "%d", number);
```

它可能打印一位数字或多达 11 位数字（10 位数字加上一个符号，每个符号根据区域设置的字符集至少需要一个字节的存储），我们可以使用

```
fwrite(&number, sizeof(int), 1, fPtr);
```

它总是在具有四字节整数的系统上从变量 number 向 fPtr 表示的文件写入四个字节（我们稍后会解释 1 参数）。稍后，fread 可用于将这四个字节读入整数变量 number。尽管 fread 和 fwrite 以定长而非变长格式读取和写入数据，例如整数，但它们处理的数据以计算机“原始数据”格式（即字节数据）处理，而不是 printf 和 scanf 的人类可读文本格式。因为数据的“原始”表示是系统相关的，所以“原始数据”可能在其他系统上不可读，或由其他编译器或使用其他编译器选项生成的程序不可读。

## fwrite 和 fread 可以写入和读取数组

函数 fwrite 和 fread 能够从文件读取和写入数据数组。fread 和 fwrite 的第三个参数是要从文件读取或写入的数组元素的数量。前面的 fwrite 函数调用将单个整数写入文件，因此第三个参数为 1（就像写入数组的一个元素一样）。文件处理程序很少将单个字段写入文件。通常，它们一次写入一个 struct，如我们在以下示例中所示。

## 问题陈述

考虑以下问题陈述：

创建一个能够存储最多 100 条定长记录的交易处理系统。每条记录应包含一个将用作记录键的账号、姓氏、名字和余额。 resulting 程序应能够更新账户、插入新账户记录、删除账户并将所有账户记录列出到格式化的文本文件中以便打印。使用随机访问文件。

接下来的几节介绍创建交易处理程序所需的技巧。图 11.10 显示了如何打开随机访问文件、使用 struct 定义记录格式、向文件写入数据并关闭文件。此程序使用函数 fwrite 用空 struct 初始化文件 “accounts.dat” 的全部 100 条记录。每个空 struct 包含账号为 0、姓氏为 ""（空字符串）、名字为 "" 和余额为 0.0。文件以这种方式初始化是为了创建文件存储的空间并使能够确定记录是否包含数据。

// Fig. 11.10: fig11_10.c
// Creating a random-access file sequentially
#include <stdio.h>

Fig. 11.10 | 顺序创建随机访问文件。（第 1 部分，共 2 部分。）

```c
// Fig. 11.11: fig11_11.c
// Writing data randomly to a random-access file
#include <stdio.h>

// clientData structure definition
struct clientData {
    unsigned int acctNum;  // account number
    char lastName[15];     // account last name
    char firstName[10];    // account first name
    double balance;        // account balance
}; // end structure clientData

int main(void)
{
    FILE *cfPtr;  // accounts.dat file pointer

    // fopen opens the file; exits if file cannot be opened
    if ((cfPtr = fopen("accounts.dat", "rb+")) == NULL) {
        puts("File could not be opened.");
    }
    else {
        // create clientData with default information
        struct clientData client = {0, "", "", 0.0};

        // require user to specify account number
        printf("%s", "Enter account number\n");
        printf("%s", " (1 to 100, 0 to end input): ");
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

    }
    fclose(cfPtr); // fclose closes the file
}
```

输入账号（1 到 100，0 结束输入）：37
输入姓氏、名字、余额：Barker Doug 0.00
输入账号：29
输入姓氏、名字、余额：Brown Nancy -24.54
输入账号：96
输入姓氏、名字、余额：Stone Sam 34.98
输入账号：88
输入姓氏、名字、余额：Smith Dave 258.34
输入账号：33
输入姓氏、名字、余额：Dunn Stacey 314.33
输入账号：0

Fig. 11.12 | 图 11.11 中程序的示例执行。

## 11.7.1 使用 fseek 定位文件位置指针

行 40–41 将 cfPtr 引用的文件的文件位置指针定位到由 (client.accountNum - 1) * sizeof(struct clientData) 计算得到的字节位置。该表达式的值称为偏移量或位移。因为账号在 1 到 100 之间，而文件中的字节位置从 0 开始，所以在计算记录的字节位置时要从账号中减去 1。因此，对于记录 1，文件位置指针被设置为文件的字节 0。符号常量 SEEK_SET 表示文件位置指针相对于文件开头按偏移量定位。如上所述，对文件中账号 1 的查找将文件位置指针设置为文件开头，因为计算出的字节位置为 0。

图 11.13 说明了指向内存中 FILE 结构的指针。图中文件位置指针表示下一个要读取或写入的字节距离文件开头 5 个字节。

## fseek 函数原型

fseek 的函数原型为

```
int fseek(FILE *stream, long int offset, int whence);
```

其中 offset 是从 whence 在 stream 指向的文件中查找的字节数——正偏移向前查找，负偏移向后查找。参数 whence 是 SEEK_SET、SEEK_CUR 或 SEEK_END 中的一个值（均在 <stdio.h> 中定义），它们指示查找开始的位置。SEEK_SET 表示查找从文件开头开始；SEEK_CUR 表示查找从文件当前位置开始；SEEK_END 表示查找从文件末尾开始。
