# 初学者的 C 编程：速成课程




## Introduction

Congratulations on downloading *C Programming for Beginners: Crash Course – Ultimate Edition* and thank you for doing so.

The following chapters will discuss some of the things that you need to know in order to get started with working in the C programming language. This is one of the first coding languages that worked to make things easier for people to use. Many of the programming languages that came before this were too complicated and only those really advanced in computers were able to figure it out. The C language changed all this and made it easier for anyone to learn how to code and it is now the basis for many of our modern languages.

This guidebook is going to take some time to look over the basics of the C language and how you can learn how to use it on your own. We will discuss some of the history that comes with this programming language as well as the basics in functions, variables, and keywords before moving on to comparisons, such as the if and if else statements inside of this language.

When you are done with this book, you will have experience writing some of your own code, with some of the examples that are inside, and the confidence to go out there and make some new programs. When you are ready to learn one of the best programming languages out there, and one of the first that made programming easier for everyone, make sure to read through this guidebook and learn how the C programming language can work for you!

There are plenty of books on this subject on the market, thanks again for choosing this one! Every effort was made to ensure it is full of as much useful information as possible, please enjoy!

## Chapter 1: An Introduction to the C Programming Language

When it comes to learning a new programming language, there may seem to be a lot of parts that you need to keep track of. You may worry as a beginner that it is too hard to put together a code on your own and that you need years of experience. Even if you have worked in coding in the past, you may worry about how difficult it will be to learn something new and how different it is from your chosen computer language. But coding can be simple to learn, even when you are brand new to the process.

In this book, I am going to take some time to show you how to use the C programming language, one of the best options out there for all the options and power that come with learning how to do your own coding. I will show you some of the jargon that comes with learning how to program and walk you through some of the steps that are needed to end this book with writing your own code.

The C programming language started in 1972 with the help of Dennis Ritchie. At the time, Ritchie was a computer scientist at the AT&T Bell Laboratories and he needed to develop a few programs for his own personal use. He was trying to make the process of computing as simple as he could and he realized that many of the current languages were too complex for what he wanted and for what other people were able to use.

The goal with this new language was to help create a programming language that was efficient, but also one that could help the community form a fellowship. They knew that to keep things working smoothly you couldn't just have information put into the terminal of the code, but you needed to have some post programming communication there as well.

The result of all this work was the C programming language. This is a language that is general purpose as well as structured and it is known as a procedural oriented programming language. It is not a language that is designed for a specific application, but it is well suited for those who need a scientific or business application. There are many features inside, such as macros, looping statements, and control structures that are required for the applications.

There are many different features that you are going to enjoy as a user of the C language including:

- Interactivity: this was one of the first of its kind to interact with the user and become easier to use, even without a lot of experience.
- Reliability: the C language is really reliable. You will be able to write out your codes and not worry about them crashing or having issues down the line.
- Efficiency and effectiveness: if you want a programming language that is effective and gets the job done, none will work the same as the C language.
- Flexibility: this language is really flexible. There are many different programs that you are able to work with inside this language and while it is mostly used for business purposes, you would be able to use it for any of your own needs.
- Portability: the C language can go where you go, working on a variety of different platforms whether you are on a Windows computer, Mac, Linux operating system, or something else.

While there have been many programming languages developed over the years and the changes made, the C language is still a great one to learn how to use. Many programmers still use the C language and many of the newer programming languages will use C as their foundation. If you want to learn a language that will make other coding languages easier to learn down the road, the C language is the best option for you.

### Getting Your IDE

Before you are able to use your C language, you need to make sure that you download a good IDE to go with it. The IDE, or the Integrated Development Environment is basically the area where you will write, link, edit, compile, and run your code. Your C language is basically not going to work unless you have an IDE in place to help you out. With the right one, you will be able to do all the tasks above plus work with a variety of graphical tools, create your own complex programs, and even do some debugging.




幸运的是，这些编程语言所用的大多数 IDE 都可以免费下载和使用，因此你不需要花太多钱就能把它们搭建起来。在本书中，我会使用 Code Blocks IDE 来运行 C 语言，不过你也可以根据自己希望用代码实现的目标，选择其他不同的工具来帮助你。

Code Blocks IDE 是最好的选择之一，因为它具备你需要的所有功能。你不需要再去网上寻找编译器或其他组件来帮助你编写代码，因为它们已经整合在一起。你可以访问下面的网站下载 Code Blocks：http://www.codeblocks.org

只要安装好合适的 IDE，你很快就能使用 C 语言并写出一些代码。无论你是有编程经验，还是刚刚开始学习，我都会带你一步步完成用 C 语言编写优秀代码和项目所需的步骤。

## 第 2 章：使用 C 语言编写第一个项目的基础

