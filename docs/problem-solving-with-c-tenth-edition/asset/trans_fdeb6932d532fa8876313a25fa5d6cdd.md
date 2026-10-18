

## 数字证据

数字证据是指以二进制形式存储或传输的信息，可能在法庭上被依赖。

它可能存在于计算机硬盘、手机、个人数字助理（PDA）、光盘、DVD 或存储卡等地方。

### 可在以下位置找到数字证据：
- 计算机
- 手机
- 个人数字助理（PDAs）
- 光盘和 DVD
- 存储卡
- 数字相机

![](img/88b1f375f11336dbd9dac8b1675d0698_54_0.png)

the text contained in the quotes to be written to the screen. The \n at the end of the quoted string tells the computer to start a new line after writing out the text. Similarly, the next line of the program also begins with cout, and that program line causes the following line of text to be written to the screen:

```
Enter the number of pods:
```

The next program line starts with the word cin, so it is an input statement. Let’s look at that line:

```
cin >> numberOfPods;
```

This line may be read, ‘get numberOfPods from cin’ or simply ‘input numberOfPods’.

If you think of the word cin as standing for the keyboard (the input device), then the arrows say that input should be sent from the keyboard to the variable numberOfPods. Look again at the sample dialogue. The next line shown has a 10 written in bold. We use bold to indicate something typed in at the keyboard. If you type in the number 10, then the 10 appears on the screen. If you then press the Return key (which is also sometimes called the Enter key), that makes the 10 available to the program. The statement which begins with cin tells the computer to send that input value of 10 to the variable numberOfPods. From that point on, numberOfPods has the value 10; when we see numberOfPods later in the program, we can think of it as standing for the number 10.

Consider the next two program lines:

```
cout << "Enter the number of peas in a pod:\n";
cin >> peasPerPod;
```

These lines are similar to the previous two lines. The first sends a message to the screen asking for a number. When you type in a number at the keyboard and press the Return key, that number becomes the value of the variable peasPerPod. In the sample dialogue, we assume that you type in the number 9. After you type in 9 and press the Return key, the value of the variable peasPerPod becomes 9.

The next nonblank program line, shown below, does all the computation that is done in this simple program:

```
totalPeas = numberOfPods * peasPerPod;
```

The asterisk symbol, *, is used for multiplication in C++. So this statement says to multiply numberOfPods and peasPerPod. In this case, 10 is multiplied by 9 to give a result of 90. The equal sign says that the variable totalPeas should be made equal to this result of 90. This is a special use of the equal sign; its meaning here is different than in other mathematical contexts. It gives the variable on the left-hand side a (possibly new) value; in this case it makes 90 the value of totalPeas.

The rest of the program is basically more of the same sort of output. Consider the next three nonblank lines:

```
cout << "If you have ";
cout << numberOfPods;
cout << " pea Pods\n";
```

These are just three more output statements that work basically the same as the previous statements that begin with cout. The only thing that is new is the second of these three statements, which says to output the variable numberOfPods. When a variable is output, it is the value of the variable that is output. So this statement causes a 10 to be output. (Remember that in this sample run of the program, the variable numberOfPods was set to 10 by the user who ran the program.) Thus, the output produced by these three lines is:

```
If you have 10 pea pods
```

Notice that the output is all on one line. A new line is not begun until the special instruction \n is sent as output.

The rest of the program contains nothing new, and if you understand what we have discussed so far, you should be able to understand the rest of the program.

## PITFALL 使用 \n 时使用错误的斜杠

当你在 cout 语句中使用 \n 时，请确保使用的是反斜杠，即写成 \。如果你弄错了而使用 /n 而不是 \n，编译器不会给出错误信息。你的程序会运行，但输出看起来会很奇怪。

## PROGRAMMING TIP 输入和输出语法

如果你把 cin 想象成键盘或输入设备的名称，把 cout 想象成屏幕或输出设备的名称，那么就很容易记住箭头 >> 和 << 的方向。它们指向数据移动的方向。例如，考虑下面的语句：

