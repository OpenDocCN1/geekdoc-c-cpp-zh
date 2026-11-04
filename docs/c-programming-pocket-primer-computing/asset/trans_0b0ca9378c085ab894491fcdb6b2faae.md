
有时你需要创建多个二进制可执行文件，而 make 工具使你能够以直接的方式指定目标。假设你需要创建三个名为 mybin1、mybin2 和 mybin3 的可执行文件，其中每个可执行文件都依赖于其关联的 C 程序以及 HelloWorld.c 程序。

清单 A.11 显示了 Makefile7 的内容，它说明了如何指定目标。

### 清单 A.11：Makefile7

```makefile
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm

# invokes targets mybin1, mybin2, and mybin3
all: mybin1 mybin2 mybin3

# 'mybin1' creates mybin1
mybin1: mybin1.o HelloWorld.o
    $(CC) $(CFLAGS) HelloWorld.c -o mybin1

# 'mybin2' creates mybin2
mybin2: mybin2.o HelloWorld.o
    $(CC) $(CFLAGS) HelloWorld.c -o mybin2

# 'mybin3' creates mybin3
mybin3: mybin3.o HelloWorld.o
    $(CC) $(CFLAGS) HelloWorld.c -o mybin3

# removes mybin1, mybin2, mybin3, and *.o files
clean:
    $(RM) mybin1 mybin2 mybin3 *.o
```

清单 A.11 以若干宏定义开头，接着是 all 目标，它指定了依赖项 mybin1、mybin2 和 mybin3，但没有命令行依赖项。因此，make 工具会尝试构建这些文件的最新版本。

## MAKEFILE 中的其他目标类型

到目前为止，示例 makefile 中的目标涉及创建目标文件或二进制可执行文件，但你也可以定义其他类型的目标。例如，清单 A.12 显示了 MakefileTar 的内容，它说明了如何创建 tar（磁带归档）文件以及提取 tar 文件的内容。

### 清单 A.12：MakefileTar

```makefile
TAR=/usr/bin/tar
CTFLAGS=-cvf
XTFLAGS=-xvf
TARFILE=mytar.tar

ctarfile:
    @echo "### Listing of C Programs:"
    @ls -l *.c
    @echo "### Creating tar file:"
    $(TAR) $(CTFLAGS) $(TARFILE) *.c

xtarfile:
    @echo "### Extracting tar file:"
    $(TAR) $(XTFLAGS) $(TARFILE)
```

清单 A.12 以若干宏定义开头，接着是两个目标。第一个目标是 ctarfile，它会显示当前目录中 C 程序的详细列表，然后用这些 C 程序创建一个 tar 文件。

第二个目标是 `xtarfile`，它将执行与 `ctarfile` 目标相反的操作：提取在 `ctarfile` 目标中创建的 tar 文件 `mytar.tar` 的内容。

调用 `ctarfile` 目标的输出如下：

```text
### Listing of C Programs:
-rw-r--r--  1 ocampesato  staff  2048 Jan 26 12:40 Hello2.c
-rw-r--r--  1 ocampesato  staff    83 Jan 19 21:30 HelloWorld.c
### Creating tar file:
/usr/bin/tar -cvf mytar.tar *.c
a Hello2.c
a HelloWorld.c
```

调用 `xtarfile` 目标的输出如下：

```text
### Extracting tar file:
/usr/bin/tar -xvf mytar.tar
x Hello2.c
x HelloWorld.c
```

## 在 MAKEFILE 中指定头文件和库

你已经看到过若干 makefile，其目标将头文件指定为依赖项。此外，你可以使用 “-I” 前缀加路径限定目录来指定头文件，如下所示：

```text
-I/usr/include
```

上一行使 `make` 工具能够在用户指定的目录中搜索头文件。

上一行中的 -I 选项实际上是由 makefile 传递给编译器的；也就是说，它并不是在命令行上传递给 make 命令的。然而，make 工具也支持 -I 选项，用于为 makefile 设置搜索路径。请注意，目录 `/usr/include` 默认已包含在内，因此没有必要指定此目录。

另一方面，假设你创建了位于 `/usr/local/include` 目录中的头文件 `mytime.h`。那么以下代码片段将使编译器能够在正确的位置找到 `mytime.h`：

```text
-I/usr/local/include
```

上一代码片段的优点是，你无需在自定义头文件或自定义 C 程序中显式引用此目录的内容。

