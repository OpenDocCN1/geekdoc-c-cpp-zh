

# 表 15.1 字符串和字符 I/O 方法（需要头文件 iostream）（续）

| C++ 方法 | 描述 | 示例 |
|---|---|---|
| cin.putback(charExp) | 将 charExp 的字符值推回输入流 | cin.putback(cKey); |
| cin.ignore(n, char) | 忽略最多接下来的 n 个输入字符，直到检测到 char 为止；如果未指定参数，则忽略输入流上的下一个单个字符 | cin.ignore(80,'\n');cin.ignore(); |

表 15.1 中列出的方法 cin.getline()、cin.get() 和 cin.peek() 用于输入。 （它们与为字符串类定义同名的方法不同。）字符输出函数 put() 和 putback()， however，是与字符串类相同的。

程序 15.1 显示了使用 cin.getline() 和 cout 在用户键盘上输入和输出字符串。

# 程序 15.1

```
#include <iostream>
using namespace std;

int main ()
{
    const int MAXCHARS = 81;
    char message [MAXCHARS]; // an array of characters with
    // enough storage for a complete line
    cout << "Enter a string:\n";
    cin.getline(message,MAXCHARS, '\n');
    cout << "The string just entered is:\n"
         << message << endl;

    return 0;
}
```

以下是程序 15.1 的一个示例运行：

```
Enter a string:
This is a test input of a string of characters.
The string just entered is:
This is a test input of a string of characters.
```

程序 15.1 中使用的 cin.getline() 方法会不断接受并将用户键盘上输入的字符存储到名为 message 的字符数组中，直到输入 80 个字符为止（第 81 个字符随后用于存储结束符 NULL 字符 '\0'），或检测到 Enter 键。按下 Enter 键会生成换行字符 '\n'，cin.getline() 将其解释为行结束符。cin.getline() 遇到的所有字符，除了换行字符之外，都存储在 message 数组中。在返回之前，cin.getline() 会在存储的字符集后附加一个 NULL 字符 '\0'，如图 15.2 所示。然后使用 cout 对象显示 C 字符串。

![](img/202cface8244f523c2641baa2e00d7dd_688_0.png)

# 图 15.2 使用 cin.getline() 输入 C 字符串

尽管程序 15.1 中使用 cout 对象进行 C 字符串输出，但 cin 对象不能用作 cin.getline() 的替代来输入 C 字符串，因为它在遇到空格或换行符时会停止读取字符。cin.getline() 方法的语法如下：

```
cin.getline(str, terminatingLength, terminatingChar)
```

str 是一个 C 字符串或指向字符的指针（在第 8 章中讨论），terminatingLength 是一个整数常量或变量，表示可以输入的最大字符数，而 terminatingChar 是一个可选的字符常量或变量，指定终止字符。如果省略此可选的第三个参数，则默认终止字符为换行符 '\n'。因此，语句

```
cin.getline(message, MAXCHARS);
```

可以用作以下较长语句的替代：

```
cin.getline(message, MAXCHARS, '\n');
```

两种方法调用都会在按下 Enter 键时停止读取字符，或在读取 MAXCHARS 个字符后停止，以先到者为准。由于 cin.getline() 允许指定输入流的任何终止字符，因此语句如 cin.getline(message, MAXCHARS, 'x'); 也是有效的。此语句在按下 x 键时停止接受字符。在所有后续程序中，假设输入以按下 Enter 键结束，这会生成换行字符。因此，传递给 getline() 的可选第三个参数，即终止字符，被省略。

# C 字符串处理

C 字符串可以使用标准库函数或作为下标数组变量进行操作。 （指针也可以使用，如第 15.2 节所述。）目前，重点关注使用下标以字符为单位处理 C 字符串。 （可用于使用的库函数也在第 15.2 节中讨论。）

作为一个具体示例，来看复制 string2 内容到 string1 的 strcpy() 函数：

```
// copy string2 to string1
void strcpy(char string1[], char string2[])
{
    int i = 0;                // i is used as a subscript

    while ( string2[i] != '\0' )  // check for end of string
    {
        string1[i] = string2[i];  // copy the element to string1
        i++;
    }
    string1[i] = '\0';           // terminate the first string
    return;
}
```

strcpy() 函数用于一次一个字符地将字符从一个字符数组复制到另一个字符数组。如所写，函数中的下标 i 用于通过“沿着字符串移动”一次一个字符的方式访问 string2 数组中的每个字符。当从 string2 数组访问每个字符时，它会被复制到 string1 数组。虽然此函数可以大大缩短并写得更紧凑，这在第 15.2 节中完成，但它确实说明了 C 字符串操作的主要特征：

