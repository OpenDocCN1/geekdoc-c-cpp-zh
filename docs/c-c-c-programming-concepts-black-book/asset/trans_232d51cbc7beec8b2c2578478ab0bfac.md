

![](img/43c5f409f9b17790a628c4b4df854b61_316_0.png)

## 11 C 语言中的交叉编译

| 如果需要了解的信息： | 见页码： |
|---|---:|
| 在 Linux 环境中编译 C 代码 | 276 |
| 交叉编译 | 277 |

交叉编译器能够为与编译器自身运行平台不同的平台创建可执行代码。当无法在代码将要执行的平台上编译代码时，就会使用交叉编译器。一个组织可能希望在多个平台上运行代码。在这种情况下，可以同时使用一个单一的构建环境和交叉编译器。通常，交叉编译器用于嵌入式系统。

在本章中，我们学习如何在 Linux 环境中编译 C 代码。然后，本章讨论交叉编译的基础知识。

### 在 Linux 环境中编译 C 代码

在进行交叉编译之前，我们必须了解如何使用编译器的各种选项来编译 C 代码。为此，我们以 Linux 环境为例。要在 Linux 中编译 C 代码，我们首先需要使用文本编辑器（如 vim）在 Linux 中创建一个 C 文件。考虑以下在 Linux 环境中创建的名为 hello.c 的示例程序：

```c
#include<stdio.h>
int main()
{
    printf("\n This is test ");
    return();
}
```

C 程序的编译是使用标准的 gcc 编译器完成的。hello.c 程序可以使用以下命令编译：

```bash
gcc hello.c -o hello
```

上述命令将 hello.c 程序编译为名为 hello 的可执行文件。只需在命令行中输入 hello 即可运行该可执行文件。

hello.c 程序也可以使用以下命令编译：

```bash
gcc -c hello.c
gcc hello.o -o hello
```

第一条命令执行编译并生成源文件的汇编代码，但不进行链接。第一条命令的输出将是一个目标代码文件 hello.o。第二条命令将 hello.o 文件与标准库函数和系统库链接，以生成最终的可执行文件。中间文件 hello.o 将在此过程中被删除。

在编译过程中，gcc 编译器可以使用各种选项。例如，-g 选项指示编译器在生成的代码中包含调试信息。-g 选项可以如下使用：

```bash
gcc -g testProg.c -o testProg
```

使用 -g 选项生成的目标代码将包含可用于 gdb 调试器运行代码时的符号。

另一个重要的选项是 -Wall，它显示代码中可能出现的所有警告。警告可能由于多种原因出现在代码中，例如未初始化的变量、未使用的变量和返回类型不匹配。-Wall 选项可以如下使用：

```bash
gcc -g -Wall testProg.c -o testProg
```

gcc 编译器还允许程序员在使用 -g 选项时指定优化级别。优化级别通过使用 -o 选项来指定，如下所示：

```bash
gcc -O testProg.c -o testProg
```

-o 选项可以实现不同级别的优化。优化范围从 -O1 到 -O3。这些优化级别用于提高速度。例如，-O0 值用于不进行任何优化。在调试代码时，建议不要在代码中进行任何类型的优化，因为优化后的代码将不具备标准 GNU 调试器进行调试所需的正确调试符号。

-I 选项用于在目标代码中包含头文件。此选项可以如下使用：

```bash
gcc testProg.c -o testProg -lm
```

-I 选项告知 gcc 编译器在何处查找代码中使用的头文件。

也可以编译包含多个源文件的程序。用于编译此类程序的命令如下：

```bash
gcc file1.c file2.c -o myprog
```

由于 file1.c 和 file2.c 文件包含源代码，因此在创建目标文件之前需要先编译这两个文件。如果使用以下选项编译代码，也可以获得类似的结果：

```bash
gcc -c file1.c
gcc -c file2.c
gcc file1.o file2.o -o myprog
```

第三条命令的优点在于它分别编译每个源文件。当编译器尝试创建 myprog 文件时，file1.c 文件可能已被修改。在这种情况下，只会重新编译 file1.c，而不会重新编译 file2.c。这将在一定程度上加快编译速度。

接下来，让我们了解交叉编译。

### 交叉编译

每当我们先在 Linux 环境中构建代码时，主机平台和目标平台应始终相同。这是因为编译后生成的二进制文件在同一平台上运行。现在，假设我们想在不同的平台上运行该二进制文件。在这种情况下，我们不能直接将二进制文件加载到目标平台并期望它能够执行。为此，我们需要在编译代码时考虑目标平台的架构。这种编译称为交叉编译。

