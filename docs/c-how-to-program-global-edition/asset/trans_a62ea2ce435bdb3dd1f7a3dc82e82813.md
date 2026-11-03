
在此应用程序中，号码用作记录键——文件将按账号顺序创建和维护。本程序假定用户按账号顺序输入账户。在一个全面的应收账款系统中，将提供排序功能，以便用户可以按任意顺序输入记录。然后记录将被排序并写入文件。[注意：图 11.6–11.7 使用图 11.2 中创建的数据文件，因此您必须先运行图 11.2 中的程序，然后再运行图 11.6–11.7 中的程序。]

```
~~~c
// Fig. 11.2: fig11_02.c
// Creating a sequential file
#include <stdio.h>

int main(void)
{
   FILE *cfPtr; // cfPtr = clients.txt file pointer

   // fopen opens file. Exit program if unable to create file
   if ((cfPtr = fopen("clients.txt", "w")) == NULL) {
      puts("File could not be opened");
   }
   else {
      puts("Enter the account, name, and balance.");
      puts("Enter EOF to end input.");
      printf("%s", "? ");

      unsigned int account; // account number
      char name[30]; // account name
      double balance; // account balance

      scanf("%d%29s%lf", &account, name, &balance);

      // write account, name and balance into file with fprintf
      while (!feof(stdin)) {
         fprintf(cfPtr, "%d %s %.2f\n", account, name, balance);
         printf("%s", "? ");
         scanf("%d%29s%lf", &account, name, &balance);
      }

      fclose(cfPtr); // fclose closes file
   }
}
~~~

```
~~~
Enter the account, name, and balance.
Enter EOF to end input.
? 100 Jones 24.98
? 200 Doe 345.67
? 300 White 0.00
? 400 Stone -42.16
? 500 Rich 224.62
? ^Z
~~~

Fig. 11.2 | 创建顺序文件。

### 11.3.1 指向 FILE 的指针

现在让我们检查这个程序。第 7 行指出 `cfPtr` 是一个 *指向 FILE 结构的指针*。C 程序使用单独的 FILE 结构管理每个文件。每个打开的文件必须有一个单独声明的类型为 FILE 的指针来引用该文件。您无需了解 FILE 结构的具体细节即可使用文件，但如果愿意，可以研究 `stdio.h` 中的声明。我们很快就会确切地看到 FILE 结构如何 *间接* 指向操作系统的文件控制块（FCB）。

### 11.3.2 使用 fopen 打开文件

第 10 行命名了程序要使用的文件——"clients.txt"——并与文件建立了“通信线路”。文件指针 `cfPtr` 被赋值为使用 `fopen` 打开的文件的 *指向 FILE 结构的指针*。函数 `fopen` 接受两个参数：

- 一个文件名（可以包含通向文件位置的路径信息）和
- 一个文件打开模式。

文件打开模式 "w" 表示文件要以写入方式打开。如果文件 *不存在* 且以写入方式打开，`fopen` 会创建该文件。如果已存在的文件以写入方式打开，则文件内容会被 *没有任何警告* 地丢弃。在程序中，`if` 语句用于确定文件指针 `cfPtr` 是否为 `NULL`（即文件未打开，因为文件不存在或用户没有权限打开文件）。如果为 `NULL`，程序会打印错误消息并终止。否则，程序会处理输入并将其写入文件。

> > **公共编程错误 11.1**
> >
> > *以写入方式（"w"）打开现有文件，而实际上用户希望保留文件，会在没有任何警告的情况下丢弃文件内容。*

> > **公共编程错误 11.2**
> >
> > *在程序中尝试引用文件之前忘记打开文件是一个逻辑错误。*

### 11.3.3 使用 feof 检查文件结束指示符

程序提示用户为每条记录输入各个字段，或在数据输入完成后输入 *文件结束*。图 11.3 列出了各种计算机系统输入文件结束的键组合。

