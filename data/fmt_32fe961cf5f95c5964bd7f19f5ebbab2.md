
```
//****************************************************************************************************
```

```cpp
#include <iostream>
#include <fstream>
#include <iomanip>
using namespace std;
const int MAX_CODE_SIZE = 250;
void readCode(istream& infile, int list[], int& length, bool& lenCodeOk);
void compareCode(istream& infile, ostream& outfile, const int list[], int length);
```

```cpp
int main ()
{
    //Step 1
    int codeArray[MAX_CODE_SIZE]; //用于存储秘密代码的数组
    int codeLength; //用于存储秘密代码长度的变量
    bool lengthCodeOk; //用于指示秘密代码长度是否小于等于 250 的变量
    istream infile; //输入文件流变量
    ostream outfile; //输出文件流变量
    char inputFile[51]; //用于存储输入文件名的变量
    char outputFile[51]; //用于存储输出文件的变量
    cout << "Enter the input file name: ";
    cin >> inputFile;
    cout << endl;
    //Step 2
    infile.open(inputFile);
    if (!infile)
```

```cpp
cout << "Cannot open the input file." << endl;
return 1;
```

```cpp
cout << "Enter the output file name: ";
cin >> outputFile;
cout << endl;
```

```cpp
outfile.open(outputFile);
```

```cpp
readCode(infile, codeLength, //Step 3
lengthCodeCodeOK);
```

```cpp
if (lengthCodeOK) //Step 4
compareCode(infile, outfile, codeArray, lengthCode);
```

```cpp
else
cout << "Length of the secret code " "*must be <= " << MAX_CODE_SIZE << endl; //Step 5
```

```cpp
infile.close();
outfile.close();
```

```cpp
return 0;
}
// 在此处放置之前描述的 readCode 和 compareCode 函数的定义。
// 用户输入有阴影显示。
```

**示例运行：** 在此示例运行中，用户输入有阴影显示。

**Enter the input file name:** `Ch8_SecretCodeData.txt`

**Enter the output file name:** `Ch8_SecretCodeOut.txt`

**Input File Data:** (`Ch8_SecretCodeData.txt`)

7 9 2 7 8 3 5 6 7 9 2 7 8 3 5 6

**Output File Data:** (`Ch8_SecretCodeOut.txt`)

| Code Digit | Code Digit Copy |
| :--- | :--- |
| 9 | 9 |
| 2 | 2 |
| 7 | 7 |
| 8 | 8 |
| 3 | 3 |
| 5 | 5 |
| 6 | 6 |

**Message transmitted OK.**

# 编程示例：文本处理

（行数和字母计数）现在让我们编写一个程序，读取给定文本，按原样输出，并打印文本的行数以及每个字母在文本中出现的次数。大写字母和小写字母被视为相同；也就是说，它们会被合并计数。

由于有 26 个字母，我们使用一个包含 26 个组件的数组来执行字母计数。我们还需要一个变量来存储行数。

文本存储在一个文件中，我们将其命名为 `textin.txt`。输出将存储在一个文件中，我们将其命名为 `textout.out`。

- 输入：包含待处理文本的文件。
- 输出：一个包含文本、行数以及每个字母在文本中出现次数的文件。

（注：后续文本中存在大量重复段落，已根据要求仅翻译核心逻辑并保持格式）

586 | 第 8 章：数组与字符串

```cpp
void writeTotal(ofstream& outtext, int lc, int list[])
{
    outtext << endl;
    outtext << "The number of lines = " << lc << endl;
    for (int index = 0; index < 26; index++)
        outtext << static_cast<char>(index + static_cast<int>('A'))
                << " count = " << list[index] << endl;
}
//end writeTotal
```

我们现在描述 `main` 函数的算法。

