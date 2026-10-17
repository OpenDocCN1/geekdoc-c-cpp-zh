
运行程序时，你将看到你的 Bash 历史文件内容被逐字符地逐渐显示出来，就像在旧式的电打字终端上一样，而不是以树莓派的全速显示。

## 在从输入流读取数据时处理数据

下一个示例从一个名为 `wordlist` 的文件中读取单词列表，挑选出长度为特定字符数的单词。例如，它可以自动找到文件中所有 12 个字母的单词。

在查看如何实现之前，我们首先需要创建一个新的单词文件，或者找到一个可以使用的现有文件。

### 为程序创建一个单词字典文件

相当多的 Linux 程序都使用了“字典文件”。这是一个用于查找正确拼写的单词列表。诸像 LibreOffice Writer 这样流行的文字处理器就使用了此类文件。Linux 中还有几个独立的拼写检查工具，包括 `aspell` 和 `ispell`。

在英国，许多 Linux 系统使用名为 `british-english` 的文件，它可以在 `/usr/share/dict/` 目录下找到。

要检查该文件是否已于你的树莓派上，请尝试在命令行中输入以下内容：

```bash
ls -als /usr/share/dict/british-english
```

希望你发现系统上已经有了这个文件。如果没有，你可以从命令行在你的系统上安装该单词列表：

```bash
sudo apt-get install british
```

假设安装一切顺利，如果你按照之前的方法再次尝试 `ls` 命令，你现在应该会发现 `/usr/share/dict/british-english` 文件存在于你的树莓派上了。

如果你想检查此文件的内容，请尝试：

```bash
cat /usr/share/dict/british-english
```

这将以滚动列表的形式显示文件内容，每行一个单词。

或者，你也可以选择为你任何想要处理的其它语言使用不同的字典文件。互联网上有许多其他文件可以下载，包括经常更新新单词的开源文件。

如果你仍然无法在树莓派上找到字典文件，或者无法从互联网下载，你可以自己创建一个包含几个不同单词的简单文件。只需在 Nano 中创建一个新的文本文件，并在保存文件之前将每个单词写在不同的一行即可。

下面是我为了测试示例 11.8 - `word_lengths.cpp` 而创建的一个非常短的单词文件。该文件已保存为与程序相同目录下的 `wordlist`。你可能会注意到这些单词是按字母顺序排列的——这在以后将很有用。

如你所见，我选择了英语语言中一些最重要的单词：

```
alien
awesome
camera
cat
dog
frisbee
pizza
octopus
outter
toast
```

在下一个程序中，为你你想要使用的单词列表提供正确的文件名非常重要。

如果你想使用 `/usr/share/dict/british-english` 字典，你的代码需要以下 `open()` 语句：

```cpp
dictionaryFile.open("/usr/share/dict/british-english");
```

如果你的单词字典是你自己创建的 `wordlist` 文件，你的代码应该使用：

```cpp
dictionaryFile.open("wordlist");
```

我在程序流中包含了这两个 `open()` 语句，尽管后者被注释掉了。你选择使用哪一个？注释掉你不需要的那行，或者完全删掉它。

### 示例 11.8 - word_lengths.cpp

```cpp
#include <iostream>    // 程序将在屏幕上显示一些文本
#include <fstream>       // 程序将使用文件
using namespace std;               // 将使用标准标识符 string, cout 和 endl
int main()
{
    int numEntriesFound = 0;
    // 告诉用户将发生什么
    cout << "Enter number of characters to search for" << endl;
    unsigned int chars;
    cin >> chars;
    // 尝试打开当前登录用户的历史文件 
    ifstream dictionaryFile;
    dictionaryFile.open("wordlist");
    // 检查文件是否存在并可以被打开
    if (historyFile.good())
    {
        // 如果文件成功打开，则读取文本
        string lineText;
        while (getline(dictionaryFile, lineText))
        {
            // 读取单个字符
            if (lineText.length() == chars)
            {
                cout << lineText << endl;
                numEntriesFound++;
            }
        }
        // while 结束 - 在读取最后一行后结束
        cout << endl << "**** End of file reached ****" << endl;
        // 告诉计算机你已经完成了文件的使用
        dictionaryFile.close();
    }
    else
    {
        cout << "ERROR! Could not read from the Bash history file!" << endl;
    }
    cout << endl << endl << "File closed." << endl;
    return 0;
}
```

