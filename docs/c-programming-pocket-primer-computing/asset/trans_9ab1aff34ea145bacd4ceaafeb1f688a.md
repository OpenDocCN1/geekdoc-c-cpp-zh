
checks the timestamp of a file and its dependencies in order to determine whether a target must be invoked. In addition, when dependencies are checked, updates are performed recursively.

For example, if a C source code file has a timestamp that is more recent than its corresponding executable, then the associated target in the makefile is invoked, and the associated commands are executed.

In many cases the purpose of the makefile is to create an executable, and the associated target is often the first target in the makefile. For example, if `FindMain2` is the first target in a makefile, then make will execute the commands for the target `FindMain2`.

> **注意** 默认情况下，“make”总是从 makefile 中的第一个目标运行命令，但不会运行其他目标中的任何命令。

If you do not specify the "-o" switch the compiler will create the default executable whose name is `a.out`.

In general terms, a makefile contains one or more entries, where each entry consists of the following:

- 一个目标（通常是一个文件）
- 其依赖项（目标所依赖的文件）
- 要调用的命令（基于目标和依赖项）

请记住，依赖关系是传递的。例如，如果 A 依赖于 B 而 B 依赖于 C，则 A 依赖于 C。检查你的 C 程序以确定每个文件的依赖关系，然后将适当的目标添加到你的 makefile 中。

你也可以使用 makedepend 程序，它分析 C 程序中的头文件（".h"）以确定依赖关系。

## 多个源文件和 make 工具

前几章中的 C 程序不依赖于其他 C 程序。然而，当存在对其他 C 程序（由你或其他人编写）的依赖时，你可以为这些其他 C 程序定义目标。

例如，假设 C 程序 main1.c 依赖于 C 程序 depend1.c 和 depend2.c，其内容分别显示在列表 A.6、列表 A.7 和列表 A.8 中。

https://www.thegeekstuff.com/2012/03/linux-nm-command/

### 列表 A.6：main1.c

```
#include <stdio.h>
#include "depend1.h"
#include "depend2.h"

int main()
{
    printf("Hello from main1.c\n");
    depend1();
    depend2();
    return 0;
}
```

列表 A.6 包含两个与 main1.c 位于同一目录中的 .h 文件：你可以通过包含语句使用双引号（“”）而不是尖括号（<>）来确定这一事实。接下来，main() 函数以 printf() 语句开始，然后调用 depend1() 和 depend2() 函数，这两个函数均未在此 C 程序中定义。

### 列表 A.7：depend1.c

```
#include <stdio.h>

void depend1()
{
printf("Hello from depend1.c\n");
}
```

列表 A.7 以 depend1() 函数开始，该函数包含一个 printf() 语句，显示当前文件 depend1.c 的名称。此语句的唯一目的是帮助你查看程序执行的流程。

### 列表 A.8：depend2.c

```
#include <stdio.h>

void depend2()
{
printf("Hello from depend2.c\n");
}
```

列表 A.8 以 depend2() 函数开始，该函数包含一个 printf() 语句，显示当前文件 depend2.c 的名称。此语句的唯一目的是帮助你查看程序执行的流程。

列表 A.9 显示了指定所需依赖关系的文件 Makefile5 的内容。

### 列表 A.9：Makefile5

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm -f

OBJECTS = depend1.o depend2.o
HEADERS = depend1.h depend2.h

main1: $(OBJECTS) $(HEADERS)
        $(CC) $(CFLAGS) $(OBJECTS) HelloWorld.c -o HelloWorld

depend1.o: depend1.c
        $(CC) -c depend1.c

depend2.o: depend2.c
        $(CC) -c depend2.c

clean:
        $(RM) main1 $(OBJECTS) 2>/dev/null
```

列表 A.9 包含你在之前的 makefile 中见过的几个宏，以及宏 `OBJECTS` 和 `HEADERS`，它们分别指定对象文件列表和头文件列表。

列表 A.9 的下一部分定义了目标 `main1`，它依赖于对象文件和头文件。下一对目标指定如何编译源文件 `depend1.c` 和 `depend2.c` 以分别生成对象文件 `depend1.o` 和 `depend2.o`。

最后的目标是用于“清理”文件的标准目标，在本例中为 `$(OBJECTS)` 指定的对象文件和二进制可执行文件 `main1`。请注意，如果 `depend1.c` 或 `depend2.c` 中的任何一个被修改，则该文件将被重新编译以创建相应的对象文件，而该对象文件又包含在创建二进制可执行文件 `main1` 的新版本步骤中。

按如下方式使用 `-f` 开关启动 `make` 命令：

```
make -f Makefile5
```

现在启动新创建的可执行文件：

```
./main1
```

输出如下所示：

```
Hello from main1.c
Hello from depend1.c
Hello from depend2.c
```

下一节将向你展示如何创建可以以简洁方式处理多个依赖关系的 makefile。

## 用于多个 C 文件的宏

在 [第7章](#) 中，你使用了以下命令以生成二进制可执行文件 FindMain2：

```
gcc -o FindMain2 FindChar2.c FindMain2.c
```

[列表 A.10](#) 显示了 `Makefile6` 的内容，其中 FindMain2 作为目标，当其任何依赖项被修改时就会生成。

### 列表 A.10：Makefile6

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm -f

EXEC = main1
SRC = $(EXEC).c depend1.c depend2.c
OBJ = $(SRC:.c=.o)
LIB = $(SRC:.c=.h)

all: $(EXEC)

# this target generates main1
$(EXEC): $(OBJ)
	$(CC) -o $@ $^ $(LDFLAGS) -lm

%.o: %.c ${LIB}
	$(CC) -o $@ -c $< ${CFLAGS}

clean:
	$(RM) main1 2>/dev/null
```

> 列表 A.10 以一些熟悉的宏定义开始，然后是特定于定义这些宏的 makefile 的宏 `EXEC`、`SRC`、`OBJ` 和 `LIB`。

`OBJ` 宏包含一条规则，指定如何从 C 源文件生成对象文件 ".o"。`LIB` 宏包含一条规则，指定如何确定与 C 源文件关联的头文件。

## makefile 中的其他宏

宏是一个简单的字符串，为其分配一个值后，你就可以在 makefile 目标中使用该字符串。一般语法涉及指定名称然后为其分配值，如下所示：

```
macroname = macrovalue
```

宏与你在前几章中见过的 C 程序中的 `#define` 有些相似。每当 `make` 命令遇到宏名时，它都会用其定义的值替换宏名。事实上，本附录中的一个早期 makefile 包含简单的宏，如下所示：

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm

hello: HelloWorld.c
	$(CC) $(CFLAGS) HelloWorld.c -o HelloWorld
```

CFLAGS 指定编译和创建对象文件的标志

你会注意到，一旦宏被定义，就可以用它来定义后续宏。

由于本附录中的 makefile 简单且简短，使用宏的价值有限。尽管如此，养成在 makefile 中使用宏的习惯是个好主意，特别是如果它们可能变得更复杂。

### 自动变量

如果你想真正精通 make 工具，你需要学习许多在 makefile 中具有特殊意义的变量。以下是一些受支持变量的简短列表，以及它们用途的简短描述：

- $@ 是规则的目标文件名
- $% 是目标成员名：如果目标是 foo.a(bar.o)，则 $% 为 bar.o，$@ 为 foo.a。
- $< 是第一个先决条件的名字
- $? 是比目标更新的所有先决条件的名称
- $^ 是所有先决条件的名称

make 工具支持许多其他内置变量，你可以在线搜索以获取更多信息。

## 在 makefile 中创建多个可执行文件