使用 C 语言相当简单。你可以只写一行代码，也可以继续写出较长、更复杂的代码，让它运行游戏或其他处理流程。虽然之后你可以编写更复杂的代码，但我先介绍 C 语言中的一些基础写法，帮助你熟悉起来。

### 编写一个示例代码

首先，我们来看看如何编写示例代码。它不会像之后讨论的某些代码那样产生输出，但能帮助你掌握如何用 C 语言创建和保存代码，从而为后面要做的内容做好准备。

开始时，你需要进入 Code Blocks IDE，或你选择的任何其他 IDE，然后点击“新建”按钮。你需要打开一个“空文件”。接下来，你需要在编辑器中输入代码，以便创建并保存一个代码文件。我会保持简单，只输入一行，如下所示：

```
main() {}
```

现在，你需要保存源文件，点击“保存”按钮即可。你可以将其保存到计算机的默认位置，也可以选择你希望将所有代码文件保存在计算机上的文件夹；选择权在你手中，只要记住保存位置，以便以后需要时可以找到它们。

请务必将文件命名为以后能记住的名称，否则随着时间推移，文件越来越多，你会感到混乱。我会把这个文件命名为 `dummy.c`。保存后，源文件就已创建并保存在你的计算机上。现在，你可以点击“构建”按钮。

书。

### 函数

函数在这种语言中非常重要，其中许多函数都位于 C 语言的库中。函数会把代码连接起来，从而构成你想要的程序。当你想在自己的程序中创建或使用函数时，需要加入一个头文件，该头文件会定义这个函数。函数能实现的事情非常多，我稍后会给出一些例子，展示函数可以有多强大。

### 运算符

运算符会在代码中用于处理程序内部的数据。运算符有多种类型，它们会根据你的使用方式以不同方式工作。C 语言中最常见的一些运算符包括：

- 数学运算符：包括你在代码中进行加、减、除、乘所需的各种符号。
- 比较运算符：这类运算符让你能够在代码中比较不同的值或信息，以判断语句为真还是为假。
- 赋值运算符：赋值运算符让你可以更方便地在代码中为变量赋值。

### 变量和值

变量和值彼此相似，但也有一些区别。值可以包含数值和字符，你也可以让它们包含任何想要的内容。例如，数值可以是分数、小数，也可以是非常小或非常大的数字。至于字符，你可以使用一个字母、一个完整的句子，甚至更多内容，具体取决于你想让代码实现什么。

现在我已经花了一些时间解释代码编写的基础部分，接下来我们把前面的 `dummy.c` 程序拿出来，看看这实际上是如何运行的。只需打开你之前保存该代码的位置即可；我会把 `main` 函数定义为一个整数函数。这基本上意味着它会向操作系统返回一个整数值。我们需要做一些编辑才能实现这一点。

在编辑器中，你需要在 `main` 前面加上关键字 `int`，以确保得到你想要的整数输出。请确保这两个词之间留一个空格，以便编译器能够分别读取它们。那么，先输入下面的代码：

```c
int main()
{
}
```

你会发现这段代码与我们最初写出的第一段代码有些不同，但这种花括号写法是大多数经验丰富的程序员更喜欢使用的。现在，是时候在这个 `main` 函数中添加一条语句，让它真正显示输出。我会保持简单，只添加数字 3。

你首先需要输入 `return`，然后输入数字 3。下面给出实现这一点的语法示例：

```c
int main()
{
    return(3);
}
```

记得在语句后面加上分号。保存文件，然后点击“构建”按钮。只要你按照我上面的代码输入，就不会出现错误或提示信息。接着点击“运行”按钮。

在使用 Linux 或 Mac 系统时，你很可能看不到除构建日志以外的输出，日志会显示程序以状态 0 终止。在 PC 电脑上，终端窗口会显示返回值 3。

任何时候想让示例程序产生输出，你都需要引入输出函数。C 语言中的关键字不会输出任何内容，因为它们只是基本词汇，例如 `int` 和 `return`。你可以通过程序中的 `puts` 命令来实现输出。

我们来看看写下一些代码后它会如何运行。请确保 `puts` 函数位于括号内，并把一段文本放在双引号中，这样才能正常工作。下面是我要使用的示例：

```c
int main()
{
    puts("I am the King of the C programming world");
    return 3;
}
```

当你保存这段源代码并点击“构建”时，计算机上应该会出现一条警告。即使没有看到，你也需要知道，此刻还有另一个步骤要做。在 `puts` 函数正常工作之前，它必须有定义，否则编译器会感到困惑。`puts` 的定义位于 I/O 头文件中，你需要借助预处理器指令把它放入源代码。

下面是一个示例，展示它在代码中如何呈现，以保持结构清晰并避免错误。

```c
#include<stdio.h>

int main()
{
    puts("I am the King of the C programming world");
    return 3;
}
```