```cpp
cout << endl; // 显示空行
// 提示用户输入一个字母 - 将搜索以该字母开头的单词
cout << "Starting with letter (or * for all)" << endl;
char firstLetter;
cin >> firstLetter;
firstLetter = toupper(firstLetter); // 将将不区分大小写
cout << endl; // 显示空行
// 尝试打开字典文件 - 请根据你的系统使用正确的文件名
f-stream dictionaryFile;
dictionaryFile.open("/usr/share/dict/british-english");
// dictionaryFile.open(wordlist.txt);
// 如果文件成功打开，则读取文件内容
if (dictionaryFile.good()) {
    // 逐行读取文件内容
    string lineOf;
    while (getline(dictionaryFile, lineOf)) {
        // 检查文件中的单词是否是用户寻找的
        if (lineOf.length() == chars) {
            if (firstLetter == '*' || (toupper(lineOf.at(0)) == firstLetter)) {
                cout << lineOf << endl;
                numEntriesFound++;
            }
        }
    }
}
cout << endl << "*** End of search ***" << endl;
// 电脑你已完成文件的使用。
dictionaryFile.close();
cout << endl << endl; // 显示空行
// 显示找到的单词摘要
cout << "Found " << numEntriesFound;
cout << " entries with this number of characters." << endl;
} else {
    cout << "ERROR! COULD NOT READ FROM FILE!!!" << endl;
}
return 0;
```

你可以看到当我搜索以字母 `z` 开头的三个字母单词时发生了：

```
Enter number of chars to search for
3
Starting with letter (or * for all)
z
Z's
Zen
Zoe
zap
zed
zip
it
zoo
*** End of search ***
Found 8 entries with this number of characters.
```

你还可以看到 `*` 通配符对所有首字母都有效：

```
Enter number of chars to search for
23
Starting with letter (or * for all)
*
electroencephalograph's
*** End of search ***
Found 1 entries with this number of characters.
```

### 如何更高效地搜索排序后的数据

对于按字母顺序排列的单词文件，程序实际上可以变得更高效。如果用户想找到所有以特定字母开头的单词，一旦找到了以该字母开头的单词，就没有必要继续搜索文件的其余部分了，因为找不到其他匹配的单词。

逐行读取文件的 `while` 循环可以在找到一个单词的字母超过了用户感兴趣的特定字母时终止。例如，如果你想找到所有以字母 `s` 开头的单词，那么在此之后继续搜索是没有意义的，因为程序保证不会找到任何有用信息：

```cpp
// 如果超过了用户想要的字母，则停止搜索
if (lineOf.at(0) > firstLetter) {
    break;
}
```

请注意，`usr/share/dict/british-english` 的内容实际上并不是按字母顺序排列的。如果你在文本编辑器中查看该文件，你会发现以大写字母开头的单词列在前面，接着是小写字母开头的单词，最后是以重音符号等特殊字符开头的单词。

### 数据的不同排序方式

为什么 `/usr/share/dict/british-english` 文件的顺序是这种，而不是你在书架上的印刷字典中看到的严格字母顺序呢？因为该文件最初是由某人使用扩展 ASCII 字符集中的字符顺序进行排序的。

注意在 ASCII 中，字符 `À` 在字符集中总是出现在字符 `a` 之前。同样地，在扩展 ASCII 中，特殊的“罗马罗马”字符出现在小写字母之后。这意味着 `É`、`é`、`é` 和 `é` 出现在常规的小写字母之后。

由于字符集中字符代码的顺序通常用于在内存或文件中对数据进行排序，这导致创建了并非严格按`字母顺序`（alphabetic order）排序的数据。这种数据被称为`字典序排序的`（lexicographically sorted）——即按照不同符号在字符集中的顺序进行排序。在这里，字典文件条目 `ESPs` 可以出现在 `earthworm` 之前，而 `earthworm` 又在 `Emigre` 之前。

### 使用数组存储并处理来自文件的数据

