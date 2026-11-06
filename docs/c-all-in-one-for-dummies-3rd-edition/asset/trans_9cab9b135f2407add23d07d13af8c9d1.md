
除了数字之外的任何内容，因为它调用了我们的 EnterOnlyNumbers() 例程。最后，我们输入了一个密码，你可以看到，当我们按下每个键时，计算机显示了星号。然后应用程序保留了秘密密码，并且还是把它写到了屏幕上。

## 理解预处理器指令

编译应用程序时，编译器做的第一件事就是让你的代码经过一个称为预处理器的程序。预处理器只是查找代码中以 # 符号开头的某些语句。你在每个应用程序中已经见过一条这样的语句：#include。这些预处理器语句称为指令，因为它们告诉预处理器去做某事；它们指导预处理器。

把预处理器看作一台机器，它把你的代码转换成临时的、整理好的版本，该版本已经完全准备好进行编译。例如，看看这条预处理器指令：

```cpp
#include <iostream>
```

如果预处理器看到这一行，它会把名为 iostream 的文件中的全部文本（是的，这是一个文件名；它没有扩展名）插入到整理后的源代码版本中。

假设名为 iostream 的文件如下所示：

```cpp
int hello = 10;
int goodbye = 20;
```

里面只有两行。（当然，真正的 iostream 文件要复杂得多。）再假设你自己的源文件 MyProgram.cpp 中有以下内容（如 Preprocessor 示例所示）：

```cpp
#include <iostream>
int main()
{
    cout << "Hello" << endl;
}
```

然后，在预处理器完成预处理后，它会创建一个临时整理后的文件（其中 iostream 文件中的行被插入到 MyProgram.cpp 文件中原来 #include 行的位置），使其看起来像这样：

```cpp
int hello = 10;
int goodbye = 20;
int main()
{
    cout << "Hello" << endl;
}
```

换句话说，预处理器用该文件的内容替换了 `#include` 行。现在，源文件本身也可能有 `#include` 行，而这些行会被它们所引用文件的内容替换。你可能想象得到，原本只是一个只有几行的简单应用程序，在预处理器处理完它之后，实际上可能会有数百行。（事实上，这还是保守估计：我们把默认的 `Code::Blocks` 代码交给预处理器处理，结果它包含 25,613 行！你可以在 `Main.txt` 中看到输出，该文件包含在可下载源代码的 `Preprocessor` 文件夹中。其中许多是空行，原因多种多样，但尽管如此，它仍然是一个非常大的文件！）

![](img/6ba99460b0feb3585671a4612ff5fabb_241_0.png)

别担心：当预处理器处理它时，你的原始源代码文件不会改变。预处理器会创建一个*临时*文件，而编译器编译的正是*那个*文件。另外，你不必手动运行预处理器；编译器会为你运行它。

![](img/6ba99460b0feb3585671a4612ff5fabb_241_1.png)

尽管你不必自己运行预处理器，但如果你好奇它的输出是什么样子，也可以运行。`Code::Blocks` 编译器实际上会调用 `gcc.exe` 来执行编译过程。然而，`gcc` 只是一个启动编译器的小应用程序。但在启动编译器之前，它会运行预处理器。预处理器命令是 `cpp`（代表 C 预处理器）。如果你的路径设置正确，并且想试一试，只需在命令行中输入 `cpp`、源文件名、重定向符号（`>>`）以及输出文件名，例如 `cpp main.cpp >> main.txt`。在大多数情况下，你可以通过在命令行中输入以下行并按 Enter 键来正确设置路径：

```
path=C:\CodeBlocks\MinGW\bin;%path%
```

准备好面对*大量*的行。但看到输出以及代码在准备送入编译器时的样子，是很有意思的。

除了 `#include`，预处理器还为你提供了许多其他指令。其中比较有用的是 `#define` 指令。下面是一个示例 `#define` 行：

```cpp
#define MYSPECIALNUMBER 42
```

预处理器看到这一行后，每次遇到 `MYSPECIALNUMBER` 这个词，就会把它替换为 *42* 这个词（也就是定义后面的任何字母、数字和其他字符序列）。但 `#define` 还允许你创建所谓的*宏*。看看这一行：