- 1. 声明变量。
- 2. 打开输入文件。
- 3. 如果输入文件不存在，则退出程序。
- 4. 打开输出文件。
- 5. 初始化变量，如 `lineCount` 和数组 `letterCount`。
- 6. 读取第一个字符。
- 7. 当（未到输入文件末尾时）：
  7.1 处理下一行；调用函数 `copyText`。
  7.2 增加行数。（增加变量 `lineCount`）
  7.3 读取下一个字符。
- 8. 输出行数和字母计数。调用函数 `writeTotal`。
- 9. 关闭文件。

主算法

```cpp
完整程序代码列表
************************************************************************************
// 作者: D.S. Malik
//
// 程序: 行数与字母计数，按原输出文本，并且
// 该程序读取文本，输出行数以及每个字母
// 在文本中出现的次数。大写字母和小写字母
// 被视为是相同的；也就是说，
// 它们被合并在一起计数。
************************************************************************************
```

```cpp
#include <iostream>
#include <fstream>
#include <cctype>
using namespace std;
void initialize(int& lc, int list[]);
void copyText(istream& intext, ostream& outtext, char& ch, int list[]);
void characterCount(char ch, int list[]);
void writeTotal(ostream& outtext, int lc, int list[]);
int main()
{
    //Step 1: 声明变量
    int lineCount;
    int letterCount[26];
    char ch;
    ifstream infile;
    ofstream outfile;
    infile.open("textin.txt"); //Step 2
    if (!infile) //Step 3
    {
        cout << "Cannot open the input file." << endl;
        return 1;
    }
    outfile.open("textout.out"); //Step 4
    initialize(lineCount, letterCount); //Step 5
    infile.get(ch); //Step 6
    while (infile) //Step 7
    {
        copyText(infile, outfile, ch, letterCount); //Step 7.1
        lineCount++; //Step 7.2
        infile.get(ch); //Step 7.3
    }
    writeTotal(outfile, lineCount, letterCount); //Step 8
    infile.close(); //Step 9
    outfile.close(); //Step 9
    return 0;
}
```

```cpp
void initialize(int& lc, int list[])
{
    lc = 0;
    for (int j = 0; j < 26; j++)
        list[j] = 0;
} //end initialize
```

```cpp
void copyText(istream& intext, ofstream& outtext, char& ch, int list[])
{
    while (ch != '\n') //处理整行
    {
        outtext << ch; //输出字符
        characterCount(ch, list); //调用函数 character 计数
        intext.get(ch); //读取下一个字符
    }
    outtext << ch; //输出换行符
}//end copyText
```

```cpp
void characterCount(char ch, int list[])
{
    int index;
    ch = toupper(ch); //Step a
    index = static_cast<int>(ch) - static_cast<int>('A'); //Step b
    if (0 <= index && index < 26) //Step c
        list[index]++;
} //end characterCount
```

```cpp
void writeTotal(ofstream& outtext, int lc, int list[])
{
    outtext << endl;
    outtext << "The number of lines = " << lc << endl;
    for (int index = 0; index < 26; index++)
        outtext << static_cast<char>(index + static_cast<int>('A'))
                << " count = " << list[index] << endl;
} //end writeTotal
```

示例运行 (textout):

已知用于计算的第一个设备是算盘。算盘发明于亚洲，但在古代巴比伦、中国和整个欧洲一直使用到中世纪后期。算盘使用架子上的滑动珠子进行加减法。1642年，法国哲学家、数学家布莱兹·帕斯卡发明了一种名为“帕斯卡机”的计算设备。它带有轮子的移动拨盘，可以计算高达八位的数的和。算盘和帕斯卡机只能执行加法和减法运算。随后在17世纪后期，戈特弗里德·冯·莱尼茨发明了一种能够进行加、减、乘、除法的设备。

```
The number of lines = 62
A count = 16
B count = 29
C count = 32
D count = 54
E count = 7
F count = 9
G count = 9
H count = 24
I count = 45
J count = 0
K count = 30
L count = 8
M count = 33
N count = 30
O count = 0
P count = 0
Q count = 91
R count = 33
S count = 3
T count = 1
U count = 25
V count = 9
W count = 6
X count = 0
Y count = 6
Z count = 1
```