有时，程序需要重复使用来自文件的数据。为了节省时间，一次性读取所有数据并存储在计算机内存中反复使用会很有帮助。（这假设内存中有足够的空间来容纳整个文件的内容）。

接下来，创建一个包含一些简单数据的文本文件并将其保存为文件名 `places`。

这是一个我使用 Nano 创建的 `places` 文件的示例：

| Exeter |
| Portree |
| London |
| Dundee |
| Swansea |
| Bristol |
| Glasgow |
| Belfast |
| Leeds |
| Cardiff |
| Manchester |
| Sheffield |
| Plymouth |

下一页的 **示例 11.10 - read_into_array.cpp** 从 `places` 文件中读取名称到计算机内存中。它将其存储在一个名为 `placeName` 的 `string` 类型单值数组中。

程序随后会选取一个随机数，称为 `choice`。它使用这个随机数作为 `placeName` 数组的索引。程序随后会选取一个随机数，称为 `choice`。它使用这个随机数作为 `placeName` 数组的索引来选择一个神秘地点，称之为 `secretName`。为了让它更容易，电脑会显示神秘地点有多少个字母以及以什么字母开头。

### 示例11.10 - read_into_array.cpp

```cpp
#include <iostream>    // 将在屏幕上显示
#include <fstream>     // 将使用文件
#include <cstdlib>     // 将使用 rand() 和 srand() 函数
#include <ctime>        // 使用 time() 函数作为随机种子
using namespace std;           // 使用标准标识 string, cout 和 endl
int main() {
    int errorCode = 0;
    const int MAX_PLACES = 30;
    // 用于存储从文件中读取的不同地点的数组
    string playerName[MAX_PLACES];
    int howManyPlaces = 0;
    // 尝试打开文件
    ifstream myFile;
    myFile.open("places");
    // 如果无法打开文件，退出程序
    if (!myFile.good()) {
        cout << "CAN'T FIND FILE." << endl;
        exit(1);
    }
    // 打开了文件，读取地点名称并存数组
    string onePlace;
    while (myFile.good() && howManyPlaces < MAX_PLACES) {
        getline(myFile, onePlace);
        playerName[howManyPlaces] = onePlace;
        howManyPlaces = howManyPlaces + 1;
    }
    // 设置随机数种子使选择变得随机
    srand(time(0));
    // 通过为数组选择随机索引选取地点
    int choice = rand() % howManyPlaces;
    string secretName = playerName[choice];
    // 显示地名的长度作为线索
    cout << "I have " << secretName.length() << " letters..." << endl;
    // 显示地名的首字母作为另一个线索
    cout << "My first letter is " << secretName.at(0) << endl;
    // 要求用户猜测地点名称
    string guess = "";
    while (guess != secretName) {
        cout << "Guess the place..." << endl;
        cin >> guess;
        if (guess == secretName) {
            cout << "YOU GOT IT!" << endl;
        } else {
            cout << "Nope! Keep trying." << endl;
        }
    } // 控制猜测的循环循环结束
    return errorCode;
}
```

继续...

这是程序运行的一个示例：

| I have 8 letters... |
| My first letter is P |
| Guess the place... |
| Penzance |
| Nope! Keep trying. |
| Guess the place... |
| Plymouth |
| YOU GOT IT! |

# 创建一个简单的拼写检查器

此程序利用了我们目前学到的技术来打开文件并将值读取到数组中，以便对其进行搜索。

该程序模拟了一个你在文字处理器中可能会使用的简单拼写检查器。它从词汇字典文件 `wordlist`（在示例 11.8 - `word_lengths.cpp` 中已使用）读取一个可接受的拼写列表，并将其存储在一个名为 `wordArray` 的数组中。当用户输入一个字符串值时，计算机会在数组中搜索对应的单词，如果找到，则判断为拼写正确；否则，则判断为未识别的单词或包含拼写错误的单词。

# 示例 11.11 - spell_check.cpp

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本作为输出
#include <fstream>       // 程序将使用文件操作
using namespace std;               // 将使用标准标识符 string, cin, cout, endl
//
// 此常量值将被程序的所有部分使用（全局常量）
const int MAX_WORDS = 100000;      // 这足够一个典型的字典文件使用
//
```