gcc 编译器经常用于交叉编译。该编译器要求每个目标平台都有可用的编译后的二进制副本。为此，需要使用正确的 --target 选项编译二进制文件。此外，gcc 编译器需要使用相同的 --target 选项进行正确配置。之后，gcc 编译器就可以正常运行了。

在 gcc 中进行交叉编译要求目标平台的 C 库函数的某些部分在主机系统上也可用。可以只编译标准库的一部分，而不是编译完整的标准库。另一种有用的方法是使用 newlib 选项，它是一个只包含基本信息的微型 C 库。

借助 GNU Autotools 包可以轻松完成交叉编译。Autotools 包提供了指定构建平台、目标平台和主机平台的选项。构建平台是编译器被编译的平台。通常，它保持不变，因为它是宿主平台的默认值。主机平台是源代码产物执行的平台。另一方面，交叉编译需要目标平台。它表示包本身将生成什么类型的目标代码。

现在，考虑一个场景：我们希望交叉编译一段代码，使其能够在 Intel PowerPC 驱动的系统上运行。请执行以下步骤来交叉编译代码：

- 1. 从 http://gcc.gnu.org/releases.html 链接下载 binutils-2.14、gcc-3.3.2、glibc-2.3.2、glibc-linuxthreads-2.3.2 和 gdb-6.0（可选）包。
- 2. 构建所有包。建议在与解压目录不同的目录中构建这些包。现在，在配置 binutils 时将 powerpc 指定为目标平台。这可以通过将 --target 选项设置为 powerpc-linux 来完成。使用以下命令构建这些包：

```bash
mkdir build-binutils && cd build-binutils
../binutils-2.14/configure --target=powerpc-linux --prefix=/opt/buckeye/powerpc-linux
make all install
```

- 3. 将交叉编译的二进制文件添加到路径中，如下所示：

```bash
export PATH=$PATH:/opt/buckeye/powerpc-linux
mkdir build-gcc && cd build-gcc
../gcc-3.3.2/configure --target=powerpc-linux --prefix=/opt/buckeye/powerpc-linux \
--disable-shared --disable-threads \
--enable-languages=c --with-newlib
make all-gcc install-gcc
```

设置路径后，我们可以使用最小的 gcc 开始交叉编译。

现在，我们还需要交叉编译 glibc。

- 4. 下载 glibc-linuxthreads 以构建用于交叉编译的 glibc。使用以下命令交叉编译 glibc：

```bash
mkdir build-glibc && cd build-glibc
tar xvzf ../glibc-linuxthreads-2.3.2.tar.gz ../glibc-2.3.2/
../glibc-2.3.2/configure --prefix=/opt/buckeye/powerpc-linux --target=powerpc-linux \
--enable-add-ons=linuxthreads \
--with-headers=${PATH_to_your_powerpc_linux_kernel_tree}/linuxppc_2_4_devel/include \
--with-binutils=/opt/buckeye/powerpc-linux/powerpc-linux/bin
make all install
```

glibc 可能会针对 glibc-2.3.2/stdio-common/sscanf.c ... 报错；因此，我们需要按如下方式更改该文件的签名：

```c
int sscanf (const char *s, const char *format, ...)
```

- 5. 重新配置 gcc 编译器，如下所示：

```bash
../gcc-3.3.2/configure --target=powerpc-linux --prefix=/opt/buckeye/powerpc-linux \
--enable-shared --enable-threads \
--enable-languages=c
make all install
```

现在让我们总结本章讨论的要点。

### 总结

在本章中，我们学习了如何使用各种选项（如 -g 和 -o）在 Linux 环境中编译 C 代码。此外，我们还学习了交叉编译的基础知识。

### 快速复习

#### 多项选择题

- Q1. 以下哪个选项用于引发代码中的所有警告？
    - i. -Wall
    - ii. -Werror
    - iii. -O
    - iv. 以上都不是

- Q2. 以下哪个选项用于指示编译器包含调试符号？
    - i. -g
    - ii. -O
    - iii. -P
    - iv. -w

#### 主观题

- Q1. 解释交叉编译的过程。

- Q2. 借助本章所示的步骤，设计一个在 x86_64 平台上执行交叉编译的方案。

