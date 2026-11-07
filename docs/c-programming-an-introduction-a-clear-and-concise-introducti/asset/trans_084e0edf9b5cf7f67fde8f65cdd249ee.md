
块内的语句称为循环体。

while 循环有两个必要的组成部分：1）一个需要测试的条件；2）一个使得条件最终变为 false 的语句。第二个组成部分很重要，因为如果控制循环的条件永远不会变为 false，循环将永远运行（或至少直到计算机资源耗尽）。这种情况被称为*无限循环*。

让我们看两个简单的 while 循环示例。第一个示例将 “Hello, World!” 这个短语显示十次。代码如下：

```cpp
int number = 1;

while (number <= 10)
{
    cout << "Hello, World!" << endl;
    ++number;
}
```

这个示例非常简单，但它指出了成功实现 while 循环所需的重要组件。变量 number 称为循环控制变量。该变量的值控制循环的迭代。通常，循环控制变量在循环外部被赋予一个值。然后，循环控制变量在条件中进行测试。因为我们要显示十次 “Hello, World!”，所以每次循环迭代时 number 的值都必须小于或等于 10。它被初始化为 1，这样条件将为 true，从而进入循环体。

变量初始化后，将测试 while 循环条件。由于 number 当前值为 1，且 1 小于或等于 10，条件为 true，因此进入循环体。短语 “Hello, World!” 被显示到控制台，在最后一行，number 的值增加到 2。

此时，程序回到循环条件，再次进行测试。由于 2 小于或等于 10，条件为 true，并执行另一次迭代。这一过程持续到 number 的值变为 11。当条件被测试时，该值为 false，因为 11 不小于或等于 10，而是大于 10，因此控制权转移到右花括号之后的语句。

下一个示例也没有做什么非常重要的事情，但它再次演示了 while 循环的常见组成部分。我们要编写一个程序，对整数 1 到 10 求和。我们的循环控制变量将再次命名为 number。它被初始化为 1，并在每次迭代时增加 1。我们还需要在循环外部初始化第二个变量（sum），用来在计算过程中保存这些数字的和。

程序如下：

```cpp
// WhileLoop.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number, sum;
    number = 1;
    sum = 0;
    while (number <= 10)
    {
        sum += number;
        ++number;
    }
    cout << "The sum of 1 - 10 is " << sum << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出是：

The sum of 1 - 10 is 55

这个程序还演示了循环控制变量除了控制循环迭代之外，还可以用于其他用途，因为 number 的值被用来计算总和。

## 从文件读取数据

在大多数 C++ 程序中，主要有两种类型的 while 循环——计数器控制循环和哨兵控制循环。上面讨论的示例都是计数器控制循环，因为循环的条件基于达到某个计数，无论是在 “Hello, World!” 示例中循环的迭代次数，还是在计算总和示例中达到某个数字。

另一方面，哨兵控制循环由特定情况控制，例如达到特定值，或者资源耗尽，例如到达文件末尾。该值称为哨兵值，当获得该哨兵值时，哨兵控制循环停止。

哨兵控制循环的一个经典示例是读取文本文件内容的循环。读取数据文件通常由哨兵值控制，因为我们不知道何时到达文件末尾。无法输入特定值，例如要读取的行数，除非我们事先知道文件中有多少行，但这种情况很少见。我们将讨论如何通过读取文本文件的内容来开发哨兵控制循环。

## 处理文本文件

为了从文本文件读取数据，我们需要使用一些特殊函数和对象，它们是外部库 fstream 库的一部分。该库称为“文件流”库，允许我们将文本文件作为流打开，就像我们使用 iostream 库来处理控制台和键盘一样。

第一步是包含 fstream 库的预处理器指令：

```cpp
#include <fstream>
```

该指令被放置在与 iostream 库指令相同的组中。

下一步是创建一个表示我们要读取的文件的文件对象。由于我们正在从文件读取数据，因此文件对象的数据类型是 ifstream。如果我们要将数据写入文件，则会使用 ofstream（输出）数据类型。创建文件对象的代码行是：

```cpp
ifstream myFile;
```

我们还需要一个字符串变量来存储读取的数据：

```cpp
string line;
```

然后我们需要将文件对象与物理文件关联起来。我们使用 open() 函数来完成这一步，将文件的完整路径作为函数的参数传入。该函数直接从文件对象调用，如下所示：

```cpp
myFile.open("c:\\data\\example.txt");
```

open() 函数的参数必须是文件的完整路径，除非文件位于程序所在的同一目录中，在这种情况下，我们可以只使用文件名：

```cpp
myFile.open("example.txt");
```

当文件打开后，我们就可以读取其内容了。这需要一个 while 循环，该循环将一直运行到文件中没有更多数据为止。这是一个哨兵控制循环的示例，我们用于读取数据的哨兵值是由 fstream 函数 eof() 给出的 true/false 值。当文件中还有更多数据要读取时，该函数返回 false，当没有更多数据时返回 true。代码如下：

```cpp
while (!myFile.eof())
{

```

请注意，我们在这里使用了 !（非）运算符，因为 eof() 函数在有数据可读时返回 false，因此我们必须对该 false 值取反，以便循环继续运行。

循环体中的第一行读取一行文本并将其存储在一个变量中：

```cpp
getline(myFile, line);
```

下一行也是最后一行，显示从文件读取的文本：

```cpp
cout << line << endl;
}
```

最后，无论何时打开文件，我们都应该关闭它，并且有一个 close() 函数正是为此目的而设计的：

```cpp
myFile.close();
```

完整的程序如下：

```cpp
// textFile.cpp : main project file.
#include "stdafx.h"
using namespace System;
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main(array<System::String ^> ^args)
{
    ifstream myFile;
    string line;
    myFile.open("example.txt");
    while (!myFile.eof())
    {
        getline(myFile, line);
        cout << line << endl;
    }
    myFile.close();
    Console::ReadKey();
    return 0;
}
```

这个示例演示了如何处理文本文件，但它并没有真正解决一个问题。让我们编写一个程序，从文件中读取一组每日最高温度，并计算平均最高温度。这是一个有趣的问题，因为我们必须跟踪已读取的温度数量，以便计算平均值。首先，创建一个包含温度列表的文本文件。尽量不要注意你在文件中放了多少个温度，但至少包括十五到二十个温度。

下面是计算平均温度的程序：

```cpp
// readTemps.cpp : main project file.

#include "stdafx.h"

using namespace System;
#include <iostream>
#include <fstream>
using namespace std;

int main(array<System::String ^> ^args)
{
    ifstream temps;
    int temp, totalTemps, numTemps;
    double average;
    totalTemps = numTemps = 0;
    temps.open("C:\\data\\temperatures.txt");
    while (!temps.eof())
    {
        temps >> temp; // read an int
        totalTemps += temp;
        ++numTemps;
    }

    average = totalTemps / numTemps;
    cout << "The average temperature is: " << average
         << endl;
    Console::ReadKey();
    return 0;
}
```

这个程序中有一些你以前没见过的新东西。这一行：

```cpp
totalTemps = numTemps = 0;
```

