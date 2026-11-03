
```c
5  printf("Here is a value: 27\\n");
6

7  return(0);
8 }
9

10

```

The *printf* function in line 5 of our sample code above generates an output that would have you believe that the number 27 was a value, but it is not. It is part of a string—just the characters 2 and 7. To specify a value, you need to do two things. First, you must place a value into the code—in this case the number
*printf* 函数在我们上面示例代码的第 5 行生成的输出会让你相信数字 27 是一个值，但它不是。它是字符串的一部分——只是字符 2 和 7。要指定一个值，你需要做两件事。首先，你必须将一个值放入代码中——在这种情况下是数字

- Second, you must direct the *printf* function to display that value.
- 其次，你必须指示 *printf* 函数显示该值。

Edit line five to replace the characters 2 and 7 with ‘%d.’ In some editors, you may see the %d highlighted. That is because it is a special symbol for the *printf* function. It is a placeholder. In this case, it is a placeholder for an integer value—a whole number. Place a comma after the string and add a second argument to the *printf* function: the value 27.
编辑第五行，用 ‘%d’ 替换字符 2 和 7。在某些编辑器中，你可能会看到 %d 被高亮显示。这是因为它是 *printf* 函数的一个特殊符号。它是一个占位符。在这种情况下，它是整数值——一个整数——的占位符。在字符串后加上一个逗号，并在 *printf* 函数中添加第二个参数：值 27。

Note how a value is shown in its own color in the Code Blocks editor. The printf function now has two arguments. The first is called the formatting string. It contains one placeholder, which is %d. Matching that placeholder is the second argument: the integer value 27. Your code should now look like this:
注意在 Code Blocks 编辑器中值是如何以自己的颜色显示的。printf 函数现在有两个参数。第一个称为格式化字符串。它包含一个占位符，即 %d。与该占位符匹配的是第二个参数：整数值 27。你的代码现在应该如下所示：

```c
1 #include <stdio.h>
3 int main()
4 {
5 printf("Here is a value: %d\\n", 27); 6
```

```c
7 return(0);
8 }
9

10

```

Now save, build and run the code. In the output, 27 represent the value 27. Its output is text, of course. But inside the program, it is a number and not text. Now, copy line five of our sample code in line 6 and then change the number to 29. Save, build and run your code.
现在保存、构建并运行代码。在输出中，27 代表值 27。当然，它的输出是文本。但在程序内部，它是一个数字而不是文本。现在，将我们示例代码的第五行复制到第 6 行，然后将数字改为 29。保存、构建并运行你的代码。

```c
1 #include <stdio.h>
3 int main()
4 {
```

- printf("Here is a value: %d\n", 27);
- printf("Here is a value: %d\n", 29); 7

```c
8 return(0);
9 }
10

11

```

As you can see, two lines are output. The same placeholder is used in both *printf* functions. However, because a different value is specified, the new value is output for the second statement. The %d placeholder is just that—it holds the place of another argument. In fact, you can specify multiple placeholders providing that you have arguments to match, just like in line 7 of the code below:
如你所见，输出了两行。两个 *printf* 函数都使用了相同的占位符。然而，由于指定了不同的值，第二条语句会输出新的值。%d 占位符就是这样——它为另一个参数占位。事实上，只要你有匹配的参数，你就可以指定多个占位符，就像下面代码第 7 行那样：

```
1 #include <stdio.h>

3 int main()
4 {
```

- `printf("Here is a value: %d\n", 27);`
- `printf("Here is a value: %d\n", 29);`
- `printf("Here are the values %d, %d, and %d\n", 51,52,53); 7`
- `return(0);`

```
9 }
```

You can even do math in a printf function. Although, it is the C language that does the math, not the printf function. Take a look at the code below:
你甚至可以在 printf 函数中进行数学运算。虽然进行数学运算的是 C 语言，而不是 printf 函数。看一下下面的代码：

```
1 #include <stdio.h>
3 int main()
4 {
5 printf("Everyone knows that 2+2=%d\n", 4); 6
7 return(0);
8 }
9

10

```

