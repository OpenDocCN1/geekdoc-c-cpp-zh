
当执行该程序时，它会创建一个名为 `configFile` 的输入流。使用该流，程序会尝试打开一个名为 `activities` 的 CSV 数据文件。它使用 `good()` 成员函数来测试文件是否已打开，以及流是否包含准备好读取的数据。

程序创建了三个字符串值数组，分别称为 `firstName`、`surname` 和 `activity`。这些数组存储了关于人员及其选择的活动的详情。程序开始执行一个 `while` 循环，从文件的每行中反复读取三个值，并将这些值存储在三个不同的数组中。一旦到达文件末尾或数组满，`while` 循环将终止。

现在数组中包含了文件中的数据，可以对其进行搜索。程序创建了一个无限 `while` 循环，允许用户输入想要搜索的特定活动名称。它会在 `activity` 数组中搜索用户输入的文本。如果找到，将显示每个选择该特定活动的人的名字和姓氏。如果没有发现任何人参加了目标活动，程序会在屏幕上显示“NOT FOUND.”。

| 输入活动名称： |
| :--- | :--- |
| water-park | Maya Taylor-Wright |
| paintball | Hazel Forder, Sam Hodgson |
| yodelling | NOT FOUND. |

## 选择示例：输入你想要使用的文件名

在之前的示例中，我们已经看到可以创建一个文件流，将数据从文件引入计算机内存：你的程序告诉计算机打开一个具有特定名称的文件。到目前为止，此文件名一直作为字面量构建在程序代码中，并在调用文件流的 `open()` 成员函数时使用：

```cpp
// 检查存储卡上是否存在该文件并打开它以准备读取数据

istream originalFile;

originalFile.open("airportdata");
```

通常，运行程序的人可能想要选择打开哪一个文件。我们可以要求用户输入他们存储的文件名，并将其存储在字符串变量中，然后使用它来打开文件：

显示如何选择文件名然后打开该特定文件的示例

遗憾的是，`open()` 函数在 C++ 语言存在之前就已经创建了——它是来自“C”语言的代码，即 C++ 的前身。事实上，C++ 中使用的一些常用函数实际上来自 C。

C 处理文本字符串的方式与 C++ 不同。在 C语言中，没有所谓的“string”数据类型。当你想要创建并使用变量来存储文本数据时，你必须创建一个字符数组，并在一个特殊的空字符来标记文本的结束。这些被称为“以空终止的字符串”或“C 风格字符串”。

许多较旧的 C 函数在被调用时，期望将 C 风格的字符串作为参数（输入值）。如果你尝试给 C 函数提供一个 C++ 字符串值进行处理，它期望的是一个以空终止的字符串，函数将不会将其识别为有效参数。需要的是将 C++ 字符串转换为 C 风格的空终止字符串，以便该值可以作为参数使用。

幸运的是，使用 C 风格的空终止字符串转换特定文件是非常简单的。`c_str()` 函数可以为我们完成工作：

```cpp
// 示例显示如何使用 C 风格的空终止字符串作为文件名选择特定文件

// 获取以 C++ 字符串值表示的文件名

cout << "Please type in the filename:" << endl;

string fileName;

cin >> fileName; // 注意这是一个 C++ 字符串

// 创建用于从文件中读取数据的“缓冲区”

istream originalFile;

// 将文件名转换为 C 风格的空终止字符串，然后打开文件

originalFile.open( fileName.c_str() );
```

第 11 章：数据文件 | 423

## 同时处理多个文件

下一个示例涉及多个文件的操作。它从你选择的文件中读取文本，创建该文件的一个副本，通过在新文件的每行文本之后插入一个额外的空行，使之具有双倍行间距。为了选择要处理的文件，程序使用了上一页描述的技术，允许用户输入他们选择的文件名。

程序使用了两个文件流——一个输入文件流和一个输出文件流。这两个文件流都同时保持打开状态。与任何处理文件的程序一样，你要确保程序打开的每一个文件流在程序处理完成后最终都被关闭。

### 示例 11.14 - two_files.cpp