# 快速复习

- 1. 如果数据类型只能存储一个值，则它是简单类型。
- 2. 在结构数据类型中，每个数据都是其他数据的集合。
- 3. 数组是固定数量组件的结构数据类型。所有组件的类型相同，并通过相对位置访问。
- 4. 字符串是以空字符终止的字符数组。
- 5. 字符串可以使用引号括的字符面量进行初始化。
- 6. 字符串的长度通过计数直到空字符来确定。
- 7. 大写字母和小写字母被视为是相同的；也就是说，它们被合并在一起计数。
- 8. 数组索引是访问数组元素的整数。
- 9. 数组索引的范围是从 0 到 size - 1。
- 10. 字符串可以使用 `strcpy` 函数从一个拷贝到另一个。
- 11. 使用 `strlen` 函数找到字符串的长度。
- 12. 字符串可以使用 `strcat` 函数进行连接。
- 13. 字符串可以使用 `strcmp` 函数进行比较。
- 14. `cstring` 头文件提供了处理字符串的函数。
- 15. 字符串可以作为指针或数组传递给函数。
- 16. 数组不能从函数返回，但指针可以。
- 17. 数组可以使用指针在函数内部进行修改。
- 18. 多维数组是数组的数组。

# 练习题

练习末尾括号中的数字指的是章节开头列出的学习目标。

- 1. 判断下列陈述的对或错。
  a. `double` 类型是简单数据类型的示例。(1)
  b. 一维数组是结构化数据类型的示例。(1)
  c. 数组的大小在编译时确定。(1, 6)
  d. 假定以下声明：
  ```
  int list[10];
  ```
  语句：
  ```
  list[5] = list[3] + list[2];
  ```
  更新了数组 `list` 的第 5 个分量。(2)
  e. 如果数组索引越界，程序总是以错误形式终止。(3)
  f. 对 `int` 数组允许的唯一聚合操作是自增和自减操作。(5)
  g. 数组可以按值或按引用作为参数传递给函数。(6)
  h. 函数可以返回数组类型的值。(6)
  i. 在 C++ 中，字符串允许进行某些聚合操作。(11, 12, 13)
  j. 声明：
  ```
  char name[16] = "John K. Miller";
  ```
  声明 `name` 为一个包含 15 个字符的数组，因为字符串 "John K. Miller" 只有 14 个字符。(11)
  k. 声明：
  ```
  char str = "Sunny Day";
  ```
  声明 `str` 为一个长度未指定的数组。(11)
  l. 作为参数时，二维数组按值或按引用传递。(15, 16)

- 2. 考虑以下声明：(1, 2)
  ```
  double currentBalance[91];
  ```
  在该声明中，识别以下内容：
  a. 数组名称
  b. 数组大小
  c. 每个数组分量的数据类型
  d. 数组索引的取范围
  e. 第一个、中间和最后一个元素的索引分别是什么？

- 3. 识别以下数组声明中的错误（如果有）。如果语句不正确，请提供正确的语句。(1, 2)
  ```
  a. int primeNum[99];
  ```
  ```
  b. int testScores[0];
  ```
  ```
  c. string names[60];
  ```
  ```
  d. int list100[0..99];
  ```
  ```
  e. double[50] gpa;
  ```
  ```
  f. const double LENGTH = 26;
     double list[LENGTH - 1];
  ```
  ```
  g. const long SIZE = 100;
     int list[2 * SIZE];
  ```

- 4. 确定以下数组声明是否有效。如果声明无效，请解释原因。(1, 2)
  a. `int list[61];`
  b. `strings names[20];`
  c. `double[-50] ratings[];`
  d. `double flowers[35];`
  e. `int SIZE = 10;`