这个版本包含了预处理器指令以及 `puts` 函数的定义。你可以保存文件，然后点击编辑器顶部的“构建”和“运行”按钮。如果所有内容都输入正确，你就可以避免错误；在输出终端窗口中，你为 `puts` 函数写入的语句以及数字 3 都会显示在屏幕上。

学习 C 语言的一些基础编写方法，可以让你更容易理解其中的原理。我展示了在使用 C 语言时可以使用的几个选项，但你能做的事情还有很多。花些时间熟悉这些代码的运行方式，多尝试 IDE 和编译器，在继续编写更复杂的代码之前先让自己适应。




## 第三章：C 编程语言中的条件语句

在大多数情况下，当你编写代码时，程序会按照代码中出现的顺序逐行执行语句。但有时你会想要改变程序的流程。if 语句是改变程序流程顺序最简单的方法之一，它使程序能够为你做出决策，而不是仅仅逐行读取代码。

本章中，我们将花一些时间研究 if 关键字，并学习 C 语言内部是如何进行不同比较的，以便编译器能够根据你放入代码中的内容以及用户输入到系统中的内容处理多个决策。

### 比较运算符

我将讨论的第一部分是如何在 C 语言内部实现比较。在进行比较时，程序会评估两个表达式或值。为了进行这些评估，你可以使用该语言中提供的一些比较运算符。一些常见的比较运算符包括：

- (!=): 这表示不等于
- (>=): 这表示大于或等于。
- (<=): 这表示小于或等于。
- (<): 这表示小于。
- (>): 这表示大于。
- (==): 这表示等于。

现在我们已经学习了一些最常见的比较运算符，是时候通过以下示例看看它在代码中是如何工作的了。

```c
#include <stdio.h>
int main()
{
    int a;

    printf("Type an integer:");
    scanf("%d", &a);
    printf("You typed %d. \n", a);
    if(a > 10)
    printf("%d is greater than \n", a);

    return(0);
}
```

在此示例中，用户将被提示输入其整数值。第 9 行显示的值，然后当你到达第 10 行时，if 语句将评估该值。如果它确定该值高于 10，则第 11 行将被执行。但如果该值低于 10，则第 11 行将被跳过。花点时间构建然后运行此代码以设置它。

完成之后，输入你想要的任何值。我将使用数字 45。当你将此数字输入代码时，它将起作用，编译器将显示第 11 行的 printf 语句。但如果我选择像 5 这样的数字，第 11 行及其对应的语句将被跳过，程序将终止。

### If 语句

我上面稍微谈到了 if 语句在代码中如何工作。大体上，if 语句的格式与其他我们将要处理的语句略有不同。它将被拆分为至少两行。第一行将把 if 条件放在括号中。如果它评估条件并发现为真，则下一行将被执行。它基本上只是一个被分成两行的语句，因此分号将与语句的第二部分一起，而不是在第一部分之后。

现在，如果你愿意，可以将 if 语句写在一行中，但这不是常见的编程礼仪，通常当它们被分成两行或更多行并用括号括起来时，代码更易于阅读。

你也可以选择在代码中加入多个 if 语句。这允许你根据设定的条件和用户提供的输入在代码内部执行几件事。以下是一个很好的示例，你也可以在程序中尝试：

```c
#include <stdio.h>
int main()
{
int a;
printf("Type an integer: ");
scanf("%d", &a);
printf("You typed %d.\n", a);
if(a > 10)
{
printf("%d is greater than\n", a);
}
if(a < 10)
{
printf("%d is lesser than\n", a);
}
return(0);
}
```

通过这段代码，我们可以看到有两个 if 比较语句紧挨着。它们各自都有自己的括号，并且将评估两个不同的条件；一个检查大于，另一个检查小于。花点时间构建并运行此代码。

运行代码后，你会看到根据输入的值，对于大于 10 或小于 10 的值，将显示必要的输出。请注意，使用此选项时，当你输入数字 10 时不会显示输出，只有当你输入大于 10 或小于 10 的数字时才会显示。你可以在第 16 行将其改为“小于或等于 10”，以便更改此问题并在你使用数字 10 时获得输出。

### Else 语句

虽然 if 语句可以帮助在 C 语言中添加一些比较，但你也可以使用 else 语句来帮助你。这些对于你想要创建的二选一决策非常有用。看看下面的代码，了解 else 语句如何在你的代码中工作：

```c
#include <stdio.h>

int main()
{
    int a;

    printf("Type an integer: ");
    scanf("%d", &a);
    printf("You typed %d. \n", a);
    if(a > 10)
    {
        printf("%d is greater than \n", a);
    }
    else
    {
        printf("%d is less than or equal to 10. \n", a);
    }

    return(0);
}
```

上面的代码基本上是对我们之前使用的代码的重写，但我们添加了 else 语句。在第 10 行，我们使用了 if 条件来进行评估。如果该条件被评估为真，则该语句将被执行。如果条件被评估为假，则代码中 else 部分的语句将被执行。花点时间构建并运行此代码，并尝试几个输入以查看其工作原理。