```cpp
#include <iostream> // 程序将在屏幕上显示一些文本

#include <fstream> // 程序将使用文件

#include <cstring> // 程序使用 exit() 和 c_str() 函数

using namespace std; // 将使用标准标识符 string, cout 和 endl

int main()
{
    // 输入原始文件的名称
    cout << "Name of the original file that contains the text:" << endl;
    string inputFileName, outputFileName;
    cin >> inputFileName; // 注意这是一个 C++ 字符串
    outputFileName = inputFileName + ".new";

    // 创建“缓冲区”并尝试打开原始文件
    ifstream originalFile;
    originalFile.open(inputFileName.c_str());

    // 原始文件的文本已成功打开
    if (originalFile.is_open())
    {
        // 创建一个同名但以 ".new" 结尾的新文件
        ofstream newFile;
        newFile.open(outputFileName.c_str());

        // 只有在新文件创建成功时才继续
        if (newFile.is_open())
        {
            string lineOfText;
            while (originalFile.good())
            {
                getline(originalFile, lineOfText); // 从文件中读取整行
                // 写入新文件，后跟一个额外的空行
                newFile << lineOfText << endl << endl;
            } // 读取最后一行后结束
        }
        newFile.close(); // 完成对新文件的使用
    }
    else
    {
        cout << "ERROR! COULD NOT CREATE FILE!" << endl;
    }
    originalFile.close(); // 完成对原始文件的使用
    cout << "Done - look in " << outputFileName << endl;
} else {
    cout << "ERROR! COULD NOT READ FROM ORIGINAL FILE!" << endl;
    return 0;
}
```

## 使用 stringstream 在文本和数值之间进行转换

C++ 可以在使用 `string` 数据类型存储的文本值与数值值（例如使用 `int` 或 `float` 数据类型存储的值）之间进行转换。

在开始之前，你需要创建一个包含以下简单数据的文本文件 "numbers"：

| 32 |
| 27 |
| 199 |

该文件的内容看起来是数值，但它们实际上是文本值。遗憾的是，字符串值无法作为数字进行处理——你的程序无法对文本执行常见的数值计算。

要在文本和数值数据之间进行转换，你的程序可以使用一种名为 `stringstream` 的特殊功能，它是 `<sstream>` 库的一部分。

数据值可以被送入 `stringstream` 对象中，准备转换为其他数据类型。然后，你可以以希望使用的数据类型形式从 `stringstream` 中提取或“拉取”出来。

例如，字符串值 "1.75" 可以送入 `stringstream`。然后它可以作为数值 1.75 被拉取出来，并使用 `float` 数据类型表示。一旦它变成了 `float` 形式，就可以对其进行数学运算，而这在字符串值上是无法可能的。

`int` 值 2001 可以被送入 `stringstream`。该值可以再次被拉取为字符串值 "2001"。一旦它变成了字符串值形式，就可以对文本的部分进行操作，甚至可以对其中的单个字符进行操作。你可以想象字符串可能会被拆分成单个字符——这对于文本值来说很容易做到，但对于存储为数值数据类型的值来说并非如此。

要在程序中使用 `stringstream`，你必须包含 `<sstream>` 库：

```cpp
#include <sstream>
```

然后你可以在代码中创建一个类型为 `stringstream` 的对象 `conversionStream`：

```cpp
stringstream conversionStream;
```

现在你现在可以将一个值送入 `stringstream`，使其准备好转换：

```cpp
int numValue = 123;
conversionStream << numValue;
```

然后可以将该值从 `stringstream` 中拉回，存储在具有不同数据类型的变量中：

```cpp
string textValue;
conversionStream >> textValue;
```

在上面的示例中，一旦 `int` 值 123 被转换为字符串值，就可以对其执行诸如 `length()` 或 `at()` 之类的字符操作。这对于具有数值数据类型的值是不可能的。

这里有一个程序，它将读取你的 "numbers" 文件，使用 `stringstream` 将字符串值转换为 `int`。

一旦值被转换为整数，它们就会被加在一起创建一个运行总和，并在到达文本文件末时显示该总和。

### 示例 11.15-convert_to_integers.cpp