- 使用下标访问数组元素（指针也可以使用）
- 使用结束符 NULL 字符来确定何时停止处理

在回顾 strcpy() 时，请注意两个 C 字符串作为数组传递给函数。然后将 string2 的每个元素分配给 string1 的等效元素，直到遇到结束符标记。对 NULL 字符的检测迫使控制复制元素的 while 循环终止。由于 NULL 字符未从 string2 复制到 string1，因此 strcpy() 中的最后一条语句会在 string1 后附加一个结束符字符。在使用 strcpy() 时，必须确保为 string1 数组分配了足够的空间以存储 string2 数组的元素。

程序 15.2 在一个完整的程序中包含了 strcpy() 函数。请注意，其函数原型声明它期望接收两个字符数组。

# 程序 15.2

```
#include <iostream>
using namespace std;

void strcpy(char [], char []); // function prototype

int main()
{
    const int MAXCHARS = 81;
    char message[MAXCHARS];    // enough storage for a complete line
    char newMessage[MAXCHARS]; // enough storage for a copy of message
    int i;

    cout << "Enter a sentence: ";
    cin.getline(message,MAXCHARS);    // get the string
    strcpy(newMessage,message);      // pass two array addresses
    cout << newMessage << endl;

    return 0;
}

void strcpy(char string1[], char string2[]) // copy string2 to string1
{
    int i = 0;                        // i is used as a subscript

    while (string2[i] != '\0')        // check for end of string
    {
        string1[i] = string2[i];      // copy the element to string1
        i++;
    }
    string1[i] = '\0';               // terminate the first string

    return;
}
```

以下是程序 15.2 的一个示例运行：

```
Enter a sentence: How much wood could a woodchuck chuck.
How much wood could a woodchuck chuck.
```

# 逐字符输入

正如 C 字符串可以使用逐字符技术进行处理，它们也可以以这种方式输入和显示。例如，来看程序 15.3，它使用字符输入函数 cin.get() 一次接受一个字符的字符串。程序 15.3 的阴影部分基本上替换了程序 15.1 中使用的 cin.getline() 函数。

## 1.1 认识三角形

三角形是生活中常见的图形。观察下图，你能发现哪些三角形？

![](img/202cface8244f523c2641baa2e00d7dd_691_0.png)

由不在同一条直线上的三条线段首尾顺次相接所组成的图形叫做三角形（triangle）。

如图1-1，线段AB，BC，CA是三角形的边，点A，B，C是三角形的顶点。∠A，∠B，∠C是相邻两边组成的角，叫做三角形的内角，简称三角形的角。

![](img/202cface8244f523c2641baa2e00d7dd_691_1.png)

图1-1

顶点是A，B，C的三角形，记作"△ABC"，读作"三角形ABC"。

△ABC的三边，有时也用a，b，c来表示。如图1-1，顶点A所对的边BC用a表示，边CA、边AB分别用b、c来表示。

# EXERCISES 15.1

- 1. **(Program)** a. 以下函数可用于选择并显示用户输入字符串中的所有元音：

```
void vowels(char strg[])
{
    int i = 0;
    char c;
    while ((c = strg[i++]) != '\0')
        switch(c)
        {
            case 'a':
            case 'e':
            case 'i':
            case 'o':
            case 'u':
                cout << c;
        } // end of switch
    cout << endl;
    return;
}
```

请注意，vowels() 中的 switch 语句利用了在没有 break 语句的情况下所选 case 会“贯穿”的事实。因此，所有所选 case 都会导致 cout 对象调用。将 vowels() 包含在接受用户输入字符串然后显示字符串中所有元音的工作程序中。对于输入 How much is the little cow worth?，你的程序应显示 ouieieoa。

- b. 修改 vowels() 以计算并显示传递给它的字符串中的元音总数。

- 2. **(Modify)** 修改练习 1a 中的 vowels() 函数以计算并显示字符串中每个元音的数量。

- 3. **(Program)** a. 编写一个 C++ 函数来计算字符串中的总字符数，包括空格。不要在计数中包含结束符标记。

- b. 将为练习 3a 编写的函数包含在完整的可用程序中。

- 4. **(Program)** 编写一个程序，从键盘接受一个字符串并显示每个字符的十六进制等价物。

- 5. **(Program)** 编写一个 C++ 程序，从键盘接受一个字符串并以每行一个单词的方式显示该字符串。

