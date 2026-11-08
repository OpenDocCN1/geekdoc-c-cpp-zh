

```cpp
void initialize(int& lc, int list[])
{
    int i;
    lc = 0;

    for (i = 0; i < 26; i++)
        list[i] = 0;
} //end initialize

void copyText(ifstream& intext, ofstream& outtext, char ch,
              int list[])
{
    while (ch != '\n')       //process the entire line
    {
        outtext << ch;        //output the character

        characterCount(ch, list);   //call the function
                                     //character count
        intext.get(ch);       //read the next character
    }
    outtext << ch;            //output the newline character
} //end copyText

void characterCount(char ch, int list[])
{
    int index;

    ch = toupper(ch);                         //Step a

    index = static_cast<int>(ch)
          - static_cast<int>('A');            //Step b

    if (0 <= index && index < 26)              //Step c
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

## 示例运行（textout.out）：

今天，我们生活在一个信息几乎以光速被处理的时代。通过计算机，技术革命正在急剧改变我们生活和相互交流的方式。诸如“互联网”这样的术语，几年前还很陌生，如今已非常普遍。借助计算机，你可以在几秒钟内向亲人发送信件并收到他们的来信。你不再需要通过邮寄简历来申请工作；在许多情况下，你可以直接通过互联网提交求职申请。你可以实时查看股票行情，并即时买卖股票。学生们经常上网“冲浪”，并使用计算机设计课堂项目。他们还使用功能强大的文字处理软件完成学期论文。许多人在计算机上维护和平衡自己的支票簿。

```text
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

## 快速复习

- 1. 如果某种类型的变量一次只能保存一个值，则该数据类型是简单数据类型。
- 2. 在结构化数据类型中，每个数据项是其他数据项的集合。
- 3. 数组是一种具有固定分量数量的结构化数据类型。每个分量都具有相同的类型，并且通过分量在数组中的相对位置来访问它们。
- 4. 一维数组的元素以列表形式排列。
- 5. 不会检查数组下标是否越界。
- 6. 在 C++ 中，数组下标从 0 开始。
- 7. 数组下标可以是任何求值为非负整数的表达式。下标的值必须始终小于数组的大小。
- 8. 除了字符数组（C 字符串）的输入/输出外，数组没有聚合操作。
- 9. 数组可以在声明期间初始化。如果初始值少于数组大小，则其余元素初始化为 0。
- 10. 数组的基地址是第一个数组分量的地址。例如，如果 list 是一维数组，则 list 的基地址是 list[0] 的地址。
- 11. 将一维数组声明为形参时，通常省略数组大小。如果在形参声明中指定一维数组的大小，编译器将忽略该大小。
- 12. 在函数调用语句中，将数组作为实参传递时，只使用其名称。
- 13. 作为函数参数，数组只能按引用传递。
- 14. 由于数组作为参数只能按引用传递，因此将数组声明为形参时，不要在数据类型后使用符号 &。
- 15. 函数不能返回数组类型的值。
- 16. 尽管数组作为参数是按引用传递的，但在将数组声明为形参时，在数据类型前使用保留字 const 可防止函数修改该数组。
- 17. 单个数组分量可以作为参数传递给函数。
- 18. 顺序查找算法在列表中查找给定项，从列表中的第一个元素开始。它继续将查找项与列表中的其他元素进行比较，直到找到该项，或者列表中没有更多元素可与查找项比较为止。
- 19. 选择排序通过找到列表中最小的（或等价地，最大的）元素并将其移到列表的开头（或末尾）来对列表排序。
- 20. 对于长度为 n 的列表，选择排序恰好进行 n(n − 1)/2 次关键比较和 3(n − 1) 次元素赋值。
- 21. 在 C++ 中，字符串是包含在双引号之间的任意字符序列。
- 22. 在 C++ 中，C 字符串以空字符结尾。
- 23. 在 C++ 中，空字符表示为 '\0'。
- 24. 在 ASCII 字符集中，空字符的排序序列为 0。
- 25. C 字符串存储在字符数组中。
- 26. 字符数组可以在声明期间使用字符串表示法初始化。
- 27. C 字符串的输入和输出是 C++ 允许聚合操作的唯一地方。
- 28. 头文件 cstring 包含可用于 C 字符串操作的函数规范。
- 29. 常用的 C 字符串操作函数包括 strcpy（字符串复制）、strcmp（字符串比较）和 strlen（字符串长度）。
- 30. C 字符串逐字符进行比较。
- 31. 由于 C 字符串存储在数组中，因此可以使用数组分量访问表示法访问 C 字符串中的单个字符。
- 32. 并行数组用于保存相关信息。
- 33. 在二维数组中，元素以表格形式排列。
- 34. 要访问二维数组的元素，需要一对下标：一个表示行位置，一个表示列位置。
- 35. 在二维数组中，行编号为 0 到 ROW_SIZE - 1，列编号为 0 到 COLUMN_SIZE - 1。
- 36. 如果 matrix 是二维数组，则 matrix 的基地址是数组分量 matrix[0][0] 的地址。
- 37. 在行处理中，二维数组一次处理一行。
- 38. 在列处理中，二维数组一次处理一列。
- 39. 将二维数组声明为形参时，可以省略第一维的大小，但不能省略第二维的大小。
- 40. 将二维数组作为实参传递时，实参数组和形参数组的列数必须匹配。
- 41. C++ 在计算机内存中按行顺序形式存储二维数组。

## 练习

- 1. 判断以下陈述为真或假。
  - a. double 类型是简单数据类型的一个例子。
  - b. 一维数组是结构化数据类型的一个例子。
  - c. 数组既可以按值也可以按引用作为参数传递给函数。
  - d. 函数可以返回数组类型的值。
  - e. 数组的大小在编译时确定。
  - f. 对 `int` 数组唯一允许的聚合操作是递增和递减操作。
  - g. 给定声明：
    ```c
    int list[10];
    ```
    语句：
    ```c
    list[5] = list[3] + list[2];
    ```
    更新数组 list 第五个分量的内容。
  - h. 如果数组下标越界，程序总是因错误而终止。
  - i. 在 C++ 中，字符串允许某些聚合操作。
  - j. 声明：
    ```c
    char name[16] = "John K. Miller";
    ```
    将 name 声明为 15 个字符的数组，因为字符串 "John K. Miller" 只有 14 个字符。
  - k. 声明：
    ```c
    char str = "Sunny Day";
    ```
    将 str 声明为长度未指定的字符串。
  - l. 作为参数，二维数组既可以按值也可以按引用传递。
- 2. 考虑以下声明：
  ```c
  double passwords[100];
  ```
  在此声明中，标识以下内容：
  - a. 数组名。
  - b. 数组大小。
  - c. 每个数组分量的数据类型。
  - d. 数组下标的取值范围。
- 3. 指出以下数组声明中的错误（如果有）。如果语句不正确，请提供正确的语句。
  - a. `double weights[100];`
  - b. `int age[0..80];`
  - c. `string students[101];`
  - d. `int list[100];`
  - e. `double[50] salaries;`
  - f.
    ```c
    const double LENGTH = 30.00;
    double list[LENGTH];
    ```
  - g.
    ```c
    const int SIZE = 100;
    int list[SIZE - 1];
    ```