请注意在这段代码中我没有使用分号，而是使用了大括号。你可以不使用括号将所有内容写出来，因为只有一个语句，但这是一种很好的写法，以确保所有内容保持在一起，并且是良好的编程实践。

### Else If 语句

有时你会在代码中使用至少三个，如果不是更多的话，你想要使用的条件。在这些情况下，你需要比 if 和 else 语句稍微不同的东西。这时我们将使用 else if 语句的结构。让我们看看以下代码，了解 else if 语句的工作原理。

```c
#include <stdio.h>

int main()
{
    int a;

    printf("Type an integer: ");
    scanf("%d", &a);
    printf("You typed %d. \n", a);
    if(a > 10)
    {
        printf("%d is greater than \n", a);
    }
    else if(a < 10)
    {
        printf("%d is less than or equal to 10. \n", a);
    }
    else
    {
        printf("%d is 10, \n", a);
    }
    return(0);
}
```

使用此结构，你可以从第 10 行的 if 语句开始。如果此条件为真，则与其关联的语句将被执行。如果该语句被评估为假，它将继续到第 14 行检查的 else if 语句。如果此条件最终被评估为真，则该语句将被执行，其余所有内容将被跳过。最后是 else 语句。如果上面两个条件都不满足，则执行此语句。

好的一点是你可以添加任意多个 else if 语句。这使得系统能够根据你设定的条件和用户输入到系统中的输入，更容易评估复杂情况。

### Switch 语句

在 C 语言内部，你可以使用 if 和 else 条件来处理复杂的决策。你可以根据需要向系统添加任意多个这些条件来处理此问题，但代码中涉及的条件越多，代码可能变得越难看，写起来也越困难。不要处理这个问题，你可以使用 switch case 结构，它也可以帮助你在 C 语言中做出更多决策，而不会有所有混乱。让我们看看以下代码 to see

### switch 语句示例

```
#include <stdio.h>

int main()
{
    char a;
    printf("Your choice (1,2,3): ");
    scanf("%c", &a);
    switch(a)
    {
    case '1':
        puts("Excellent choice!");
        break;
    case '2':
        puts("This is the most common choice:");
        break;
    case '3':
        puts("I question your judgment.");
        break;
    default:
        puts("That's not a valid choice:");
        break;
    }
    return(0);
}
```

这段代码的大部分都放在 switch/case 结构中。它从第10行开始作为一个 switch 语句，然后是一系列 case 语句，每个 case 语句都有自己的语句（你可以根据正在编写的代码，以任何喜欢的方式更改这些语句）。switch case 也有自己的语句，然后是一个右花括号。所有这些都是 switch/case 结构附带的重要元素。

你可能已经注意到，它内部有 break 关键字。因此，这个结构内部共有四个关键字，包括 break、default、case 和 switch。把它放进编译器，然后运行几次，选择不同的选项，看看输出是什么，以及你是否正确放置了代码中的所有内容。

那么这一切是如何工作的呢？switch 语句处理的是单个值，而不是整个比较。它可以保存一个数学表达式，但结果最终必须只是一个值。然后，由 switch 指定的这个值会与每个 case 语句的值进行比较。如果发现比较结果为真，属于该 case 语句的语句就会被标记出来并执行。那些不被视为真的语句则会被跳过。

例如，如果用户在第12行输入数字1，那么第13行中的 puts 语句就会被执行，其余语句则被跳过。但如果他们选择数字2，你会看到第一个 case 被跳过，转而执行第二个 case，以此类推，直到找到为真的那个。

如果用户输入的值由于某种原因不匹配任何 case 条件，你的代码就会转到 default 条件。在这个例子中，如果用户输入数字4，它就会跳到 default 并执行随附的代码。

你可以把它用于任何允许用户输入某些内容的代码，比如菜单功能。这给了他们一些选择，而你可以教代码根据用户给出的答案或输入进行交互。只要他们给出的是 switch 语句允许的答案，他们就会看到你放入的正确答复！

## 第4章：在C语言中使用循环

循环可以是为C语言代码增添的有用内容。它们允许你在代码中创建事物列表，甚至创建图形和图表。它们很好用，因为只需几行代码，你就能完成一个巨大的图表，而不必试图把沿途需要的每一行都打出来。例如，如果你想制作一个从1到100的图表，逐行写出来可不太有趣，但使用合适的循环语句，你只需要几行就能做到。

循环是你在C语言代码中进行比较的另一种方式，而且有几种循环选项可以真正为你的代码增添力量。while 循环、嵌套循环和 do/while 循环是你可以使用的最常见类型，但本章中我也会花一些时间讨论 for 关键字。

### while 循环

