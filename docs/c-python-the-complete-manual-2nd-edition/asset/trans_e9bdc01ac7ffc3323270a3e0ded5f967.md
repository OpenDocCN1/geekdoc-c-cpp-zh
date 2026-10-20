
## 定义常量

常量是代码中的固定值。它们可以是任何基本数据类型，但正如其名称所示，它们的值在整个代码中保持不变。在 C++ 中定义常量有两种不同的方式：`#define` 预处理器和 `const`。

### #define 预处理器

预处理器是给编译器的指令，让它在编译代码之前对信息进行预处理。`#include` 和 `#define` 都是预处理器。

#### 步骤 1

你可以使用 `#define` 预处理器在代码中定义任何你想要的常量。首先创建一个新的 C++ 文件，并包含通常的头文件：

```cpp
#include <iostream>
using namespace std;

int main ()
{
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_119_0.png)

#### 步骤 2

现在假设你的代码中有三个不同的常量：length、width 和 height。你可以这样定义它们：

```cpp
#include <iostream>
using namespace std;
#define LENGTH 50
#define WIDTH 40
#define HEIGHT 60

int main ()
{
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_119_2.png)

#### 步骤 3

注意定义的常量使用大写字母，将所有常量定义为大写是一种良好的编程实践。这里赋给它们的值是 50、40 和 60，下面我们来调用它们：

```cpp
#include <iostream>
using namespace std;

#define LENGTH 50
#define WIDTH 40
#define HEIGHT 60

int main ()
{
    cout << "Length is: " << LENGTH << "\n";
    cout << "Width is: " << WIDTH << "\n";
    cout << "Height is: " << HEIGHT << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_119_1.png)

#### 步骤 4

编译并运行代码。正如预期的那样，它会显示所创建的每个常量的值。值得注意的是，使用 `#define` 关键字定义常量时不需要分号。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_119_3.png)

#### 步骤 5

你也可以将其他元素定义为常量。例如，在 `cout` 语句中，你可以不使用 `\n` 来表示换行，而是在代码开头定义它：

```cpp
#include <iostream>
using namespace std;
#define LENGTH 50
#define WIDTH 40
#define HEIGHT 60
#define NEWLINE '\n'
int main ()
{
cout << "Length is: " << LENGTH << NEWLINE;
cout << "Width is: " << WIDTH << NEWLINE;
cout << "Height is: " << HEIGHT << NEWLINE;
}
```

#### 步骤 6

这段代码在编译并执行后，与之前的效果完全相同，它使用新的常量 `NEWLINE` 在 `cout` 语句中插入换行。顺便说一下，创建一个换行常量并不是一个好主意，除非你让它比 `\n` 甚至 `endl` 命令更简短。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_120_0.png)

#### 步骤 7

在代码开头定义常量是初始化基础值的好方法。你可以定义游戏有三条命，甚至可以定义 `PI` 的值，而无需调用 C++ 数学库：

```cpp
#include <iostream>
using namespace std;
#define PI 3.14159
int main ()
{
cout << "The value of Pi is: " << PI << endl;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_120_1.png)

#### 步骤 8

定义常量的另一种方法是使用 `const` 关键字。将 `const` 与数据类型、变量和值结合使用：`const type variable = value`。以 `PI` 为例：

```cpp
#include <iostream>
using namespace std;
int main ()
{
const double PI = 3.14159;
cout << "The value of Pi is: " << PI << endl;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_120_2.png)

#### 步骤 9

因为你在 `main` 代码块中使用 `const`，所以需要用分号结束该行。只要名称和值不冲突，你可以使用任意一种方法，但值得一提的是，`#define` 不占用内存，所以如果你在有限的固定内存下编程，`#define` 是你最好的选择。

#### 步骤 10

`const` 的工作方式与 `#define` 非常相似。你可以创建静态整数甚至换行符：

