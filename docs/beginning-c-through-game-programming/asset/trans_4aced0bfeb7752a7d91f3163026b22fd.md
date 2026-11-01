
你可以从课程技术网站（www.courseptr.com/downloads）下载本程序的代码。程序位于第 3 章文件夹中；文件名是 `string_tester.cpp`。

```cpp
// String Tester
// Demonstrates string objects

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string word1 = "Game";
    string word2("Over");
    string word3(3, '!');

    string phrase = word1 + " " + word2 + word3;
    cout << "The phrase is: " << phrase << "\n\n";

    cout << "The phrase has " << phrase.size() << " characters in it.\n\n";

    cout << "The character at position 0 is: " << phrase[0] << "\n\n";

    cout << "Changing the character at position 0.\n";
    phrase[0] = 'L';
    cout << "The phrase is now: " << phrase << "\n\n";

    for (unsigned int i = 0; i < phrase.size(); ++i)
    {
        cout << "Character at position " << i << " is: " << phrase[i] << endl;
    }

    cout << "\nThe sequence 'Over' begins at location ";
    cout << phrase.find("Over") << endl;

    if (phrase.find("eggplant") == string::npos)
    {
        cout << "'eggplant' is not in the phrase.\n\n";
    }

    phrase.erase(4, 5);
    cout << "The phrase is now: " << phrase << endl;

    phrase.erase(4);
    cout << "The phrase is now: " << phrase << endl;

    phrase.erase();
    cout << "The phrase is now: " << phrase << endl;

    if (phrase.empty())
    {
        cout << "\nThe phrase is no more.\n";
    }

    return 0;
}
```

## 创建 string 对象

在 `main()` 中我做的第一件事就是以三种不同的方式创建三个 string 对象：

```cpp
string word1 = "Game";
string word2("Over");
string word3(3, '!');
```

在这组代码的第一行中，我直接使用赋值运算符创建 string 对象 `word1`，方式与你见过的其他变量相同。结果是 `word1` 为 "Game"。

接下来，我通过将想要赋给变量的 string 对象放在一对圆括号中来创建 `word2`。结果是 `word2` 为 "Over"。

最后，我通过在一对圆括号中提供一个数字后跟一个字符来创建 `word3`。这会生成一个由所提供的字符组成的 string 对象，其长度等于该数字。结果是 `word3` 为 "!!!"。

## 连接 string 对象

接下来，我通过连接前三个 *string* 对象来创建一个新的 string 对象 *phrase*：

```cpp
string phrase = word1 + " " + word2 + word3;
```

结果是 *phrase* 为 "Game Over!!!"。

注意，你之前只见过对数字起作用的 `+` 运算符，它同样也能连接 *string* 对象。这是因为 `+` 运算符已被重载。当你第一次听到 *overloaded* 这个词时，可能会觉得这不是什么好事——运算符要爆炸了！但这是件好事。运算符重载重新定义了一个熟悉的运算符，使它在新的、之前未定义的情境中以不同方式工作。在这个例子中，我使用 `+` 运算符不是为了加数字，而是为了连接 *string* 对象。我之所以能做到这一点，仅仅是因为 *string* 类型专门重载了 `+` 运算符，并定义了它在与 string 对象一起使用时表示 *string* 对象连接。

## 使用 size() 成员函数

好的，是时候看看 *string* 的成员函数了。接下来，我使用成员函数 *size()*：

```cpp
cout << "The phrase has " << phrase.size() << " characters in it.\n\n";
```

*phrase.size()* 通过成员选择运算符 `.`（点号）调用 *string* 对象 *phrase* 的成员函数 *size()*。*size()* 成员函数只是返回该 *string* 对象大小的无符号整数值——也就是它的字符数量。因为 *string* 对象是 "Lame Over!!!"，所以该成员函数返回 12。（每个字符都计入，包括空格。）当然，对另一个 *string* 对象调用 *size()* 可能会根据该 *string* 对象中的字符数返回不同的结果。

### 提示

*string* 对象还有一个成员函数 *length()*，它与 *size()* 一样，返回 *string* 对象中的字符数。

## 对 string 对象进行索引

string 对象存储一个 char 值序列。你可以通过使用下标运算符（`[]`）提供索引号来访问任何单个 char 值。这正是我接下来要做的：

```cpp
cout << "The character at position 0 is: " << phrase[0] << "\n\n";
```

序列中的第一个元素位于位置 0。在上一条语句中，`phrase[0]` 是字符 G。并且由于计数从 0 开始，所以 string 对象中的最后一个字符是 `phrase[11]`，即使该 string 对象有 12 个字符。