循环将是一种非常重复的控制程序执行方式。你可以指定让该循环重复的条件，以及你希望在代码中重复的一组语句，还有让循环停止的方法。如果你忘记加入停止循环的部分，程序基本上会一直运行下去并使计算机卡死，所以一定要加入这一部分。

下面是一个代码示例，它将使用 while 循环让代码从1数到10。

```c
#include <stdio.h>

int main()
{
    int x;
    x = 1;
    while(x <= 10)
    {
        printf("%d\n",x);
        x++;
    }
    return(0);
}
```

循环条件显示在第8行，它表示当变量的值小于或等于数字10时，只要条件最终为真，循环内部的语句就会继续重复。第11行显示 x 的值将会递增，因此每次执行循环时它都会增加1，直到 x 的值大于10。当你构建并运行这段代码时，你将能看到数字1到10的显示。

你可以对此进行更改，以获得任意多个 while 循环。例如，假设你希望代码数到20。你只需要转到 while 语句所在的部分，更改你想使用的数字。你也可以更改希望递增的步长。上面的代码设置为 x = 1，所以它只是增加1，但你可以把这个变量改成任何你想要的值，比如以2或5为步长计数，以获得你想要的结果。

### do/while 循环

在进行循环时，你还有另一个选项，那就是 do/while 循环。它类似于 while 循环，但几乎就像是倒过来的版本。对于 while 循环，代码会检查条件是否为真，如果为真，然后才执行。对于 do/while 循环，代码会先执行一次，然后检查条件是否满足，再决定是否再次运行。如果你想确保语句至少运行一次，do/while 循环就是最适合你的选项。让我们看看下面的代码，了解 do/while 代码如何工作。

```c
#include <stdio.h>

int main()
{
    char ch;
    ch = 'A';
    do
    {
        putchar(ch);
        ch++;
    }
    while (ch != 'z');
    putchar('\n');
    return(0);
}
```

你会注意到，do/while 循环从第9行的语句“do”开始。这一个没有条件，因为这些语句会一个接一个地执行。然后你可以看到，while 条件会出现在第14行。该循环将依赖 ch 变量作为条件，它首先在第7行初始化，然后在第12行被修改。花点时间在编译器中构建并运行这段代码。

在这段代码中，'z' 不会被打印出来，因为它被视为退出条件。如果你希望在代码中看到 'z'，你需要将代码末尾的退出条件设为 'z+1'。这样一来，你基本上创建了一个无限循环，因为它带有一个加一。如果你构建并尝试运行这个版本，你最终会陷入无限循环，需要按 Ctrl + C 才能退出程序。

有时你确实会想要使用无限循环，但作为初学者，你很可能会无意中遇到这种情况。可以通过在代码中添加 break 语句来修复无限循环。这里我们将把 break 语句正好插入到代码的第8行，如下所示：

```c
#include <stdio.h>

int main()
{
    while(1)
    {
        printf("I'm endlessly looping!");
        break;
    }
    return(0);
}
```

现在保存、构建并运行代码。由于其中加入了 break 语句，循环只会运行一次，而不是一直反复循环。如果你愿意，甚至可以使用这个 break 代码来让循环提前跳出。

基本上，while 循环和 do/while 循环非常相似。对于 while 循环，你会让代码检查条件是否满足，如果为真，语句或循环就会执行。另一方面，do/while 循环至少会执行一次，先执行，然后判断条件是否为真，再决定是否反复循环。你可以用同样的方式使用它们，但如果你想确保循环至少发生一次，就应该选择 do/while 循环。

### for 循环

当你想在代码中创建循环时，for 关键字是一个很好用的关键字。



与使用 while 循环不同，for 循环只需一行就能完成，这确实让它用起来稍微隐晦一些，但它仍然是一种更流行、更传统的循环类型。一个很好的例子如下：

```c
#include <stdio.h>

int main()
{
    int x;

    for (x = 0; x < 10; x++)
        printf("%d\n", x);

    return(0);
}
```

你看到的第一部分是初始化，即语句 x=0，这是在循环开始时进行的赋值。这段代码中的第二项是循环条件。循环会继续重复，直到该条件不再为真；在这个例子中，就是直到 x 等于 10。最后，你会注意到迭代语句。每当循环重复自身时，这个特定的语句都会被执行。

分号不会跟在 for 语句的圆括号后面，而是会跟在单个循环语句后面，也就是第 8 行花括号内的那条语句。花点时间构建并运行这段代码。按照现在的设置，代码会从 0 开始一直到 9，然后一旦到 10 循环就会停止，因为此时条件不再为真。在这个程序中，除非你另行指定，否则程序会从 0 而不是 1 开始计数。

由于大多数时候你会希望从 1 开始计数，因为这是大多数人习惯的方式，你会转到第 8 行，把 x 改成 x+1。这不会改变 x 的值，但会影响输出结果。请务必保存、构建并运行这段代码，看看它会给你带来什么结果。

