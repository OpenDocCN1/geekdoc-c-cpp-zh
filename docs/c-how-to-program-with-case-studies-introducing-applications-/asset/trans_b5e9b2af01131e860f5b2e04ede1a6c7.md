
可访问的。存储期和作用域（*名称可使用的位置*）是两个独立的问题，我们将在 5.13 节看到。

具有静态存储期的标识符有几种类型：*外部标识符*（如全局变量和函数名）以及用存储类说明符 `static` 声明的局部变量。全局变量和函数名默认具有存储类 `extern`。全局变量通过在任何函数定义之外放置变量声明来创建。它们在整个程序执行期间保留其值。全局变量和函数可以被文件中在其声明或定义之后的任何函数引用。这也是使用函数原型的原因之一——当我们在调用 `printf` 的程序中包含 `stdio.h` 时，函数原型被放在文件开头，以使名称 `printf` 对文件其余部分已知。

将变量定义为全局变量而非局部变量，会使不需要访问该变量的函数意外或恶意修改它时产生非预期副作用。一般来说，应避免使用全局变量，除非在具有独特性能要求的情况下（如第 15 章所述）。仅在特定函数中使用的变量应定义为该函数中的局部变量。

局部 `static` 变量仍然只在其定义的函数中已知，并在函数返回时保留其值。下一次调用该函数时，`static` 局部变量包含函数上次退出时的值。以下语句将局部变量 `count` 声明为 `static` 并将其初始化为 1：

```c
static int count = 1;
```

如果你没有显式初始化静态存储期的所有数值，它们默认初始化为零。

关键字 `extern` 和 `static` 在显式应用于外部标识符时具有特殊含义。第 15 章讨论 `extern` 和 `static` 与外部标识符及多源文件程序的显式使用。

ERR PERF

### 自测题

- **1.（填空）** 程序中的每个标识符都有属性，包括存储类、存储期、________ 和 ________。

  **答案：** 作用域、链接。

- **2.（多项选择）** 以下陈述 a)、b) 或 c) 中哪一个是*错误的*？

  a) 标识符的存储期是标识符存在于内存中的时期。

  b) 标识符的作用域是标识符在程序中可以被引用的位置。

  c) 关键字 `auto` 声明具有自动存储期的变量。此类变量在程序控制进入定义它们的块时创建。它们在块活动期间存在，并在程序控制退出该块时被销毁。

  d) 以上所有陈述都是*正确的*。

  **答案：** d。

## 5.13 作用域规则

标识符的作用域是程序中可以引用该标识符的部分。例如，块中的局部变量只能在该块中其定义之后或嵌套于该块内的块中被引用。四种标识符作用域是函数作用域、文件作用域、块作用域和函数原型作用域。

### 函数作用域

标签是后跟冒号的标识符，例如 `start:`。标签是*唯一*具有函数作用域的标识符。标签可以在其出现的函数中的任何位置使用，但不能在函数体之外引用。标签用于 switch 语句（作为 case 标签）和 goto 语句（见第 15 章）。标签在其定义的函数中是隐藏的。这种信息隐藏是实现最小权限原则的一种方式——最小权限原则是良好软件工程的一项基本原则。在应用程序的语境中，该原则指出，代码只应被授予完成其指定任务所需的权限和访问量，而不能更多。

### 文件作用域

在任何函数之外声明的标识符具有文件作用域。此类标识符从声明该标识符的位置到文件末尾，在所有函数中都是“已知的”（即可访问的）。全局变量、函数定义和放置在函数之外的函数原型都具有文件作用域。

### 块作用域

在块内定义的标识符具有块作用域。块作用域在块的结尾右花括号（`}`）处结束。在函数开头定义的局部变量具有块作用域，函数参数也是如此，函数将这些参数视为局部变量。任何块都可以包含变量定义。当块嵌套，并且外层块的标识符与内层块的标识符同名时，外层块的标识符会被隐藏，直到内层块终止。在内层块中执行时，内层块看到的是其局部标识符的值，*而不是*外围块中同名标识符的值。因此，通常应避免使用会隐藏外层作用域中名称的变量名。声明为 `static` 的局部变量仍然具有块作用域，即使它们从程序启动之前就存在。因此，存储期*不*影响标识符的作用域。

### 函数原型作用域

