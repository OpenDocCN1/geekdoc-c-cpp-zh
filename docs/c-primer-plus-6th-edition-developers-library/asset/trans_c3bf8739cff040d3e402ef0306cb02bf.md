
程序名。使用 `argv[0]` 而不是显式地使用程序名，可以在你更改可执行文件名时自动改变错误信息。这个特性在 Unix 等允许一个文件拥有多个名称的环境中也很方便。但要注意——某些操作系统可能不识别 `argv[0]`，因此这种用法并非完全可移植。

`exit()` 函数会导致程序终止，并关闭所有打开的文件。`exit()` 的参数会被传递给某些操作系统，包括 Unix、Linux、Windows 和 MS-DOS，其他程序可以使用它。通常的约定是，正常终止的程序传递值 0，异常终止则传递非零值。可以使用不同的退出值来区分不同的失败原因，这是 Unix 和 DOS 编程中的常见做法。然而，并非所有操作系统都识别相同范围的返回值。因此，C 标准规定了一个相当有限的取值范围。具体来说，标准要求使用值 0 或宏 `EXIT_SUCCESS` 表示成功终止，使用宏 `EXIT_FAILURE` 表示不成功终止。这些宏以及 `exit()` 的原型都位于 `stdlib.h` 头文件中。

在 ANSI C 中，在初次调用 `main()` 时使用 `return` 与调用 `exit()` 具有相同的效果。因此，在 `main()` 中，语句

```
return 0;
```

你一直使用的这条语句，其效果等同于下面这条语句：

```
exit(0);
```

但请注意限定短语“初次调用”。如果你让 `main()` 成为一个递归程序，`exit()` 仍然会终止程序，但 `return` 会将控制权传递给上一级递归，直到到达最初的那一级。此时 `return` 才会终止程序。`return` 和 `exit()` 的另一个区别是，即使在 `main()` 之外的其他函数中调用 `exit()`，它也会终止程序。

## fopen() 函数

接下来，程序使用 `fopen()` 打开文件。该函数在 `stdio.h` 中声明。它的第一个参数是要打开的文件的名称；更确切地说，是包含该名称的字符串的地址。第二个参数是一个字符串，用于标识文件要以何种模式打开。C 库提供了多种可能模式，如表 13.1 所示。

表 13.1 fopen() 的模式字符串

| 模式字符串 | 含义 |
|---|---|
| "r" | 以读取模式打开文本文件。 |
| "w" | 以写入模式打开文本文件，将现有文件截断为零长度；如果文件不存在，则创建该文件。 |

## fclose() 函数

`fclose(fp)` 函数关闭 `fp` 所标识的文件，并在需要时刷新缓冲区。对于一个不像这个程序这样随意的程序，你应该检查文件是否已成功关闭。`fclose()` 函数在成功时返回值 0，失败时返回 EOF：

```
if (fclose(fp) != 0)
    printf("Error in closing file %s\n", argv[1]);
```

例如，如果磁盘已满、可移动存储设备已被移除，或者发生了 I/O 错误，`fclose()` 函数可能会失败。

## 指向标准文件的指针

`stdio.h` 文件将三个文件指针与 C 程序自动打开的三个标准文件关联起来：

| 标准文件 | 文件指针 | 通常情况 |
|---|---|---|
| 标准输入 | stdin | 键盘 |
| 标准输出 | stdout | 屏幕 |
| 标准错误 | stderr | 屏幕 |

这些指针都是指向 FILE 的指针类型，因此它们可以用作标准 I/O 函数的参数，就像示例中的 `fp` 一样。接下来，我们看一个创建新文件并向其中写入数据的示例。

## 一个简易的文件精简程序

接下来的程序将选定数据从一个文件复制到另一个文件。它同时打开两个文件，一个使用“r”模式，另一个使用“w”模式。该程序（见程序清单 13.2）采用只保留每第三个字符这种简单粗暴的方式来压缩第一个文件的内容。最后，它将压缩后的文本放到第二个文件中。第二个文件的名称是在旧名称后附加 `.red`（表示 reduced）得到的。使用命令行参数、同时打开多个文件以及追加文件名，通常都是非常实用的技术。这种特定的压缩形式吸引力有限，但正如你将看到的，它也有自己的用处。（同样，把这个程序改成使用标准 I/O 技术而不是命令行参数来提供文件名，也是一件简单的事。）