### 嵌套循环

for 循环对于清理一些代码编写工作真的很有帮助，而且在你处理所谓的嵌套循环时也能帮上忙。嵌套循环一开始听起来可能很复杂，但它比 while 循环更容易使用。让我们通过下面的代码来看看如何使用嵌套循环：

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main()
{
    int column, r;
    srand((unsigned)time(NULL));       /*Seed Randomizer*/

    for (column = 0; column < 10; column++)
    {
        r = rand();
        printf("%2d\t", r % 100);
    }
    putchar('\n');

    return(0);
}
```

我上面放出的代码会输出十个随机选择的数字。花点时间构建并运行这段代码，然后你会看到输出中有一行十个随机选择的值。这些值之间的间距将通过使用我们在第 14 行用到的 ‘\t’ 字符来实现。

这只是使用嵌套循环时所能做到的事情之一。你还可以用它来制作 1 到 100 或更多数字的网格，并在图表中加入各种你需要的不同项目。这比单独写出每个部分要快，而且完成后确实能做出不错的最终成果。

## 第 5 章：C 编程语言中的变量

正如我之前稍微提到过的，变量将成为代码中不同数据类型的容器。变量，或者说容器，能够保存浮点值、字符、整数或其他值。在本章中，我将进一步解释变量，以及如何在 C 语言代码中使用它们，并说明它们如何工作。

那么，如何区分变量和值呢？值几乎可以是代码中的任何东西，比如整数、字符，或代码中可以定义的其他东西。另一方面，变量将是把这些数据类型放在一起的容器。通常它们必须有某种东西把它们联系起来，但它们不必完全相同。例如，你可以有一个包含学校用品的变量，比如铅笔、钢笔、纸、粉笔、笔记本等等。这些东西在某个方面是相似的，放在一起也说得通，但它们并不完全相同。

当你在 C 语言中声明一个变量时，你会了解变量的类型和变量的名称。让我们先看看如何声明一个整数变量：

```c
#include <stdio.h>

int main()
{
    int a;

    printf("The value of a is %d\n", a);

    return(0);
}
```

在这个例子中，整数变量类型是 "int"，它的名称是 a。上面代码中的变量从未被赋值，但即使从未给它赋值，你仍然可以在代码中使用它，就像第 7 行所示那样。快速构建并运行这个程序。在你那边，可能会看到一个随机值出现。与你可能遇到的其他一些语言不同，C 语言不会在声明变量时初始化它们。在内部，程序会分配一块内存来存储该变量的信息。

在这种情况下，这块内存尚未被初始化，但也没有被设置为零。它只是被放在你内存中的某个位置。无论那里已经放了什么值，都会被变量立即接收，你会在屏幕上看到它作为输出。这背后的意思是，你需要在尝试使用变量之前先初始化它。解决这个问题的一个好方法是使用以下代码：

```c
#include <stdio.h>

int main()
{
    int a;

    a = 65;

    printf("The value of a is %d\n", a);

    return(0);
}
```

保存这些更改，然后构建并运行程序。现在代码的输出更加可预测，因为你知道变量的值。

除了知道变量的名称和值之外，你还可以在这种语言中了解关于变量的其他一些信息。其中之一就是 sizeof 运算符。

`sizeof` 是 C 语言中的关键字之一，但它也被视为运算符。sizeof 关键字的作用是返回该变量使用了多少字节的存储空间。这似乎不太重要，但当你在使用 C 语言时，它会派上用场，有时你会需要知道这些信息。下面是一个如何在代码中使用 sizeof 关键字的示例：

```c
#include <stdio.h>

int main()
{
    int a;

    printf("An int variable occupies %lu bytes of storage\n", sizeof(a));

    return(0);
}
```

在这个示例中，变量 a 没有被初始化，但由于它没有被使用，所以这不是大问题。sizeof 运算符出现在 printf 语句内部，它只是把变量 a 作为 int 变量进行求值，以返回计算机上占用了多少存储空间。你将得到的输出是一个长无符号整数值。你可以通过修改一些代码来反映这一点，从而改变你想获取的信息，比如查询一个字符会占用多少空间，而不仅仅是变量。

你还可以了解关于变量的另一件事，那就是内存位置。这会具体告诉你变量的数据位于哪里。要获取有关内存位置的信息，你需要使用和号运算符。下面是一个很好的代码示例，你可以用它来实现这一点：

```c
#include <stdio.h>