```cpp
#include <iostream>
using namespace std;
int main()
{
const int LENGTH = 50;
const int WIDTH = 40;
const char NEWLINE = '\n';
int area;
area = LENGTH * WIDTH;
cout << "Area is: " << area << NEWLINE;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_120_3.png)

## 文件输入/输出

标准 iostream 库为 C++ 程序员提供了 `cin` 和 `cout` 输入/输出功能。然而，要读写文件，你需要使用另一个 C++ 库，叫做 fstream。

### fstream 流

`fstream` 库中有两种主要的数据类型用于打开文件、读取文件和写入文件：`ofstream` 和 `ifstream`。下面是它们的工作方式。

#### 步骤 1

第一步是创建一个新的 C++ 文件，除了通常的头文件外，你还需要包含新的 `fstream` 头文件：

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main ()
{
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_121_0.png)

#### 步骤 2

首先询问用户的姓名，并将该信息写入文件。你需要用通常的 `string` 来存储姓名，并用 `getline` 来接受用户的输入。

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main ()
{
    string name;
    ofstream newfile;
    newfile.open("name.txt");
    cout << "Enter your name: " << endl;
    getline(cin, name);
    newfile << name << endl;
    newfile.close();
}
```

#### 步骤 3

我们在第 2 步的截图中加入了注释，以帮助你理解这个过程。你创建了一个名为 `name` 的字符串，用于存储用户输入的名字。你还创建了一个名为 `name.txt` 的文本文件（通过 `ofstream newfile` 和 `newfile.open` 这几行），询问用户的姓名并存储，然后将数据写入文件。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_121_1.png)

#### 步骤 4

要读取文件内容并将其输出到屏幕，你需要稍微不同的做法。首先，你需要创建一个字符串变量来存储文件的内容（逐行），然后打开文件，使用 `getline` 逐行读取文件并将这些行输出到屏幕。最后，关闭文件。

```cpp
string line;
ifstream newfile ("name.txt");

cout << "Contents of the file: " << endl;

getline(newfile, line);
cout << line << endl;
newfile.close();
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_121_2.png)

#### 步骤 5

上面的代码非常适合打开只有一两行的文件，但如果有多行呢？这里我们打开了一个罗伯特·E·霍华德的诗《Cimmeria》的文本文件：

```cpp
string line;
ifstream newfile ("c:\\users\\david\\Documents\\Cimmeria.txt");
cout << "Cimmeria, by Robert E Howard: \n" << endl;
while (getline(newfile, line))
cout << line << endl;
newfile.close();
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_122_0.png)

#### 步骤 6

你肯定能看到我们加入了一个 `while` 循环，我们会在几页后谈到它。它的意思是，只要文本文件中还有行要读取，C++ 的 `getline` 就会读取它们。当所有行都读取完毕后，输出会显示在屏幕上，然后文件被关闭。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_122_1.png)

#### 步骤 7

你还可以看到，文本文件 `Cimmeria.txt` 的位置不在 C++ 程序所在的文件夹中。当我们创建第一个 `name.txt` 文件时，它被写到了代码所在的文件夹，这是默认行为。要指定另一个文件夹，你需要使用双反斜杠，正如字符字面量/转义序列代码所要求的那样。

```cpp
string line;
ifstream newfile ("c:\\users\\david\\Documents\\Cimmeria.txt");
cout << "Cimmeria, by Robert E Howard: \n" << endl;
```

#### 步骤 8

正如你可能预料的那样，你可以将几乎任何你喜欢的内容写入文件，然后可以在记事本中读取，或通过 C++ 代码在控制台中读取：

```cpp
string name;
int age;
ofstream newfile;
newfile.open("name.txt");
cout << "Enter your name: " << endl;
getline(cin, name);
newfile << name << endl;
cout << "\nHow old are you: " << endl;
cin >> age;
newfile << age << endl;
newfile.close();
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_122_2.png)

#### 步骤 9

第 8 步中的代码又有所不同，但仅仅是在我们使用 `cin >> age` 的地方，而不是之前所用的 `getline(cin, variable)`。原因在于 `getline` 函数处理的是字符串，而不是整数；所以当你使用的数据类型不是字符串时，请使用标准的 `cin`。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_122_3.png)

#### 步骤 10

这里有一个练习：看看你是否能编写代码，将几种不同的元素写入文本文件。你可以包含用户的姓名、年龄、电话号码等，甚至可以是 `Pi` 的值和各种数学元素。这都是很好的练习。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_122_4.png)

