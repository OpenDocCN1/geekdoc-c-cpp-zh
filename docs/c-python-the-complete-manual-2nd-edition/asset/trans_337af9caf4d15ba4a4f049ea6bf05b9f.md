

## C++ 输入/输出

![](img/2f9c26fcf758b5bc56897d9c75b6347f_113_0.png)

当你编写代码让用户输入，然后使用该输入产生用户可见的内容时，会有一种令人满意的感觉。即使只是询问某人的名字，并显示个性化的欢迎信息，这也是向前迈出的重要一步。

用户交互、字符字面量、定义常量以及文件输入和输出都将在以下页面中介绍。所有这些都有助于你更好地理解 C++ 程序的工作原理。

- 116 用户交互
- 118 字符字面量
- 120 定义常量
- 122 文件输入/输出

## 用户交互

没有什么比创建一个响应你的程序更令人满意的了。这种基本用户交互是任何语言中最常教授的方面之一，有了它，你就能做得远不止按名字问候用户。

### HELLO, DAVE

你已经在我们的代码中多次使用过 cout，标准输出流。现在你将使用 cin，标准输入流，来提示用户响应。

### STEP 1

你希望用户输入到程序中的任何内容都需要存储在系统内存中的某个位置，以便检索和使用。因此，任何输入都必须首先声明为变量，以便用户可以使用。先创建一个空白的 C++ 文件并添加头文件。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_115_0.png)

### STEP 2

变量的数据类型也必须与你希望从用户处获得的输入类型相匹配。例如，要询问用户的年龄，你会使用整数，如下所示：

```
#include <iostream>
using namespace std;

int main ()
{
    int age;
    cout << "what is your age: ";
    cin >> age;

    cout <<"\nYou are " << age << " years old.\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_115_1.png)

### STEP 3

cin 命令的工作方式与 cout 命令相反。第一个 cout 行将“what is your age”输出到屏幕上，如尖括号所示。Cin 使用相反方向的尖括号，表示输入。输入被放入整数 age 中，并在第二个 cout 命令中调用。构建并运行代码。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_115_2.png)

### STEP 4

如果你要提问，需要将输入存储为字符串；要询问用户的名字，你会使用：

```
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "what is your name: ";
    cin >> name;

    cout << "\nHello, " << name << " . I hope you’re well today?\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_115_3.png)

### STEP 5

原理与之前的代码相同。用户的输入，即他们的名字，被存储在一个字符串中，因为它包含多个字符，并在第二个 cout 行中检索。只要变量 'name' 不改变，你就可以在代码中的任何地方调用它

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_0.png)

### STEP 6

你可以将输入请求链接给用户，但只要确保一开始有有效的变量来存储输入即可。假设你希望用户输入两个整数：

```
#include <iostream>
using namespace std;

int main ()
{
    int num1, num2;

    cout << "Enter two whole numbers: ";
    cin >> num1 >> num2;

    cout << "you entered " << num1 << " and " << num2 << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_1.png)

### STEP 7

同样，一旦你将数据存储在变量中，就可以对其进行操作。例如，询问用户两个数字并对其进行数学运算：

```
#include <iostream>
using namespace std;

int main ()
{
    float num1, num2;

    cout << "Enter two numbers: \n";
    cin >> num1 >> num2;

    cout << num1 << " + " << num2 << " is: " << num1 + num2 << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_2.png)

### STEP 8

虽然 cin 对于大多数输入任务效果很好，但它确实有一个限制。Cin 总是将空格视为终止符，因此它设计用于单个单词而不是多个单词。然而，getline 将 cin 作为第一个参数，变量作为第二个参数：

```
#include <iostream>
using namespace std;

int main ()
{
    string mystr;
    cout << "Enter a sentence: \n";
    getline(cin, mystr);

    cout << "Your sentence is: " << mystr.size() << " characters long.\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_3.png)

### STEP 9

构建并执行代码，然后输入包含空格的句子。完成后代码会读取字符数。如果你删除 getline 行并用 cin >> mystr 替换它然后再试一次，结果会显示到第一个空格为止的字符数。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_4.png)

### STEP 10

Getline 通常是新 C++ 程序员忘记包含的命令。当你无法弄清楚为什么代码无法工作时，终止空白会很烦人。简而言之，最好以后使用 getline(cin, variable)：

```
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "Enter your full name: \n";
    getline(cin, name);

    cout << "\nHello, " << name << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_116_5.png)

## 字符字面量

在 C++ 中，字面量是一旦定义后在整个代码中保持不变的对象或变量。然而，字符字面量由反斜杠定义，例如你在 cout 语句末尾使用的 \n 来表示新行。

当在像 cout 语句这样的地方使用时，字符字面量也称为转义序列代码。它们允许你插入引号、警报、新行等。

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
}
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_117_0.png)

你已经体验过 \n 字符字面量在放置的位置放置新行。行：cout << "Hello\n" << "I'm a C++\n" << "Program!\n"; 输出三行文本，每行在最后一个 \n 之后开始。

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
	cout << "Hello\n" << "I'm a C++\n" << "Program!\n";
}
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_117_1.png)

如果你想在 cout 语句中插入语音引号，就必须使用反斜杠，因为它本身就使用引号：

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
	cout << "Hello, user. This is how to use \"quotes\".";
}
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_117_2.png)

甚至有一个字符字面量可以触发警报。在 Windows 10 中，它是使用 \a 时响起的通知声音。试试这段代码，并调大你的音量。

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
	cout << "ALARM! \a";
}
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_117_3.png)

### A HANDY CHART

有许多字符字面量或转义序列代码可供选择。因此我们认为在你需要插入代码时为你提供一个方便的图表会很好。

| ESCAPE SEQUENCE CODE | CHARACTER |
|---|---|
| \\ | Backslash |
| \' | Single Quote |
| \" | Double Quote (Speech Marks) |
| \? | Question Mark |
| \a | Alert/Alarm |
| \b | Backspace |
| \f | Form Feed |
| \n | New Line |
| \r | Carriage Return |
| \t | Horizontal Tab |
| \v | Vertical Tab |
| \0 | Null Character |
| \uxxxx | Unicode (UTF-8) |
| \Uxxxxxxxx | Unicode (UTF-16) |

### UNICODE CHARACTERS (UTF-8)

Unicode 字符是跨所有平台标准的符号或字符。例如，版权符号，可以通过输入 Unicode 代码然后按 ALT+X 在键盘上输入。版权符号的情况下输入：00A9 Alt+X。在 C++ 代码中，你会输入：

```
#include <iostream>
using namespace std;

int main ()
{
    cout << "\u00A9";
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_118_0.png)

### UNICODE CHARACTER TABLE

可用的 Unicode 字符的完整列表可以在 www.unicode-table.com/en/ 上找到。将鼠标悬停在字符上以查看在 C++ 中输入的唯一代码。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_118_1.png)