int main()
{
    int a;
    char b;
    float c;

    puts("memory location:");
    printf("A is at %p\n", &a);
    printf("B is at %p\n", &b);
    printf("C is at %p\n", &c);

    return(0);
}
```

这段代码中声明了三个不同的变量：浮点值、字符和整数。这些变量在这段代码中没有被初始化，因为它们没有被使用，但程序仍然会在内存中的不同位置为它们分配一些空间。为了访问这些位置，需要在变量名前加上和号。你需要在 printf 语句中使用 %p 占位符，才能得到你想要的结果。

你将收到的输出值会因所使用的机器而异。甚至格式也可能因所使用的操作系统而变化。计算机负责分配内存中的位置，这有时取决于你系统上可用的内存量，或者系统决定把它放在哪里。了解信息存储在计算机上的哪里，此时可能看起来有点微不足道，但它可以让你之后更容易找到东西并处理代码。

使用变量可以帮助你在代码中正确存储信息。你可以给变量赋予任何你想要的值，你只需要注意在编写的代码中初始化它，并确保它与变量中存储的所有其他数据类型相容。



## 第 6 章：编写代码时函数的基础知识

像许多其他编程语言一样，C 语言包含一个库。作为编程初学者，你会发现这个库是你最好的朋友。它让你能够浏览并找到代码中的一些函数，也就是代码的骨架，从而帮助你写出你希望发生的事。它可以向编译器发出命令，帮助你设置代码，还有更多功能。

C 语言库中有许多你可以使用的函数，这些函数将帮助你完成不少事情。话虽如此，它们并不能做所有事情，有时你需要在这种语言中自己编写一些函数。事实上，许多使用这种语言工作了一段时间的程序员已经创建了许多自己的函数，来帮助代码正常运行。

在本章中，我会花一些时间讨论函数，包括如何设置函数、如何为它编写原型、如何调用或访问你想要的任何函数，甚至如何在需要时提前退出函数。在 C 语言中，函数会有类型、名称，以及放在圆括号中的参数。名称将是唯一的，并应用于标识你正在使用的函数。参数是零个、一个或多个值，它们会被传入函数，也被称为输入。

下面我给出了 alpha 函数，它没有输入也没有输出；这在 C 语言中是合法的。这种类型将被称为 void 函数，如下所示：

```
void alpha(void)
```

void 是变量类型，它基本上告诉编译器你没有变量类型。count 函数是整型函数，它负责生成或返回某种整数值。它需要比上面更多的输入，因此它没有任何参数。它看起来会是这样：

```
int count(void)
```

你还可以对函数做的另一件事是 hangup 函数，它将不返回任何值，所以它也是一个 void 函数。然而，这个函数略有不同，因为它确实接受单个字符作为输入，你可以选择将该字符作为参数。在 C 语言中，它将通过“ch”变量来引用。不过，在你能够使用函数之前，无论你使用哪种类型，都需要向编译器介绍它，并让编译器检查参数，以确保一切都使用正确。

当你想要调用函数时，你会通过名称调用它，然后使用圆括号。当函数被调用时，控制权会传递给该函数的语句。一旦函数全部结束，流程将继续执行函数调用之后的语句。让我们快速看看函数在代码中如何工作。下面的代码将包含两个函数来帮助说明这一点：

```
#include <stdio.h>

void blorf(void);

int main()
{
    puts("the main () function always runs first");
    blorf();
    puts("thanks, blorf()");

    return(0);
}
```

main 函数同样是 C 语言中所有代码都需要的函数。你还会注意到有一个 blorf 函数，这对系统来说是新的。在第 3 行，你正在为函数编写原型，并将函数参数和类型告知编译器。然后，编译器可以通过检查原型来确认你在代码中正确使用了该函数。而且由于原型是一条语句，它会像其他语句一样以分号结束。

然后我们继续看第 8 行，它将调用该函数。由于这个函数没有参数，圆括号将保持为空。函数本身直到第 14 行才会出现。这实际上是在重复原型，只是没有分号。属于这个特定函数的语句将位于花括号内。现在，花几分钟构建并运行这段代码，看看它是如何工作的。

现在假设你想再次调用该函数。这很简单，因为你只需要将第 8 行复制到第 9 行，它就会再次重复自身。因此，新代码看起来会是这样：

```
#include <stdio.h>

void blorf(void);

int main()
{
    puts("the main () function always runs first");
    blorf();
    blorf();
    puts("thanks, blorf()");
    return(0);
}
```

当你再次保存并运行代码时，你会看到这段输出会出现两次。

代码中的原型作用类似于函数的定义，基本上是在函数出现在代码中之前，向编译器描述它将如何被使用。有时你不需要指定原型；只有在你于使用函数之前写出函数时，这种做法才有效。下面是一个很好的例子：

```
#include <stdio.h>

void soup(void)
{
    puts("Pea green soup!");
}