```cpp
#define oldmax(x, y) ((x) > (y) ? (x) : (y))
```

预处理器获知这一行后，每次看到 `oldmax` 这个词后面跟着括号中由逗号分隔的两个内容，就会把它替换为 `((x) > (y) ? (x) : (y))` 的形式，用逗号前的内容替换 *x*，用逗号后的内容替换 *y*。例如，如果你随后有这样一行：

无论你使用哪个编译器。（在 Code::Blocks 中，选择“项目>构建选项”。在打开的“项目构建选项”对话框中，单击“编译器设置”选项卡，然后单击“#defines”子选项卡，如图9-1所示。按图中所示输入编译器选项。）要通过命令行选项定义 DEBUG 符号，请将以下行添加到命令中：

```
-D DEBUG
```

无论是在 gcc 命令中，还是在 Code::Blocks 的“项目构建选项”对话框中。然后，当你包含这个编译器选项时，DEBUG 符号就会在整个应用程序中被定义，就好像你在开头包含了 #define DEBUG 行一样。

![](img/6ba99460b0feb3585671a4612ff5fabb_243_0.png)

**图9-1：** 提供你想要用来更改应用程序输出的编译器选项。

现在，当预处理器开始遍历你的应用程序并到达 `#ifdef DEBUG` 行时，它会检查 DEBUG 符号是否已定义。如果该符号已定义，它就会把随后的行输出到整理后的文件中，直到 `#else` 行之前。然后它会跳过之后的行，直到 `#endif` 行之前。

但如果 DEBUG 符号*未*定义，预处理器就会跳过直到 `#else` 之前的行，并输出随后的行，直到 `#endif` 之前。

因此，对于本节前面给出的示例，如果 DEBUG 已定义，那么从 `#ifdef DEBUG` 开始到 `#endif` 的代码块会被替换为这个代码块前半部分的内容：

```cpp
cout << "The value of i is " << i << endl;
```

但如果 DEBUG 未定义，它会被替换为 `#else` 行之后的内容：

```cpp
cout << s << endl;
```

![](img/6ba99460b0feb3585671a4612ff5fabb_244_0.png)

当预处理器遍历你的文件时，它只是在创建一个供编译器使用的新源代码文件。这意味着这些 `#ifdef` 行只在编译器启动预处理器时影响你的应用程序。当你的应用程序编译完成并运行时，这些 `#ifdef` 行就完全不存在了。所以请记住，这些 `#ifdef` 行不会影响应用程序的运行方式——只影响它的编译方式。

![](img/6ba99460b0feb3585671a4612ff5fabb_244_1.png)

使用预处理器指令，你可以拥有应用程序的两个不同版本。在我们给出的示例中，我们正在准备两个版本：调试版本和发布版本。为了告诉编译器要构建哪个版本，我们随后通过删除或添加 -D DEBUG 行来修改命令行选项。

![](img/6ba99460b0feb3585671a4612ff5fabb_244_2.png)

-D 选项在 D 后带不带空格都可以。因此，你可以使用 -DDEBUG 或 -D DEBUG。两者作用相同。

代码清单9-3所示的 Preprocessor2 示例演示了本节涵盖的所有主题。

### 代码清单9-3：使用多种不同的预处理器指令

```cpp
#include <iostream>

using namespace std;

#define UNIVAC
const int total = 200;
const string compname = "UNIVAC";
#if defined(HAL2000)
const int total = 300;
const string compname = "HAL2000";
#else
const int total = 400;
const string compname = "My Computer";
#endif
// This is outdated, but you might
// see it on occasion. Don't write
// code yourself that does this!
#define oldmax(x, y) ((x)>(y) ? (x) : (y))
#define MYSPECIALNUMBER 42

int main()
{
    cout << "Welcome to " << compname << endl;
    cout << "Total is: " << endl;
    cout << total << endl;

    // Try out the outdated things.
    cout << "*** max ***" << endl;
    cout << oldmax(5, 10) << endl;
    cout << oldmax(20, 15) << endl;
    cout << MYSPECIALNUMBER << endl;
}
```