```cpp
#include <iostream>          // 程序将在屏幕上显示一些文本
#include <fstream>            // 程序将使用文件
#include <sstream>           // 程序将使用 stringstream 转换值
using namespace std;               // 将使用标准标识符 cout 和 endl

int main() {
    // 尝试打开包含数据的文本文件
    ifstream dataFile;
    dataFile.open("numbers");

    // 检查文件是否存在并可以打开
    if (dataFile.is_open()) {
        stringstream conversionStream;       // 这将文本值转换为整数
        string lineOfText;             // 从文件中读取的文本值
        int dataValue;                  // 转换为整数后的值
        int sumTotal = 0;               //累加所有整数值的总和
        // 如果文件成功打开，则读取文本数据行
        while (dataFile.good()) {
            // 从文件中读取下一整行
            getline(dataFile, lineOfText);
            // 检查行是否为空
            if (lineOfText.length() > 0) {
                // 将文本送入 stringstream
                conversionStream << lineOfText;
                // 从 stringstream 中拉取转换后的值
                conversionStream >> dataValue;
                // 显示转换后的整数值
                cout << "converted to integer value " << dataValue << endl;
                // 将值累加到总和
                sumTotal += dataValue;
                // 清空 stringstream 的内容准备准备下一次转换
                conversionStream.str("");
                // 重置流的状态，以防遇到错误
                conversionStream.clear();
            } else {
                // 忽略空行
                cout << "Blank line - ignored" << endl;
            }
        } // 当读取最后一行时结束循环
        cout << endl << "*** End of file reached ***" << endl;
        // 关闭文件
        dataFile.close();
        // 显示所有值的总和
        cout << endl << "The total of all values is " << sumTotal << endl;
    } else {
        cout << "ERROR! Could not read from the file!" << endl;
    }
    return 0;
}
```

注意，程序还包含了这些额外的语句：
（注意：原始代码块中的逻辑已整合到上面的代码块中以确保正确性。）

## 无效数据问题

程序如何处理无法转换的值？尝试更改你的 "numbers" 文件，使其包含一些空行和一个单词。

| 32 |
| 27 |
| 12 |
| Aloha! |
| 199 |

当程序读取上述内容时，你应该看到：

```
Text value 32 converted to integer value 32
Text value 27 converted to integer value 27
Blank line - ignored
Text value 12 converted to integer value 12
Text value Aloha! converted to integer value 0
Blank line - ignored
Text value 199 converted to integer value 199
Blank line - ignored
*** End of file reached ***
```

注意，空行被简单忽略——它们不包含任何转换为数字的数据。文本 "Aloha!" 被送入转换器，它返回整数值 0。

如果你想自定义代码以拒绝文件中任何包含字母或标点的值，可以在传递给 stringstream 之前添加语句检查文本值中不可接受的字符。这很容易通过 for 循环实现，使用 `isdigit()` 函数检查原始值中的每个字符是否为数字。

```cpp
unsigned int pos;
bool foundProblem;
// 下面代码检查文本值是否仅由数字组成
foundProblem = false;
for ( pos = 0; pos < lineText.length(); pos++) {
    if ( not isdigit(lineText.at( pos ) ) {
        foundProblem = true;
    }
}
```

注意，在上面的代码中，由于我们已经在程序中包含了 `<iostream>`，我们可以在不显式包含 `<ctype>` 库的情况下使用 `isdigit()` 函数。

这里是最终的程序，它在尝试将从文件中读取的每个值转换为整数之前对其进行验证：

# 示例 11.16-validate_integers.cpp

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本
#include <fstream>       // 程序将使用文件
#include <sstream>       // 程序将使用 stringstream 来转换值
using namespace std;                   // 将使用标准字符串、cout 和 endl

int main() {
    // 尝试打开包含数据的文本文件
    ifstream dataFile;
    dataFile.open("numbers");

    // 检查文件是否存在并可以被打开
    if (dataFile.is_open()) {
        stringstream conversionStream; // 这将文本值转换为整数
        string lineOfText;             // 从文件中读取的文本值
        int dataValue;                 // 转换为整数的值
        unsigned int pos;              // 检查是否有效时在文本中的位置
```
