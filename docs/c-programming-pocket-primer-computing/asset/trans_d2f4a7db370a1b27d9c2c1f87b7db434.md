

```c
#include <stdio.h>

int main(int argc, char **argv)
{
   char *pathvar;

   pathvar = getenv("PATH");
   printf("pathvar=%s",pathvar);
}
```

清单 7.14 很直观：`main()` 函数包含与字符串 `PATH` 相关的内置 C 函数 `getenv()`。调用 `getenv()` 的结果是 `PATH` 环境变量的值，该值被赋给字符指针 `pathvar`。`main()` 函数中的最后一行代码是 `printf()` 函数，它显示 `PATH` 环境变量的值。编译并执行清单 7.14 中的代码后的输出如下：

```text
pathvar=/Users/ocampesato/jython2.5.2:/Users/ocampesato/anaconda/bin:/opt/local/bin:/Users/ocampesato/android-sdk-mac_86/platform-tools:/Users/ocampesato/android-sdk-mac_86/tools:/Users/ocampesato/apache-maven-3.1.1/bin:/usr/local/bin:/Users/ocampesato/xalan-j_2.7.1:/Users/ocampesato/lua-5.1.4/src:/Users/ocampesato/.rvm/bin:/Users/ocampesato/mongoose:/Users/ocampesato/android-ndk-r4b:/usr/local/bin:/usr/local/sbin:/usr/local/mysql/bin:/Applications/XAMPP/xamppfiles/bin:/Users/ocampesato/phantomjs/bin:../Users/ocampesato/anaconda/bin:/Library/Frameworks/Python.framework/Versions/3.3/bin:/opt/local/bin:/opt/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/local/CrossPack-AVR/bin:/usr/local/git/bin:/Users/ocampesato/.rvm/bin:/Users/ocampesato/gradle-1.9/bin:/usr/local/go/bin:/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin:/Users/ocampesato/gyp-read-only:/Users/ocampesato/depot_tools:/Users/ocampesato/hadoop-1.1.0/bin:/Users/ocampesato/local/bin:/Users/ocampesato/PebbleSDK-2.0-BETA5/binoswald-campesatos-macbook:manuscript
```

## 在 C 中设置环境变量

清单 7.15 显示了 SetEnvVars.c 的内容，说明了如何使用 putenv() 函数在当前环境中设置（“放置”）变量及其值。

### 清单 7.15：SetEnvVars.c

```c
#include <stdlib.h>
#include <stdio.h>

int main(int argc, char **argv)
{
    char *pathvar;

    pathvar = getenv("PATH");
    printf("The current path is: %s\n\n", pathvar);

    if (-1 == putenv("PATH=:/home/userid"))
    {
        printf("putenv failed \n");
        return EXIT_FAILURE;
    }

    pathvar = getenv("PATH");
    printf("The new path is: %s\n", pathvar);

    return 0;
}
```

清单 7.14 读取 PATH 环境变量的值，而清单 7.15 设置环境变量的值。事实上，清单 7.15 首先调用 getenv() 函数读取 PATH 环境变量的值，然后调用内置 C 函数 putenv() 为 PATH 变量分配新值。请注意条件逻辑：如果 putenv() 命令失败，将显示错误消息。

main() 函数的最后一部分再次调用 getenv() 函数并显示结果，只是为了确认 PATH 变量已正确更新。编译并执行清单 7.15 中的代码后的输出（为简洁起见已截断）如下：

```text
The current path is: /opt/spark/bin:/Users/owner/mongodb-osx-x86_64-3.4.2/bin:/Users/owner/anaconda2/bin:

The new path is: /:/home/userid
```

请记住，程序执行完毕后，PATH 变量将保留其初始值（即更改是临时的）。

## C 中的存储类说明符

C 中有 5 个存储类说明符：

- auto
- extern
- static
- register
- _Thread_local

auto 存储类说明符表示变量具有自动存储期。由于这是默认值，因此很少使用。extern 关键字与外部链接有关，主要用于在头文件中声明全局变量。static 关键字根据上下文有不同的含义。它可以声明具有静态存储期的变量，这意味着其值在函数的多次调用之间持续存在。它也可以声明变量具有内部链接。

