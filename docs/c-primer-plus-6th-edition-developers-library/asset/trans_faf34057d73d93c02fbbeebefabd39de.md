
f)change font  s)change size  a)change alignment
b)toggle bold  i)toggle italic  u)toggle underline
q)quit
i

ID SIZE ALIGNMENT  B  I  U
1  36  right  off  on  off

f)change font  s)change size  a)change alignment
b)toggle bold  i)toggle italic  u)toggle underline
q)quit
q
Bye!

程序应使用&运算符和合适的掩码，以确保ID和size条目被转换到指定范围内。

7. 编写一个与练习6中描述的行为相同的程序，但使用一个unsigned long变量来保存字体信息，并使用位运算符而不是位成员来管理该信息。

# C预处理器与C库

在本章中，你将学习以下内容：

+   - 预处理器指令：
+     `#define, #include, #ifdef`
+     `#else, #endif, #ifndef`
+     `#if, #elif, #line, #error, #pragma`
+   - 关键字：
+     `_Generic, _Noreturn, _Static_assert`
+   - 函数/宏：
+     `sqrt(), atan(), atan2()`
+     `exit(), atexit()`
+     `assert()`
+     `memcpy(), memmove()`
+     `va_start(), va_arg(), va_copy(), va_end()`
+   - C预处理器的更多功能
+   - 类函数宏与条件编译
+   - 泛型选择表达式
+   - 内联函数
+   - C库总体概述以及其中一些特别的实用函数

C语言本身建立在C关键字、表达式和语句以及使用它们的规则之上。然而，C标准不仅仅描述了C语言本身。它还描述了C预处理器应如何运作，确定了哪些函数构成标准C库，并详细说明了这些函数的工作方式。在本章中，我们将从预处理器开始，探讨C预处理器和C库。

预处理器在程序编译之前查看程序（因此称为“预处理器”）。按照你的预处理器指令，预处理器将程序中的符号缩写替换为它们所代表的指令。预处理器可以根据你的要求包含其他文件，它还可以选择编译器看到哪些代码。预处理器并不了解C。基本上，它接受一些文本并转换为其他文本。这种描述不足以体现它的真正用途和价值，所以让我们来看一些示例。你已经在前面遇到了一些#define和#include的示例。现在我们可以把所学的内容集中起来，并加以补充。

# 程序翻译的第一步

编译器在进入预处理之前，必须先让程序经历一些翻译阶段。编译器开始工作时，会将源代码中出现的字符映射到源字符集。这会处理多字节字符和三字符序列——这些字符扩展使C语言的外部形态更具国际化。（附录B“参考部分VII，扩展字符支持”对这些扩展进行了概述。）

其次，编译器定位每一个反斜杠后跟换行符的实例，并将它们删除。也就是说，两个物理行，例如

```
printf("That's wond\
erful!\n");
```

会被转换为一个逻辑行：

```
printf("That's wonderful!\n");
```

请注意，在这种语境下，“换行符”指的是按Enter键在源代码文件中开始新一行时产生的字符；它并不是指符号表示\n。

这个特性为预处理准备工作提供了便利，因为预处理表达式需要是一个逻辑行那么长，但这个逻辑行可以跨越多个物理行。

接下来，编译器将文本分解为一系列预处理记号，以及空白和注释的序列。（基本来说，记号是由空格、制表符或换行分隔开的组；本章稍后会更详细地讨论记号。）现在一个值得注意的点是，每个注释都会被替换为一个空格字符。因此，类似

```
int/* this doesn't look like a space*/fox;
```

会变成

```
int fox;
```

每个#define行（也就是逻辑行）都有三个部分。第一部分是#define指令本身。第二部分是你选择的缩写，称为宏。有些宏（如这些示例）表示值，它们被称为类对象宏。（C还有类函数宏，我们稍后会讲到。）宏名中不能有空格，并且必须符合C变量遵循的命名规则：只能使用字母、数字和下划线（_）字符，且第一个字符不能是数字。第三部分（该行的其余部分）称为替换列表或主体（见图16.1）。当预处理器在程序中发现你的某个宏时，它几乎总是用主体替换它。（只有一个例外，稍后我们会展示。）这种从宏到最终替换的过程称为宏展开。请注意，你可以在#define行上使用标准C注释；如前所述，在预处理器看到它之前，每个注释都会被替换为一个空格。

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_742_0.png)