唯一具有函数原型作用域的标识符是函数原型参数列表中使用的标识符。如前所述，函数原型不要求参数列表中有名称——只要求类型。如果在函数原型的参数列表中使用了名称，编译器会忽略它。函数原型中使用的标识符可以在程序的其他地方重用而不会产生歧义。

### 作用域示例

图 5.8 演示了全局变量、局部变量和静态局部变量的作用域问题。定义了一个全局变量 x 并将其初始化为 1（第 9 行）。在任何定义了名为 x 的变量的块（或函数）中，该全局变量都会被隐藏。在 main 中，定义了一个局部变量 x 并将其初始化为 5（第 12 行）。然后打印该变量，以表明全局 x 在 main 中被隐藏。接下来，在 main 中定义了一个新块，其中另一个局部变量 x 初始化为 7（第 17 行）。打印该变量，以表明它隐藏了 main 外层块中的 x。值为 7 的变量 x 在退出该块时被自动销毁，然后再次打印 main 外层块中的局部变量 x，以表明它不再被隐藏。

```c
// fig05_08.c
// Scoping.
#include <stdio.h>

void useLocal(void); // function prototype
void useStaticLocal(void); // function prototype
void useGlobal(void); // function prototype

int x = 1; // global variable

int main(void) {
    int x = 5; // local variable to main

    printf("local x in outer scope of main is %d\n", x);

    { // start new scope
        int x = 7; // local variable to new scope

        printf("local x in inner scope of main is %d\n", x);
    } // end new scope

    printf("local x in outer scope of main is %d\n", x);

    useLocal(); // useLocal has automatic local x
    useStaticLocal(); // useStaticLocal has static local x
    useGlobal(); // useGlobal uses global x
    useLocal(); // useLocal reinitializes automatic local x
    useStaticLocal(); // static local x retains its prior value
    useGlobal(); // global x also retains its value

    printf("\nlocal x in main is %d\n", x);
}

// useLocal reinitializes local variable x during each call
void useLocal(void) {
    int x = 25; // initialized each time useLocal is called

    printf("\nlocal x in useLocal is %d after entering useLocal\n", x);
    ++x;
```

**图 5.8** | 作用域。（第 1 部分，共 2 部分。）

```c
40 printf("local x in useLocal is %d before exiting useLocal\n", x);
41 }
42
43 // useStaticLocal initializes static local variable x only the first time
44 // the function is called; value of x is saved between calls to this
45 // function
46 void useStaticLocal(void) {
47 static int x = 50; // initialized once
48
49 printf("\nlocal static x is %d on entering useStaticLocal\n", x);
50 ++x;
51 printf("local static x is %d on exiting useStaticLocal\n", x);
52 }
53
54 // function useGlobal modifies global variable x during each call
55 void useGlobal(void) {
56 printf("\nglobal x is %d on entering useGlobal\n", x);
57 x *= 10;
58 printf("global x is %d on exiting useGlobal\n", x);
59 }
```

```text
local x in outer scope of main is 5
local x in inner scope of main is 7
local x in outer scope of main is 5

local x in useLocal is 25 after entering useLocal
local x in useLocal is 26 before exiting useLocal

local static x is 50 on entering useStaticLocal
local static x is 51 on exiting useStaticLocal

global x is 1 on entering useGlobal
global x is 10 on exiting useGlobal

local x in useLocal is 25 after entering useLocal
local x in useLocal is 26 before exiting useLocal

local static x is 51 on entering useStaticLocal
local static x is 52 on exiting useStaticLocal

global x is 10 on entering useGlobal
global x is 100 on exiting useGlobal

local x in main is 5
```

图 5.8 | 作用域。（第 2 部分，共 2 部分。）

该程序定义了三个函数，每个函数都不接受参数且不返回任何内容。函数 useLocal 定义了一个局部变量 x，并将其初始化为 25（第 36 行）。当调用函数 useLocal 时，会打印该变量，将其递增，然后在退出函数前再次打印。每次调用此函数时，局部变量 x 都会重新初始化为 25。

函数 useStaticLocal 定义了一个静态变量 x，并在第 47 行将其初始化为 50（回想一下，静态变量的存储空间只在程序开始执行前分配并初始化一次）。声明为 static 的局部变量会保留它们的