The *printf* statement employs a swath of placeholders, each for a specific type of value. Below is a partial list showing some of the more common placeholders:
*printf* 语句使用了一系列占位符，每个占位符对应一种特定的值类型。下面是一个部分列表，展示了一些更常见的占位符：

- `%d` Integer (whole number) values
- `%d` 整数值
- `%s` Strings
- `%s` 字符串
- `%f` Floating-point values or fractions
- `%f` 浮点值或分数
- `%c` Single characters
- `%c` 单个字符
- `%%` The percent sign
- `%%` 百分号

It helps to know about the different types of values in the C language before you can use each of these, as well as understand the whole lot of them that are not shown. Also, the placeholders have options that we’ll get into in the later chapters.
在你使用这些之前，了解 C 语言中不同类型的值是有帮助的，以及理解未显示的全部内容。此外，占位符还有选项，我们将在后面的章节中介绍。

The %s placeholder is used to display strings. It may look a little odd. However it does come in handy. Take a look at the code below:
%s 占位符用于显示字符串。它看起来可能有点奇怪。然而它确实很有用。看一下下面的代码：

```
1  #include <stdio.h>
3  int main()
4  {
5  printf("You are a %s\n", "programmer"); 6
7  return(0);
8  }
9

10

```

In this code, the %s placeholder represents the string "programmer," which is the second argument of the *printf* function. If you are following along, build and run the code above. Now, modify line five of the code above to add another placeholder and another argument to the *printf* function. Place %c before %s and squeeze a space between the two like so:
在这段代码中，%s 占位符代表字符串 "programmer"，它是 *printf* 函数的第二个参数。如果你跟着操作，构建并运行上面的代码。现在，修改上面的代码第五行，为 *printf* 函数添加另一个占位符和另一个参数。像这样在 %s 之前放置 %c 并在两者之间挤一个空格：

```
1  #include <stdio.h>
```

One final thing, because the percent character is used as a placeholder, you must specify two of them when you use a percent symbol in the *printf* statement’s formatting string. Take a look at the code below:
最后一点，因为百分号被用作占位符，当你在 *printf* 语句的格式化字符串中使用百分号时，你必须指定两个百分号。看一下下面的代码：

```c
1  #include <stdio.h>
3  int main()
4  {
5  printf("I got %d% on my C exam!\\n", 98);
7  return(0);
8  }
9

10

```

Read the *printf* statement in the code above. The %d placeholder should match up with the second argument, which is 98. It is followed by a percent sign, which indicates actual percentage, not a placeholder. Build and run this code. Now, if you don’t see any warnings, that’s okay. The output is still going to look weird. In some compilers, you will see warnings that indicate trouble.
阅读上面的代码中的 *printf* 语句。%d 占位符应与第二个参数 98 匹配。它的后面跟着一个百分号，表示实际的百分比，而不是占位符。构建并运行此代码。现在，如果你没有看到任何警告，那也没关系。输出仍然会看起来很奇怪。在某些编译器中，你会看到指示问题的警告。

The compiler believes that a second placeholder is desired. It does not understand the placeholder as presented. Plus, it can’t find a matching argument. If you don’t see the warning, try to run the code and see what happens.
编译器认为需要第二个占位符。它不理解所呈现的占位符。此外，它找不到匹配的参数。如果你没有看到警告，尝试运行代码看看会发生什么。

The solution is to edit line five and stick in another percent sign. It looks odd, and it is cryptic. It is the cryptic side of the C language, in fact, that enthralls so many of the nerds. However, it is going to work.
解决方案是编辑第五行并插入另一个百分号。它看起来很奇怪，而且很晦涩。事实上，正是 C 语言的这种晦涩之处吸引了许多极客。然而，它会起作用。

```c
1  #include <stdio.h>
3  int main()
4  {
```

```
5 printf("I got %d%% on my C exam!\n", 98); 6
7 return(0);
8 }
9

10

```

Save the changes, build and run. Now, the output looks more sensible.
保存更改，构建并运行。现在，输出看起来更合理了。

## Chapter 4: The C Language Variables
## 第 4 章：C 语言变量