### 陷阱

忘记索引从位置 0 开始是一个常见错误。请记住，一个有 n 个字符的 string 对象可以从位置 0 索引到位置 n - 1。

你不仅可以使用下标运算符访问 string 对象中的字符，还可以重新赋值它们。这就是我接下来要做的：

```cpp
phrase[0] = 'L';
```

我将 phrase 的第一个字符改为字符 L，这意味着 phrase 变成了 "Lame Over!!!"。

### 陷阱

C++ 编译器在处理 string 对象和下标运算符时不会进行边界检查。这意味着编译器不会检查你是否正在尝试访问一个不存在的元素。访问无效的序列元素可能导致灾难性后果，因为你可能会覆盖计算机内存中的关键数据。这样做可能会使程序崩溃，所以使用下标运算符时要格外小心。

## 遍历 string 对象

凭借你对 for 循环和 string 对象的新知识，遍历 string 对象中的各个字符轻而易举。这就是我接下来要做的：

```cpp
for (unsigned int i = 0; i < phrase.size(); ++i)
{
    cout << "Character at position " << i << " is: " << phrase[i] << endl;
}
```

循环遍历 phrase 的所有有效位置。它从 0 开始，一直到 11。在每次迭代中，string 对象的一个字符会通过 `phrase[i]` 显示出来。注意，我将循环变量 `i` 声明为 `unsigned int`，因为 `size()` 返回的值是无符号整数类型。

### 现实世界

遍历序列是游戏中的一项强大且常用的技术。例如，你可能需要遍历策略游戏中的数百个独立单位，更新它们的状态和指令。或者你可能需要遍历 3D 模型的顶点列表，以应用某种几何变换。

## 使用 find() 成员函数

接下来我使用成员函数 `find()` 来检查两个字符串字面量中是否有任何一个包含在 phrase 中。首先，我检查字符串字面量 "Over"：

```cpp
cout << "\nThe sequence 'Over' begins at location ";
cout << phrase.find("Over") << endl;
```

`find()` 成员函数在调用它的 string 对象中搜索作为参数提供的字符串。该成员函数返回你要搜索的 string 对象在调用它的 string 对象中第一次出现的位置编号。这意味着 `phrase.find("Over")` 返回 "Over" 在 phrase 中第一次出现的位置编号。由于 phrase 是 "Lame Over!!!"，`find()` 返回 5。（记住，位置编号从 0 开始，所以 5 表示第六个字符。）

但是如果你搜索的字符串不存在于调用它的 string 中会怎样？我接下来处理这种情况：

```cpp
if (phrase.find("eggplant") == string::npos)
{
    cout << "'eggplant' is not in the phrase.\n\n";
}
```

因为 "eggplant" 不存在于 phrase 中，`find()` 返回一个定义在 string 文件中的特殊常量，我通过 `string::npos` 访问它。因此，屏幕显示消息：“'eggplant' is not in the phrase.”

我通过 `string::npos` 访问的常量表示 string 对象可能的最大大小，因此它大于 string 对象中任何可能的有效位置编号。非正式地说，它的意思是“一个不可能存在的位置编号”。它是表示一个字符串在另一个字符串中找不到的完美返回值。

### 提示

使用 `find()` 时，你可以提供一个可选参数，指定程序从哪个字符位置开始查找子字符串。下面这行将开始从 string 对象 phrase 中的位置 5 开始寻找字符串字面量 "eggplant"。

```cpp
location = phrase.find("eggplant", 5);
```

## 使用 erase() 成员函数

`erase()` 成员函数从 string 对象中移除一个指定的子字符串。调用该成员函数的一种方式是指定起始位置和子字符串的长度，就像我在下面的代码中所做的那样：

```cpp
phrase.erase(4, 5);
```

上一行移除从位置 4 开始的五个字符的子字符串。因为 phrase 是 "Lame Over!!!"，该成员函数移除了子字符串 Over，结果是 phrase 变成了 "Lame!!!"。

调用 `erase()` 的另一种方式是只提供子字符串的起始位置。这会移除从该位置编号开始到 string 对象末尾的所有字符。这正是我接下来要做的：

```cpp
phrase.erase(4);
```

这一行移除了 string 对象中从位置 4 开始的所有字符。由于 phrase 是 "Lame!!!"，该成员函数移除了子字符串 !!!，结果是 phrase 变成了 "Lame"。

调用 `erase()` 的又一种方式是不提供任何参数，就像我在下面的代码中所做的那样：

```cpp
phrase.erase();
```