此外，你可以使用以下开关来指示编译器在当前目录中搜索头文件：

```text
-I.
```

还有一种选项涉及指定一个目录——相对于当前目录：

```makefile
CC=gcc
IDIR =../include
CFLAGS=-I$(IDIR)
```

### 指定库

make 工具允许你通过两种方式在 makefile 中指定库。

简写方式包括：1）去掉 “lib” 前缀，2）去掉后缀，3）在执行第 1 步和第 2 步后剩余的部分前加上 “-l”（小写 l）作为前缀。

例如，如果你希望在创建可执行文件的过程中包含库 `/usr/lib/libm.a`，请指定字符串 “-lm” 以包含此库。

完成同样操作的较长方式是在编译步骤中指定库的完整路径（最好作为宏定义），如下所示：

```text
-L/usr/lib/libm.a
```

## MAKEFILE 中的虚拟目标

如果你希望执行命令而不是创建目标，可以定义一个虚拟目标，它不涉及任何文件。

makefile 中使用的一些常见虚拟目标包括：

```text
make clean
make all
```

“clean” 目标通常用于从目录中删除文件（例如目标文件和可执行文件）。删除这些文件会强制 makefile 重新编译所有 “.o” 文件。

## 在一个 MAKEFILE 中包含另一个 MAKEFILE

源代码树通常会在源代码的主目录中放置单独的 makefile，用于处理给定目录本地的依赖项。顶层 makefile 充当“主”makefile，其中包含用于创建一个或多个可执行文件的目标。

清单 A.13 显示了 `BranchMakefile` 的内容，其中包含一个目标，该目标将执行位于 branch 子目录中的 `SubBranchMakefile` 里的一个目标。

### 清单 A.13：BranchMakefile

```makefile
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm
MAKE=/usr/bin/make
BRANCH=./branch
ECHO=echo

# only the 'hello' target
all: hello

# 'hello' creates HelloWorld
hello: HelloWorld.c
    $(ECHO) top-level directory...
    $(CC) $(CFLAGS) HelloWorld.c -o HelloWorld
    $(ECHO) going to branch...
    cd $(BRANCH); $(MAKE) -f SubBranchMakefile goodbye

# 'HelloWorld.o' creates HelloWorld.o
HelloWorld.o: HelloWorld.c
    $(CC) $(CFLAGS) -c HelloWorld.c

# removes HelloWorld and HelloWorld.o
clean:
    $(RM) HelloWorld HelloWorld.o
```

清单 A.13 以若干宏定义开头，接着是四个目标。第一个目标是 all，它依赖于目标 hello。hello 目标会打印一条语句，编译文件 HelloWorld.c 以创建 HelloWorld，然后打印另一条语句。此目标执行过程中的最后一步涉及进入一个子目录，并使用 -f 开关调用 make 工具，以指定名为 SubBranchMakefile 的 makefile 和目标 goodbye。第三个目标创建目标文件 HelloWorld.o，最后一个目标是 clean 目标，用于删除文件 HelloWorld 和 HelloWorld.o。

### 清单 A.14：SubBranchMakefile

```makefile
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm

# 'goodbye' creates GoodbyeWorld
goodbye: GoodbyeWorld.c
    $(CC) $(CFLAGS) GoodbyeWorld.c -o GoodbyeWorld

# 'GoodbyeWorld.o' creates GoodbyeWorld.o
GoodbyeWorld.o: GoodbyeWorld.c
    $(CC) $(CFLAGS) -c GoodbyeWorld.c

# removes GoodbyeWorld and GoodbyeWorld.o
clean:
    $(RM) GoodbyeWorld GoodbyeWorld.o
```

清单 A.14 以若干熟悉的宏定义开头，接着是三个语法你也熟悉的目标。请注意，此 makefile 中的 `goodbye` 目标是通过清单 A.13 中 makefile 的某个目标间接调用的。

现在，在包含清单 A.13 中 `BranchMakefile` 的目录中（而*不是*从子目录中）输入以下命令：

```text
make -f BranchMakefile
```

上述命令的输出如下：

```text
echo top-level directory...
top-level directory...
gcc -g -Wall HelloWorld.c -o HelloWorld
echo going to branch...
going to branch...
cd ./branch; /usr/bin/make -f SubBranchMakefile goodbye
gcc -g -Wall GoodbyeWorld.c -o GoodbyeWorld
```