| 操作系统 | 键组合 |
|---|---|
| Linux/Mac OS X/UNIX | &lt;Ctrl&gt; d |
| Windows | &lt;Ctrl&gt; z 然后按 Enter |

**Fig. 11.3** | 各种流行操作系统的文件结束键组合。

第 25 行使用函数 `feof` 确定 `stdin` 的文件结束指示符是否已设置。文件结束指示符告知程序没有更多数据需要处理。在图 11.2 中，当用户输入文件结束键组合时，标准输入的文件结束指示符会被设置。函数 `feof` 的参数是要测试文件结束指示符的文件的指针（本例中为 `stdin`）。当文件结束指示符已被设置时，函数返回非零（真）值；否则函数返回零。本程序中包含 `feof` 调用的 `while` 语句会在文件结束指示符未设置时继续执行。

### 11.3.4 使用 `fprintf` 写入文件

第 26 行将数据写入文件 `clients.txt`。稍后由设计用于读取文件的程序可以检索这些数据（参见第 11.4 节）。函数 `fprintf` 等同于 `printf`，只是 `fprintf` 还接受一个文件指针参数，用于指定要写入数据的目标文件。函数 `fprintf` 可以通过使用 `stdout` 作为文件指针将数据输出到标准输出，如下所示：

```
    fprintf(stdout, "%d %s %.2f\n", account, name, balance);
```

### 11.3.5 使用 `fclose` 关闭文件

用户输入文件结束后，程序使用 `fclose`（第 31 行）关闭 `clients.txt` 文件并终止。函数 `fclose` 也接受文件指针（而不是文件名）作为参数。*如果函数 `fclose` 未显式调用，操作系统通常会在程序执行终止时关闭文件。* 这是操作系统“ housekeeping ”的一个例子。

> **性能提示 11.1**
> 
> *关闭文件可以释放其他用户或程序正在等待的资源，因此您应在文件不再需要时立即关闭每个文件，而不是等待操作系统在程序终止时关闭它。*

在图 11.2 程序的示例执行中，用户输入了五个账户的信息，然后输入文件结束以表示数据输入完成。示例执行未显示数据记录在文件中实际的外观。为了验证文件是否成功创建，在下一节中我们将介绍一个读取文件并打印其内容的程序。

## FILE 指针、FILE 结构与 FCB 之间的关系

图 11.4 说明了 FILE 指针、FILE 结构和 FCB 之间的关系。当文件 `"clients.txt"` 被打开时，该文件的 FCB 会被复制到内存中。图示显示了 `fopen` 返回的文件指针与操作系统用于管理文件的 FCB 之间的连接。程序可能不处理任何文件、处理一个文件或处理多个文件。程序中使用的每个文件都将由 `fopen` 返回不同的文件指针。*文件打开后，后续的所有文件处理函数都必须使用适当的文件指针引用该文件。*

用户可以访问此内容

```
cfPtr = fopen("clients.dat", "w");
```

fopen 返回一个指向 FILE 结构的指针
（定义在 <stdio.h> 中）。

cfPtr

"clients.dat" 的 FILE 结构
包含一个描述符，即一个小整数，是打开文件表中的索引。

当程序发出如下 I/O 调用时

```
fprintf(cfPtr, "%d %s %.2f", account, name, balance);
```

程序在 FILE 结构中定位描述符（7）并使用描述符在打开文件表中查找 FCB。

只有操作系统可以访问此内容

打开文件表

程序调用操作系统服务，该服务使用 FCB 中的数据控制对磁盘上实际文件的所有输入和输出。注意：用户不能直接访问 FCB。

此条目在文件打开时从 FCB 复制而来。

Fig. 11.4 | FILE 指针、FILE 结构与 FCB 之间的关系。

### 11.3.6 文件打开模式

文件可以以多种模式之一打开，这些模式在图 11.5 中进行了总结。表格前半部分中的每个文件打开模式都有一个对应的二进制模式（包含