```
cin >> numberOfPods;
```

在上面的语句中，数据从键盘移动到变量 numberOfPods，因此箭头指向从 cin 到该变量。

另一方面，考虑输出语句：

```
cout << numberOfPods;
```

在此语句中，数据从变量 numberOfPods 移动到屏幕，因此箭头指向从变量 numberOfPods 到 cout。

## 简单 C++ 程序的布局

简单 C++ 程序的一般形式如显示 1.9 所示。就编译器而言，换行和空格不必如图中及示例中所示。编译器会接受任何合理的换行和缩进模式。事实上，编译器甚至会接受大多数不合理的换行和缩进模式。然而，程序始终应布局得易于阅读。将左大括号 { 单独放在一行，以及将右大括号 } 单独放在一行，会使这些标点符号易于找到。缩进每个语句并将每个语句放在单独一行，可以轻松看出程序指令是什么。稍后，我们的一些语句会太长而无法容纳在一行中，然后我们将使用这种模式的轻微变体进行缩进和换行。你应遵循本书示例中设定的模式，或遵循你的讲师在课堂上指定的模式。

在显示 1.8 中，变量声明位于以单词 int 开始的那一行。正如我们将在下一章看到的那样，你不必将所有变量声明放在程序开头，但那是一个很好的默认位置。除非你有理由将它们放在其他位置，否则请将它们放在程序开头，如显示 1.9 和显示 1.8 中的示例程序所示。语句是计算机遵循的指令。在显示 1.8 中，语句是以 cout 或 cin 开始的行，以及以 totalPeas 后跟等号开始的那一行。语句通常称为可执行语句。我们将交替使用术语语句和可执行语句。请注意，我们看到的每个语句都以分号结束。语句中的分号与英语句子中的句号或多或少以相同的方式使用；它标记语句的结束。

## DISPLAY 1.9 简单 C++ 程序的布局

```
1 #include <iostream>
2 using namespace std;
3 
4 int main()
5 {
6     Variable_Declarations
7 
8     Statement_1
9     Statement_2
10    ...
11    Statement_Last
12 
13    return 0;
14 }
```

目前你可以将前几行视为一种有趣的方式来表示“这是程序的开始”。但我们可以更详细地解释它们。第一行

```
#include <iostream>
```

称为包含指令。它告诉编译器在哪里找到程序中使用的某些项目的信息。在这种情况下，iostream 是包含处理键盘输入和屏幕输出例程定义的库的名称；iostream 是一个包含有关此库的一些基本信息的文件。我们在这一章前面讨论过的链接程序将库 iostream 的目标代码与你编写的程序的目标代码结合起来。对于库 iostream，这在你的系统上可能会自动发生。你最终也会使用其他库，当你使用它们时，它们需要在程序开始处的指令中命名。对于其他库，你可能需要做的不止是在程序中放置包含指令，但在程序中使用任何库时，你至少需要在程序中放置该库的包含指令。指令始终以符号 # 开始。一些编译器要求指令在 # 周围没有空格，因此最安全的做法是将 # 放在行的最开始，并且在 # 和单词 include 之间不包含任何空格。

以下一行进一步解释了我们刚刚解释的包含指令：

```
using namespace std;
```

此行表示 iostream 中定义的名称应以“标准方式”解释（std 是 standard 的缩写）。我们将在本书稍后对这一行做更多说明。

第三和第四个非空白行，如下所示，只是表示程序的主体从这里开始：

```
int main()
{
```

正确的术语是 main 函数，而不是 main 部分，但这种细微差别的原因要到第 4 章才会与我们有关。大括号 { 和 } 标记程序主体的开始和结束。它们不必单独成行，但这样做便于查找，因此我们将始终将每个大括号单独放在一行。

倒数第二行

```
return 0;
```

表示“到这里时结束程序”。此行不必是程序中的最后一件事，但在非常简单的程序中，将其放在其他任何地方都没有意义。一些编译器允许你省略此行，并会自行判断程序在没有更多语句可执行时结束。