`_Thread_local` 存储类在多线程编程中很有用，它声明的变量在每个线程中具有不同的值。register 关键字过去是向编译器提示某个变量使用频繁，应放入处理器寄存器以便快速访问。自 C 语言诞生以来，编译器优化已大幅改进，现代编译器会直接忽略 register 提示。

使用这些 C 说明符的一些示例如下：

```c
register int i;        // i is an int, register keyword
                       // probably ignored
extern int j;          // declaration for j, j must be defined
                       // elsewhere
static int k = 0;      // variable k only visible in this
                       // translation unit
_Thread_local m = 5;   // m has a different instance in each
                       // thread

void f() {
    int n = 2;         // initialized to 2 every function
                       // call
    auto int m = 2;    // same as above, auto is the default
    static int o = 3;  // set to 3 on the first function call
}
```

## 如何编写使用指针的复杂代码

这个标题略带戏谑的小节旨在向你展示最好避免的那类代码，因为很容易犯错。清单 7.16 显示了 `DontDoThis.c` 的内容，说明了如何错误地使用指针。

### 清单 7.16：DontDoThis.c

```c
#include <stdlib.h>

int main()
{
  // a data value and an array
  int value, array[10];

  // point to the first element
  int *arrptr = &array[0];
  printf("arrptr: %d\n", arrptr);

  // get element #0 from arrptr
  value = *arrptr++;
  printf("value1: %d\n", value);

  value = *++arrptr;
  printf("value2: %d\n", value);

  // get element #1 from arrptr
  value = ++*arrptr;
  printf("value3: %d\n", value);
}
```

尽管清单 7.16 中的代码在语法上是正确的，但即使是经验丰富的 C 程序员也可能无意中引用指针的内存位置，而不是指针的内容（这是非常常见的情况）。

运行清单 7.16 中编译后的代码，你将看到以下输出：

```text
arrptr: 1560138064
value1: 280822976
value2: 0
value3: 1
```

再举一个例子，考虑以下代码块，它使用指针将字符串从源（q）复制到目标（p）：

```c
void copy_string(char *p, char *q) {
    while (*p++ = *q++);
}
```

尽管可以确定前一个代码块的用途，但下面这段更长——但等价——的代码更容易理解、维护和调试：

```c
void copy_string(char *dest, char *source)
{
    while (1) {
        *dest = *source;

        // Exit if we copied the end of string
        if (*dest == '\0') return;

        ++source;

        ++dest;
    }
}
```

请注意，if 语句和 return 语句位于同一行。在这个例子中，代码非常直观，不可能产生混淆，这向你表明，关于代码语法的规则可能存在例外。

## C 中的错误处理

尽管 C 不直接支持错误处理，但你可以通过返回值确定程序执行的结果。回想一下，C 程序中的 main() 函数返回类型为 `int`，这意味着你可以返回不同的值来表示程序执行的不同结果。

### errno 全局变量

大多数 C 函数调用在发生错误时返回 -1 或 `NULL`，并通过全局变量 `errno` 设置错误代码。因此，你可以检查该变量的值，以便根据该变量的值决定如何继续。如果你感兴趣，各种错误代码定义在 `<errno.h>` 头文件中。

### perror() 和 strerror() 函数

C 编程语言提供了 `perror()` 和 `strerror()` 函数，用于显示与 `errno` 关联的文本消息。

`perror()` 函数显示你传给它的字符串，随后是一个冒号、一个空格，然后是当前 `errno` 值的文本表示。例如，如果你的 C 程序找不到某个目录，将显示以下消息：

> 错误：没有那个文件或目录

`strerror()` 函数返回指向当前 `errno` 值文本表示的指针，其输出与 `perror()` 函数的输出类似。

### 如何从错误中退出

请记住以下行为：尝试*浮点数除以零*的 C 程序是运行时错误，而*整数除以零*是未定义行为。解决方案包括检查……的值

