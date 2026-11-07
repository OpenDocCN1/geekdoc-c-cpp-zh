
函数 `characterCount`，它需要数组 `letterCount` 来更新相应字母的计数。因此，我们必须将数组 `letterCount` 传递给 `copyText` 函数，以便它可以将该数组传递给函数 `characterCount`。

```cpp
void copyText(ifstream& intext, ofstream& outtext, char& ch,
              int list[])
{
    while (ch != '\n')        //process the entire line
    {
        outtext << ch;        //output the character
        characterCount(ch, list);    //call the function
                                    //character count
        intext.get(ch);       //read the next character
    }
    outtext << ch;            //output the newline character
} //end copyText
```

该函数递增字母计数。为了递增相应字母的计数，它必须知道该字母是什么。因此，characterCount 函数有两个参数：一个字符变量和用于更新字母计数的数组。用伪代码表示，该函数为：

- a. 将字母转换为大写。
- b. 找到该字母对应的数组索引。
- c. 如果索引有效，则递增相应的计数。在这一步，我们必须确保该字符是字母。我们只统计字母，因此其他字符——例如逗号、连字符和句点——会被忽略。

按照此算法，该函数的定义是：

```cpp
void characterCount(char ch, int list[])
{
    int index;

    ch = toupper(ch);                         //Step a

    index = static_cast<int>(ch)
          - static_cast<int>('A');             //Step b

    if (0 <= index && index < 26)              //Step c
        list[index]++;
} //end characterCount
```

该函数输出行数和字母计数。它有三个参数：输出文件流变量、行数以及用于输出字母计数的数组。该函数的定义是：

```cpp
void writeTotal(ofstream& outtext, int lc, int list[])
{
    int index;

    outtext << endl << endl;
    outtext << "The number of lines = " << lc << endl;

    for (index = 0; index < 26; index++)
        outtext << static_cast<char>(index
                 + static_cast<int>('A'))
                << " count = " << list[index] << endl;
} //end writeTotal
```

现在描述 main 函数的算法。

- 1. 声明变量。
- 2. 打开输入文件。
- 3. 如果输入文件不存在，则退出程序。
- 4. 打开输出文件。
- 5. 初始化变量，例如 lineCount 和数组 letterCount。
- 6. 读取第一个字符。
- 7. 当（未到输入文件末尾）时：
    - 7.1. 处理下一行；调用函数 copyText。
    - 7.2. 递增行数。（递增变量 lineCount。）
    - 7.3. 读取下一个字符。
- 8. 输出行数和字母计数。调用函数 writeTotal。
- 9. 关闭文件。

## 完整程序清单

```cpp
//************************************************************************
// Author: D. S. Malik
//
// Program: Line and Letter Count
// This program reads a text, outputs the text as is, and also
// prints the number of lines and the number of times each
// letter appears in the text. An uppercase letter and a
// lowercase letter are treated as being the same; that is,
// they are tallied together
//************************************************************************

void initialize(int& lc, int list[])
{
    int j;
    lc = 0;

    for (j = 0; j < 26; j++)
        list[j] = 0;
} //end initialize

void copyText(ifstream& intext, ofstream& outtext, char& ch,
              int list[])
{
    while (ch != '\n')          //process the entire line
    {
        outtext << ch;          //output the character

        characterCount(ch, list);   //call the function
                                    //character count
        intext.get(ch);             //read the next character
    }

    outtext << ch;              //output the newline character
} //end copyText

void characterCount(char ch, int list[])
{
    int index;

    ch = toupper(ch);                       //Step a

    index = static_cast<int>(ch)
          - static_cast<int>('A');          //Step b

    if (0 <= index && index < 26)           //Step c
        list[index]++;
} //end characterCount

void writeTotal(ofstream& outtext, int lc, int list[])
{
    int index;

    outtext << endl << endl;
    outtext << "The number of lines = " << lc << endl;

    for (index = 0; index < 26; index++)
        outtext << static_cast<char>(index
                  + static_cast<int>('A'))
                << " count = " << list[index] << endl;
} //end writeTotal
```

### 示例运行（textout.out）：

今天我们生活在一个信息几乎以光速被处理的时代。通过计算机，技术革命正在急剧改变我们生活和相互交流的方式。诸如“互联网”这样的术语，几年前还很陌生，如今已非常普遍。借助计算机，你可以在几秒钟内向亲人发送信件并收到他们的来信。你不再需要邮寄简历来求职；在许多情况下，你可以直接通过互联网提交求职申请。你可以实时查看股票行情，并立即买卖股票。学生们经常“冲浪”互联网，并使用计算机设计课堂项目。他们还使用强大的文字处理软件完成学期论文。许多人在计算机上维护和平衡支票簿。

```
The number of lines = 15
A count = 53
B count = 7
C count = 30
D count = 19
E count = 81
F count = 11
G count = 10
H count = 29
I count = 41
J count = 4
K count = 3
L count = 31
M count = 26
N count = 50
O count = 59
P count = 21
Q count = 0
R count = 45
S count = 48
T count = 62
U count = 24
V count = 7
W count = 15
X count = 0
Y count = 20
Z count = 0
```

## 快速回顾

- 1. 如果某种数据类型的变量一次只能保存一个值，则该数据类型是简单数据类型。
- 2. 在结构化数据类型中，每个数据项都是其他数据项的集合。
- 3. 数组是一种具有固定数量分量的结构化数据类型。每个分量都具有相同的类型，并且通过分量在数组中的相对位置来访问这些分量。
- 4. 一维数组的元素以列表形式排列。
- 5. 不会检查数组索引是否越界。
- 6. 在 C++ 中，数组索引从 0 开始。
- 7. 数组索引可以是任何求值为非负整数的表达式。索引的值必须始终小于数组的大小。
- 8. 除了字符数组（C 字符串）的输入/输出外，数组没有聚合操作。
- 9. 数组可以在声明期间初始化。如果初始值少于数组大小，则其余元素被初始化为 0。
- 10. 数组的基地址是第一个数组分量的地址。例如，如果 list 是一维数组，则 list 的基地址是 list[0] 的地址。
- 11. 将一维数组声明为形参时，通常省略数组大小。如果在形参声明中指定一维数组的大小，编译器将忽略该大小。
- 12. 在函数调用语句中，将数组作为实参传递时，只使用其名称。
- 13. 作为函数参数，数组仅按引用传递。
- 14. 由于数组作为参数时仅按引用传递，因此将数组声明为形参时，不要在数据类型后使用符号 &。
- 15. 函数不能返回数组类型的值。
- 16. 尽管数组作为参数时按引用传递，但在将数组声明为形参时，在数据类型前使用保留字 `const` 可以防止函数修改该数组。
- 17. 单个数组分量可以作为参数传递给函数。
- 18. 顺序搜索算法从列表的第一个元素开始，在列表中搜索给定项。它继续将搜索项与列表中的其他元素进行比较，直到找到该项，或者列表中没有更多元素可与搜索项进行比较。
- 19. 在 C++ 中，字符串是用双引号括起来的任意字符序列。
- 20. 在 C++ 中，C 字符串以 null 结尾。
