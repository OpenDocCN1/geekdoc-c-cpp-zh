

## 鼠标操作

使用鼠标访问项目是 Windows 编程中最常见的方法。我们可以用鼠标执行以下操作：

- 通过移动鼠标而不按下任何按钮，将鼠标指针移动到所需位置。
- 当指针位于首选选项上方时，单击鼠标左键。

## 键盘操作

尽管使用鼠标对于基于 Windows 的应用程序是必须的，但访问也可以通过键盘完成。同时按下 ALT 键和所需菜单项的下划线字母将激活相应的下拉菜单。下划线字母称为热键。一旦下拉菜单显示出来，使用下/上箭头键可以突出显示一个选项，然后按下 ENTER 键将激活该选项。

下拉菜单中的某些选项可以通过其显示在这些选项旁边的热键组合直接激活。例如，Ctrl+N 是文件菜单中新建选项的热键组合。同样，通过按下 Ctrl+S，可以在不使用下拉菜单的情况下保存文件。这种快捷方式方法可以在 Visual Workbench 内的任何位置使用。

## D.3 实现 Visual C++ 程序

用任何高级语言编写的计算机程序的开发和实现涉及几个步骤，这些步骤已在附录 C 中描述。

## D.4 创建源代码文件

当您正确安装了 Microsoft Visual C++ 编译器后，您可以从 Microsoft Windows 启动 Visual Workbench。要启动 Visual Workbench，只需从程序组中选择 Visual C++ 图标并单击它。这将显示如 **Fig. D.2** 所示的 Visual Workbench 屏幕。一旦进入 Visual Workbench 屏幕，创建和保存程序就很简单。

### 输入程序

在输入程序之前，您需要做的第一件事是打开一个新文件。从主菜单中选择文件菜单。这将显示如 **Fig. D.4** 所示的下拉文件菜单。选项包括，在其他选项中，打开现有文件、创建新文件和保存新文件。

## D.5 编译和链接

在 Visual C++ 中，将所有源文件编译和链接以创建可执行文件的过程称为“构建”。编译源代码有三种方式，如 **Table D.2** 所示。

当选择构建菜单中的编译选项时，如果没有错误或警告，将把源代码编译为可执行代码，如 **Fig. D.7** 所示。

在编译 C++ 源文件时，Visual C++ 应用程序会提示一条消息以构建新的工作区。工作区只是一个区域，我们可以在其中保存许多源文件、它们的编译文件和链接文件，统称为项目。当我们需要使用多个源文件创建应用程序时，这将使用。

![](img/62b7c32e48e4f960a8dc2825a7119fb2_827_0.png)

```cpp
#include <iostream>  // include header file

using namespace std;

int main()
{
    cout << "C++ is better than C.\n";  // C++ statement
    return 0;
} // End of example
```

Fig. D.6  *Edit window with the sample program*

Table D.2  *Three ways of compiling*

| Command | Action |
| --- | --- |
| Build/Compile | 编译单个程序文件。结果是对象文件。此选项用于当我们想检查特定文件的语法错误时。请注意，它不进行链接，因此不会产生任何可执行文件。 |
| Build/Build | 编译所有修改/新的源文件，然后链接所有对象文件以创建新的可执行文件。当我们在项目上工作时，我们通常使用此命令。因为我们可能会在这里那里更改一些东西，并且只想编译那些修改过的程序。 |
| Build/Rebuild All | 编译项目中的所有文件并将它们链接在一起以创建可执行文件。此命令通常用于当我们想要确保项目中的所有内容都已重新构建时 |

### 可执行文件

在零错误和零警告的编译后，可执行文件 TEST.EXE 将被添加到构建菜单中，如 Fig. D.8 所示。

![](img/62b7c32e48e4f960a8dc2825a7119fb2_828_0.png)

*Fig. D.7* Output window after compiling and linking

