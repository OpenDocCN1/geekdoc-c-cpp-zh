
## 29. 内存管理

本章讲解 C 语言中的动态内存管理。C 语言提供了几个用于内存分配和管理的函数。这些函数可以在 **<stdlib.h>** 头文件中找到。

| 序号 | 函数和描述 |
|------|--------------------------|
| 1 | **void *calloc(int num, int size);**<br>该函数分配一个由 **num 个元素**组成的数组，每个元素的大小（以字节为单位）为 **size**。 |
| 2 | **void free(void *address);**<br>该函数释放由 address 指定的内存块。 |
| 3 | **void *malloc(int num);**<br>该函数分配一个 **num** 字节的数组，但不初始化它们。 |
| 4 | **void *realloc(void *address, int newsize);**<br>该函数重新分配内存，将其扩展到 **newsize**。 |

### 动态分配内存

编程时，如果你知道数组的大小，那么定义数组就很容易。例如，要存储一个人的姓名，最多可以有 100 个字符，因此你可以定义如下：

```c
char name[100];
```

但假设你并不知道需要存储的文本长度，例如，你想存储关于某个主题的详细描述。这时，我们需要定义一个字符指针，而不预先定义需要多少内存，之后根据需求分配内存，如下例所示：

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    char name[100];
    char *description;

    strcpy(name, "Zara Ali");

    /* allocate memory dynamically */
    description = malloc( 200 * sizeof(char) );
    if( description == NULL )
    {
        fprintf(stderr, "Error - unable to allocate required memory\n");
    }
    else
    {
        strcpy( description, "Zara ali a DPS student in class 10th");
    }
    printf("Name = %s\n", name );
    printf("Description: %s\n", description );
}
```

当上述代码被编译并执行时，会产生以下结果。

```text
Name = Zara Ali
Description: Zara ali a DPS student in class 10th
```

同样的程序也可以使用 **calloc();** 编写，唯一需要做的就是用 calloc 替换 malloc，如下：

```c
calloc(200, sizeof(char));
```

因此，你拥有完全的控制权，在分配内存时可以传入任意大小值，这与数组不同，数组一旦定义了大小，就无法更改。

## 30. 命令行参数

在运行 C 程序时，可以从命令行向程序传递一些值。这些值被称为命令行参数，它们通常对你的程序很重要，尤其是当你希望从外部控制程序，而不是将这些值硬编码在代码中时。

命令行参数通过 main() 函数的参数进行处理，其中 argc 指传递的参数个数，argv[] 是一个指针数组，指向传递给程序的每个参数。下面是一个简单示例，它检查命令行是否提供了任何参数，并相应地采取行动：

```c
#include <stdio.h>

int main( int argc, char *argv[] )
{
    if( argc == 2 )
    {
    printf("The argument supplied is %s\n", argv[1]);
    }
    else if( argc > 2 )
    {
    printf("Too many arguments supplied.\n");
    }
    else
    {
    printf("One argument expected.\n");
    }
}
```

当上述代码在编译并执行时带有一个参数，会产生以下结果。

```text
$ ./a.out testing
The argument supplied is testing
```

![](img/6e49c39a6ef9e32d938b03dc613e44f6_182_0.png)

当上述代码在编译并执行时带有两个参数，会产生以下结果。

```text
$ ./a.out testing1 testing2
Too many arguments supplied.
```

当上述代码在编译并执行时不传递任何参数，会产生以下结果。

```text
$ ./a.out
One argument expected
```

需要注意的是，**argv[0]** 保存程序本身的名称，**argv[1]** 是指向第一个命令行参数的指针，argv[n] 是最后一个参数。如果没有提供参数，argc 将为 1；如果传递一个参数，则 **argc** 被设为 2。

你传递的所有命令行参数以空格分隔，但如果参数本身包含空格，则可以将这些参数放在双引号 "" 或单引号 '' 中传递。让我们再次改写上面的示例，其中我们将打印程序名称，并通过双引号传递一个命令行参数：

```c
#include <stdio.h>

int main( int argc, char *argv[] )
{
    printf("Program name %s\n", argv[0]);

    if( argc == 2 )
    {
        printf("The argument supplied is %s\n", argv[1]);
    }
    else if( argc > 2 )
    {
        printf("Too many arguments supplied.\n");
    }
    else
    {
        printf("One argument expected.\n");
    }
}
```

当上述代码在编译并执行时带有一个参数，该参数包含空格但位于双引号内，会产生以下结果。

```text
$ ./a.out "testing1 testing2"

Program name ./a.out
The argument supplied is testing1 testing2
```