图16.1 类对象宏定义的各个部分。

让我们运行示例，看看它是如何工作的：

```
X is 2.
X is 4.
Consistency is the last refuge of the unimaginative. - Oscar Wilde
TWO: OW
```

事情是这样的。语句

```
int x = TWO;
```

变成

```
int x = 2;
```

因为已将2替换为TWO。然后语句

```
PX;
```

变成

```
printf("X is %d.\n", x);
```

因为进行了整体替换。这是一个新情况，因为到目前为止，我们只用宏来表示常量。在这里你会看到，宏可以表达任何字符串，甚至一个完整的C表达式。但请注意，这是一个常量字符串；%x只会打印名为x的变量。

下一行也代表了新的内容。你可能会认为FOUR被替换成了4，但实际过程是这样的：

```
x = FOUR;
```

变成

```
x = TWO*TWO;
```

然后又变成

```
x = 2*2;
```

宏展开过程到此结束。实际的乘法不是在预处理器工作时进行的，而是在编译期间进行的，因为C编译器会在编译时计算所有常量表达式（只包含常量的表达式）。预处理器不做任何计算；它只是非常字面地执行建议的替换。

请注意，宏定义可以包含其他宏。（有些编译器不支持这种嵌套特性。）

在下一行中，

```
printf (FMT, x);
```

变成

```
printf("X is %d.\n",x);
```

因为FMT被对应的字符串替换了。如果你有一个很长的控制字符串需要多次使用，这种方法会很方便。或者，你也可以这样做：

```
const char * fmt = "X is %d.\n";
```

然后你可以将fmt用作printf()的控制字符串。

在下一行中，OW被替换为相应的字符串。双引号使替换后的字符串成为字符串常量。编译器会将其存储在以空字符结尾的数组中。因此，

```
#define HAL 'Z'
```

定义了一个字符常量，而

```
#define HAP "Z"
```

定义了一个字符串：Z\0。

在示例中，我们在行末紧挨着使用了一个反斜杠，以将字符串延伸到下一行：

```
#define OW "Consistency is the last refuge of the unimagina\
tive. - Oscar Wilde"
```

请注意，第二行是左对齐的。相反，假设我们这样做：

```
#define OW "Consistency is the last refuge of the unimagina\
    tive. - Oscar Wilde"
```

那么输出将会是：

```
Consistency is the last refuge of the unimagina    tive. - Oscar Wilde
```

行首与tive之间的空格会计入字符串的一部分。

一般来说，无论预处理器在程序中的什么地方发现你的某个宏，它都会用相应的替换文本逐字替换。如果该字符串还包含宏，这些宏也会被替换。替换的一个例外是位于双引号内的宏。因此，

```
printf("TWO: OW");
```

会逐字打印TWO: OW，而不是打印

```
2: Consistency is the last refuge of the unimaginative. - Oscar Wilde
```

要打印最后这一行，你可以这样使用：

```
printf("%d: %s\n", TWO, OW);
```

在这里，宏位于双引号之外。

什么时候应该使用符号常量？对于大多数数值常量，你应该使用它们。如果某个数字是计算中使用的常量，符号名称会使它的含义更清晰。如果数字是数组大小，符号名称会使以后修改数组大小和循环限制更加容易。如果数字是系统代码，例如EOF，符号表示会使你的程序更具可移植性；只需更改一个EOF定义即可。便于记忆、易于修改、可移植性——这些特性都使符号常量很有价值。

确实，C现在支持的const关键字允许以更灵活的方式创建常量。使用const，你可以创建全局常量和局部常量、数值常量、数组常量和结构常量。另一方面，宏常量可以用来指定标准数组的大小，并作为const值的初始化值：

```
#define LIMIT 20
const int LIM = 50;
static int data1[LIMIT];    // valid
static int data2[LIM];      // not required to be valid
const int LIM2 = 2 * LIMIT; // valid
const int LIM3 = 2 * LIM;   // not required to be valid
```