Programs work fine with immediate values. But oftentimes, you don’t know what the value is. Say the value comes from input, the user types it. It is read from a file or the Internet. To store such values, you need a specific cubby-hole or container. In programming, that container is known as a variable. In this chapter, we introduce you to the concept of the variable. It is a container into which you can store values—values that are unknown or values that can change.
程序使用立即值工作得很好。但通常情况下，你不知道值是什么。假设值来自输入，用户输入它。它是从文件或互联网读取的。为了存储此类值，你需要一个特定的小隔间或容器。在编程中，该容器被称为变量。在本章中，我们向你介绍变量的概念。它是一个容器，你可以存储值——未知的值或可以改变的值。

You’ll see how to declare a variable in the C language, and how a variable is used in the code. A variable is a container for a value. Because C deals with different types of values, a variable must be declared as a specific type. It is given a name—a name that’s used in the code.
你将看到如何在 C 语言中声明变量，以及变量在代码中的使用方式。变量是值的容器。因为 C 处理不同类型的值，所以变量必须声明为特定类型。它有一个名称——在代码中使用的名称。

In C, the variable type matches the variable’s content—the type of value being stored. Integer variables can hold only integer values or whole numbers. Float variables hold floating-point values, which are very large numbers, very small numbers, or numbers with a fractional part.
在 C 中，变量类型与变量的内容相匹配——即存储的值的类型。整数变量只能保存整数值或整数。浮点变量保存浮点值，即非常大的数字、非常小的数字或带小数部分的数字。

Character variables hold single values such as the letter ‘x.’ The C language lacks a string variable type. Instead, a character array is used. We’ll discuss how that works in a later chapter.
字符变量保存单个值，例如字母 ‘x’。C 语言缺少字符串变量类型。相反，使用字符数组。我们将在后面的章节中讨论其工作原理。

int and char are all C language keywords. Additional keywords are also used to declare variables. These include double, long, short, signed, and unsigned. These are all C language keywords that are used to declare different types of variables. Take a look at the code below:
int 和 char 都是 C 语言关键字。声明变量还使用其他关键字。这些包括 double、long、short、signed 和 unsigned。这些都是用于声明不同类型变量的 C 语言关键字。看一下下面的代码：

```
1  #include  <stdio.h>
```

```c
3  int main()
4  {
5  int age;
6

7  age = 30;
8  printf("The C language is over %d years old!\n", age); 9
10 return(0);
11 }
```

This code declares an integer variable at line five. First comes the keyword int which is used to declare an integer variable. Next come the variable name: age. As this is a statement, it ends with a semi-colon. Variable names can include numbers, letters, and some symbols. They must begin with a letter, or an underline. The name must be unique, with no two variables having the same name, nor should variables have the same name as functions or C language keywords.
此代码在第五行声明了一个整数变量。首先是关键字 int，用于声明整数变量。接下来是变量名：age。由于这是一个语句，它以分号结束。变量名可以包含数字、字母和一些符号。它们必须以字母或下划线开头。名称必须是唯一的，不能有两个变量具有相同的名称，也不应将变量命名为与函数或 C 语言关键字相同。

At line seven, the variable *age* is assigned the value 30. In C, values or equations go on the right side of the assignment operator, the equal sign. The value or results of the equation is then assigned to the variable on the left. Because 30 is an integer value, it fits nicely into the integer variable
在第 7 行，变量 *age* 被赋值为 30。在 C 中，值或方程位于赋值运算符等号的右侧。然后将值或方程的结果赋给左边的变量。因为 30 是一个整数值，所以它很适合放入整数变量中

The statement at line nine displays the variable’s value by using the *printf* function. The %d placeholder is used, and the variable *age* is specified as the second argument. Now go ahead and build and run the code. The whole idea behind the variable is that its value can change. Edit the source code so that the value of the *age* variable is changed to 34. Make this modification at line seven.
第 9 行的语句使用 *printf* 函数显示变量的值。使用 %d 占位符，并将变量 *age* 指定为第二个参数。现在继续构建并运行代码。变量背后的整个思想是它的值可以改变。编辑源代码，将 *age* 变量的值改为 34。在第 7 行进行此修改。

```c
1  #include <stdio.h>
```