### 程序清单 13.2 reducto.c 程序

```
// reducto.c -- reduces your files by two-thirds!
#include <stdio.h>
#include <stdlib.h>    // for exit()
#include <string.h>

int main(int argc, char *argv[])
{
    FILE *in, *out;   // declare two FILE pointers
    int ch;
    char name[LEN];   // storage for output filename
    int count = 0;

    // check for command-line arguments
    if (argc < 2)
    {
        fprintf(stderr, "Usage: %s filename\n", argv[0]);
        exit(EXIT_FAILURE);
    }
    // set up input
    if ((in = fopen(argv[1], "r")) == NULL)
    {
        fprintf(stderr, "I couldn't open the file \"%s\"\n", argv[1]);
        exit(EXIT_FAILURE);
    }
    // set up output
    strncpy(name,argv[1], LEN - 5); // copy filename
    name[LEN - 5] = '\0';
    strcat(name,".red");           // append .red
    if ((out = fopen(name, "w")) == NULL)
    {
        // open file for writing
        fprintf(stderr,"Can't create output file.\n");
        exit(3);
    }
    // copy data
    while ((ch = getc(in)) != EOF)
        if (count++ % 3 == 0)
            putc(ch, out);  // print every 3rd char
    // clean up
    if (fclose(in) != 0 || fclose(out) != 0)
        fprintf(stderr,"Error in closing files\n");

    return 0;
}
```

假设可执行文件名为 `reducto`，我们将其应用于名为 `Eddy` 的文件，该文件包含下面这一行：

So even Eddy came oven ready.

命令如下：

```
reducto eddy
```

输出被写入一个名为 `eddy.red` 的文件。程序不会在屏幕上产生任何输出，但显示 `eddy.red` 文件应该会显示以下内容：

```
Send money
```

这个示例说明了几个编程技术。现在让我们来考察其中的一些。

`fprintf()` 函数与 `printf()` 类似，只是它需要一个文件指针作为第一个参数。我们使用 `stderr` 指针将错误消息发送到标准错误；这是 C 的常见做法。

为了构造输出文件的新名称，程序使用 `strncpy()` 将名称 `eddy` 复制到数组 `name` 中。参数 `LEN - 5` 为 `.red` 后缀和最后的空字符留出了空间。如果 `argv[1]` 字符串的长度大于 `LEN - 5`，就不会复制空字符，因此程序会添加一个空字符以防万一。在 `strncpy()` 调用之后，当 `strcat()` 函数附加 `.red` 字符串时，`name` 中的第一个空字符会被 `.red` 中的句点覆盖，从而生成 `eddy.red`。我们还检查了程序是否成功打开了该名称的文件。在某些环境中，这一点尤其重要，因为像 `strange.c.red` 这样的文件名可能是无效的。例如，在传统 DOS 下，你不能在扩展名后面再添加扩展名。（正确的 MS-DOS 做法是将任何现有扩展名替换为 `.red`，因此 `strange.c` 的精简版本将是 `strange.red`。例如，你可以使用 `strchr()` 函数定位名称中的句点（如果有），并只复制句点之前的字符串部分。）

这个程序同时打开了两个文件，因此我们声明了两个 FILE 指针。请注意，每个文件都是独立于另一个文件打开和关闭的。一次打开的文件数量是有限制的。限制取决于你的系统和实现；范围通常在 10 到 20 之间。只要这些文件不是同时打开的，你就可以对不同的文件使用同一个文件指针。

## 文件 I/O：fprintf()、fscanf()、fgets() 和 fputs()

前面各章中的每个 I/O 函数都有一个对应的文件 I/O 函数。主要区别在于，你需要使用 FILE 指针来告诉新函数要操作哪个文件。与 `getc()` 和 `putc()` 一样，这些函数要求你使用指向 FILE 的指针（例如 `stdout`）来标识文件，或者使用 `fopen()` 的返回值。

### fprintf() 和 fscanf() 函数

文件 I/O 函数 `fprintf()` 和 `fscanf()` 的工作方式与 `printf()` 和 `scanf()` 完全一样，只是它们需要一个额外的第一个参数来标识正确的文件。你已经使用过
