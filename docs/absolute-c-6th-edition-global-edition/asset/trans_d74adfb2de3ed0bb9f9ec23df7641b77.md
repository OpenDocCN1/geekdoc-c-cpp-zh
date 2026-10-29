

字符“1”和“0”不是数字10。这种字符与数字之间的转换通常是自动完成的，因此你无需考虑这些细节；然而，有时所有这些自动帮助反而会碍事。因此，C++提供了一些用于字符数据输入和输出的低级工具。这些低级工具不包含自动转换。这使你可以绕过自动工具，以任何你想要的方式进行输入/输出。如果你真的愿意，甚至可以编写能够以罗马数字记号读写int值的输入和输出函数。

## 成员函数get和put

函数get允许你的程序读入一个输入字符并将其存储到char类型的变量中。每个输入流，无论是输入文件流还是流cin，都有作为成员函数的get。我们将在此处将get描述为对象cin的成员函数。（当我们在第12章讨论文件I/O时，我们会看到它对于输入文件流的行为与对cin完全相同。）

在此之前，我们使用cin和提取运算符`>>`来读取一个输入字符（或就此而言，任何其他输入）。当你使用提取运算符`>>`时，有些事情会自动为你完成，比如跳过空白。但有时你并不想跳过空白。成员函数cin.get读取下一个输入字符，无论该字符是否为空白。

### cin.get

成员函数get接受一个参数，该参数应为char类型的变量。该参数接收从输入流中读取的输入字符。例如，以下代码将从键盘读取下一个输入字符并将其存储到变量nextSymbol中：

```
char nextSymbol;
 cin.get(nextSymbol);
```

读取空白和'\n'

重要的是要注意，你的程序可以以这种方式读取任何字符。如果下一个输入字符是空白，则此代码将读取该空白字符。如果下一个字符是换行符'\n'（也就是说，如果程序刚刚到达输入行的末尾），那么上一次对cin.get的调用会将nextSymbol的值设置为'\n'。例如，假设你的程序包含以下代码：

```
char c1, c2, c3;
 cin.get(c1);
 cin.get(c2);
 cin.get(c3);
```

并且假设你输入以下两行文本供此代码读取：

AB
CD

c1的值被设置为'A'，c2的值被设置为'B'，c3的值被设置为'\n'。变量c3不会被设置为'C'。

### 检测输入行的末尾

你可以使用成员函数get做的一件事情是让程序检测一行的末尾。以下循环将读取一行输入，并在经过换行符'\n'后停止。任何后续输入都将从下一行的开头读取。对于这第一个示例，我们只是回显了输入，但同样的技术允许你对输入执行任何你想做的操作。

```
cout << "Enter a line of input and I will echo it:\n";
char symbol;
do
{
    cin.get(symbol);
    cout << symbol;
} while (symbol != '\n');
cout << "That's all for this demonstration.\n";
```

此循环将读取任何输入行并精确回显它，包括空白。以下是此代码产生的示例对话：

```
Enter a line of input and I will echo it:
Do Be Do 1 2    34
Do Be Do 1 2    34
That's all for this demonstration.
```

请注意，换行符'\n'既被读取也被输出。由于输出了'\n'，以“That's”一词开头的字符串位于新行上。

### '\n'和"\n"

> '\n'和"\n"有时看起来像是相同的东西。在cout语句中，它们产生相同的效果，但它们不能在所有情况下互换使用。'\n'是char类型的值，可以存储在char类型的变量中。另一方面，"\n"是一个恰好由一个字符组成的字符串。因此，"\n"不是char类型，不能存储在char类型的变量中。

### put

成员函数put与成员函数get类似，不同之处在于它用于输出而不是输入。函数put允许你的程序输出一个字符。成员函数cout.put接受一个参数，该参数应为char类型的表达式，例如常量或char类型的变量。当调用该函数时，参数的值将输出到屏幕。例如，以下代码将字母'a'输出到屏幕：

```
cout.put('a');
```

函数cout.put并不允许你做任何使用插入运算符`<<`无法做到的事情，但我们包含它是为了完整起见。（当我们在第12章讨论文件I/O时，我们会看到put可以与连接到文本文件的输出流一起使用，并且不限于仅与cout一起使用。）

## 成员函数get

函数get可用于读取一个输入字符。与提取运算符`>>`不同，get读取下一个输入字符，无论该字符是什么。特别是，如果下一个输入字符是空白或换行符'\n'，get将读取它。函数get接受一个参数，该参数应为char类型的变量。当调用get时，下一个输入字符被读取，参数变量的值被设置为该输入字符。

### 示例

```
char nextSymbol;
 cin.get(nextSymbol);
```

正如我们将在第12章中看到的，如果你想使用get从文件读取，则使用输入文件流代替流cin。

如果你的程序使用cin.get或cout.put，那么与cin和cout的其他用法一样，你的程序应包含以下内容之一（或类似内容）：

```
#include <iostream>
using namespace std;
```

或

```
#include <iostream>
using std::cin;
using std::cout;
```

### 示例：使用换行函数检查输入

Display 9.2中的函数getInt询问用户输入是否正确，如果用户表示输入不正确，则要求输入新值。Display 9.2中的程序只是一个驱动程序，用于测试函数getInt，但该函数或与之非常相似的函数可以用于任何从键盘获取输入的程序中。

请注意对函数newLine()的调用。函数newLine读取当前行剩余的所有字符，但不做任何处理。这相当于丢弃该行的剩余部分。因此，如果用户输入No，则程序读取第一个字母N，然后调用函数newLine，该函数丢弃输入行的其余部分。这意味着，如果用户在下一输入行输入75，如示例对话所示，程序将读取数字75，而不会尝试读取单词No中的字母o。如果程序不包含对函数newLine的调用，那么下一个读取的项目将是包含No的行中的o，而不是下一行中的数字75。

## Display 9.2 检查输入（第1部分，共2部分）

```
//Program to demonstrate the functions newLine and getInput
#include <iostream>
using namespace std;

void newLine();
//Discards all the input remaining on the current input line.
//Also discards the '\n' at the end of the line.

void getInt(int& number);
//Sets the variable number to a
//value that the user approves of.

int main()
{
    int n;

    getInt(n);
    cout << "Final value read in = " << n << endl
        << "End of demonstration.\n";

    return 0;
}

//Uses iostream:
void newLine()
{
    char symbol;
    do
    {
        cin.get(symbol);
    } while (symbol != '\n');
}

//Uses iostream:
void getInt(int& number)
{
    char ans;
    do
    {
        cout << "Enter input number: ";
        cin >> number;
        cout << "You entered " << number
            << " Is that correct? (yes/no): ";
        cin >> ans;
        newLine();
    } while ((ans == 'N') || (ans == 'n'));
}
```