int main()
{
    printf("For breakfast I had");
    soup();
    printf("For lunch I had");
    soup();
    return(0);
}
```

在这段代码中，soup 函数会出现在 main 函数之前。这只是因为编译器仍然会在函数内部看到它们，而 main 始终是程序中第一个被执行的函数。这个示例中缺少的是 soup 函数的原型。也花点时间构建并运行这段代码。

现在我将展示另一个你可以使用的示例，它允许你在需要时使用 return 关键字提前退出函数。当你处理循环或代码中其他持续进行、而你想提前停止的事情时，就可以使用它。查看第 26 行的 return，了解它是如何工作的：

```
#include <stdio.h>

void cheers(void);

int main()
{
    int x;
    x=21;
    puts("Everyone gets free dinner!");
    cheers();
    puts("Everyone gets free dessert!");
    cheers();
    printf("%d\n", x);
    puts("Everyone pays higher taxes!");
    return(0);
}

void cheers(void)
{
    int x;
    for(x=0;x<3;x++)
        printf("Huzzah!");
    return;
    putchar('\n');
}
```

在这个示例中，你不必指定值，因为 cheers 函数被视为 void 函数，意味着它不会返回任何内容。在 main 函数中，第 17 行的 return 需要指定一个值，就像这个示例中那样，因为 main 被视为 int 函数。保存这个示例的更改，然后构建并运行代码。

这个示例的输出可能有点乱，因为你的 putchar 语句被跳过了。然而，由于紧挨在它上面的 return 语句，这段代码永远不会被执行。更常见的是看到函数基于条件提前返回，这通常会用循环或 if 语句来体现。否则，如果你看到 return 函数，这里就是函数退出的位置，控制权将回到调用该函数的地方。

在代码中使用函数的方式有很多。只要你正确定义它们，它们就能帮助编译器了解代码内部发生了什么；虽然 C 语言库中已经有许多可用函数，但你也有能力创建一些自己的函数。请记住，在这种语言中使用函数之前必须先定义它们，否则编译器会搞不清楚你想做什么，并且通常会发出错误消息。总的来说，这些函数让你在代码中能够创建的内容方面拥有很大的自由。

## 结论

感谢你读到最后，完成《C 编程入门：速成课程——终极版》；希望它富有信息量，并能够为你提供实现目标所需的所有工具，无论你的目标是什么。

下一步是开始写出一些你自己的代码。你可以尝试本指南中提供的一些代码，或者使用我们讨论过的提示和技巧，来编写适合你自己需求的代码。

作为初学者，你可能会担心编写代码过于复杂，但 C 编程语言让这件事真的很容易处理。它也是许多较新编程语言的基础，因此你可以使用这些技巧将它们整合起来，并在未来学习其他编程语言，这样入门就不必显得那么令人生畏。

在本指南中，你将了解 C 编程语言可以多么简单。我们将讨论这种语言的许多不同部分，包括 C 语言的历史、这种语言代码中的一些基础部分、如何在 C 语言中处理比较，甚至如何处理不同类型的循环以及更多内容。当你读完时，你将能够使用 C 语言创建一些基本代码，并且你会有信心继续工作并创建一些自己的程序。

当你准备好进入编程世界，并想学习如何制作一些自己的代码和项目时，请翻阅本指南，了解 C 编程语言如何让这一切成为可能。

最后，如果你觉得这本书在任何方面有用，我们始终感谢你在亚马逊上留下评论！



### 附录

C 编程语言可能已经存在一段时间了，但它是你可以使用最好的语言之一。这种语言是首批开发的语言之一，使人们学习编程变得更容易，与过去的一些其他编程语言相比，具有更高的效率和良好的可读性。

在本指南中，你将学习开始使用 C 编程语言所需了解的一些基础知识。无论你是对开始学习一种新的编程语言以丰富你的技能感兴趣，还是第一次入门，本指南都将帮助你完成最初的代码编写，以获得你想要的结果。

在本指南中，你将学习有关 C 编程语言的以下内容。

- C 语言起源的开始
- 使用这种语言编写你的第一个项目的[content]
### 参考文献

C 编程语言可能已经存在一段时间了，但它是你可以使用最好的语言之一。这种语言是首批开发的语言之一，使人们学习编程变得更容易，与过去的一些其他编程语言相比，具有更高的效率和良好的可读性。

在本指南中，你将学习开始使用 C 编程语言所需了解的一些基础知识。无论你是对开始学习一种新的编程语言以丰富你的技能感兴趣，还是第一次入门，本指南都将帮助你完成最初的代码编写，以获得你想要的结果。

在本指南中，你将学习有关 C 编程语言的以下内容。

- C 语言是如何开始的起源
- 使用这种语言编写你的第一个项目的基础
- C 语言中的语言比较是如何工作的
- 使用循环在你的代码中节省时间
- 变量在这个编程语言中是如何工作的
- 在编写代码时函数的一些基础知识

当你准备好学习当今最好的编程语言之一，或想要了解其他编程语言的一些基础知识时，请务必阅读本书，了解更多关于 C 语言的知识，以及它如何能在你的项目中发挥作用！