![](img/62b7c32e48e4f960a8dc2825a7119fb2_829_0.png)

*Fig. D.8* **Build menu after successful compilation**

输出窗口表明没有警告也没有错误。编译命令已成功生成可执行文件 TEST.EXE。

## D.6 运行程序

您已成功到达兴奋的最后阶段。现在，要运行程序，请单击构建菜单中的执行 TEST.EXE 选项。输出将在新窗口中生成，如 Fig. D.9 所示。

![](img/62b7c32e48e4f960a8dc2825a7119fb2_830_0.png)

**Fig. D.9** *Output generated*

## D.7 管理错误

程序第一次就成功运行的情况很少见。当程序包含错误时，它们会显示在消息窗口中，如 **Fig. D.10** 所示。

您可以在消息窗口中双击语法错误以转到包含该问题的行。修复所有错误，重新编译并执行程序。

## D.8 其他功能

Windows 程序员现在拥有更广泛的工具，可用于面向对象系统的开发。Microsoft 已

AppWizard，Application Wizard 的简称，帮助我们定义程序的基本结构并创建具有所需功能的初始应用程序。但是，请记住它只提供一个框架，特定应用程序的实际代码应由我们编写。

ClassWizard，AppWizard 的密切合作伙伴，允许我们添加类或自定义现有类。ClassWizard 通常在设计 AppWizard 的框架后使用。

正是 Wizards 的强大功能使 Microsoft Visual C++ 如此有用和流行。因此，了解这些工具非常重要。您必须查阅适当的参考资料以获取完整细节。

## ANSI C++ 关键字词汇表

| Keyword | Description |
| --- | --- |
| **asm** | 它用于在 C++ 程序中嵌入汇编语言语句。其使用取决于实现。 |
| **auto** | 它是局部变量的存储类说明符。auto 变量仅在声明它的块或函数中可见。所有局部变量默认都是 auto 类型。 |
| **bool** | 它是一种数据类型，用于保存布尔值，**true** 或 **false**。 |
| **break** | **break** 语句用于导致从循环和 switch 语句中退出。它用于在 switch 语句中提供标签。 |
| **catch** | **catch** 用于描述捕获异常（程序中的异常条件）的 *exception handler* 代码。 |
| **char** | 它是一种基本数据类型，用于声明字符变量和数组。 |
| **class** | **class** 用于创建用户定义的数据类型。它将数据和操作它们的功能绑定在一起。类变量称为 *objects*，是 C++ 中 OOP 的构建块。 |
| **const** | 它是一种数据类型限定符。被限定为 **const** 的数据类型不得被程序修改。 |
| **const_cast** | 它是一种强制转换运算符，用于显式覆盖 **const** 或 **volatile** 对象。 |
| **continue** | 它导致跳过循环中出现的语句直到循环结束。它类似于说“转到循环末尾”。 |
| **default** | 它是 switch 语句中的 **default** 标签。当 none 的 case 标签与 switch 中的表达式匹配时，控制将转移到此语句。 |

**delete**  
它是一个运算符，用于从内存中删除使用 new 运算符创建的对象。

**do**  
do 是一个控制语句，创建操作循环。它与另一个关键字 *while* 一起使用，形式为：

```cpp
do
{
    statements
}
while(expression);
```

当表达式变为零时，循环终止。

**double**  
它是一个浮点数据类型说明符。我们使用此说明符将浮点值的小数点后位数加倍。

**dynamic_cast**  
它是一种强制转换运算符，用于在运行时转换对象的类型。其主要应用是执行对多态对象的强制转换。

**else**  
else 用于指定执行两路分支控制中的替代路径。它与 if 语句一起使用，形式为：

```cpp
if(expression)
    statement-1;
else
    statement-2;
```

如果表达式非零，则执行 statement-1；否则执行 statement-2。

**enum**  
它用于创建用户定义的整数数据类型。示例：

```cpp
enum E{e1,e2,...};
```

