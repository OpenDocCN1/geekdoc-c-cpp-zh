
将 "Hello there World!" 连接到 dest_string。与 strcpy() 函数一样，程序员有责任确保目标C字符串定义得足够大，以容纳连接后的附加字符。

strlen() 函数返回其C字符串参数中的字符数，但不包括结尾的NULL字符。例如，函数调用 strlen("Hello World!") 返回的值是12。

最后，可以使用 strcmp() 函数比较两个字符串表达式是否相等。这种比较是逐个字符进行的，方式与第14.1节中针对string类对象描述的方式相同。程序15.5在一个完整的程序中使用这些C字符串函数。

## 程序15.5

```
#include <iostream>
#include <cstring>  // required for the string function library
using namespace std;
int main()
{
    const int MAXELS = 50;
    char string1[MAXELS] = "Hello";
    char string2[MAXELS] = "Hello there";
    int n;

    n = strcmp(string1, string2);

    if (n < 0)
        cout << string1 << " is less than " << string2 << endl;
    else if (n == 0)
        cout << string1 << " is equal to " << string2 << endl;
    else
        cout << string1 << " is greater than " << string2 << endl;

    cout << "\nThe length of string1 is " << strlen(string1)
         << " characters" << endl;
    cout << "The length of string2 is " << strlen(string2)
         << " characters" << endl;

    strcat(string1, " there World!");

    cout << "\nAfter concatenation, string1 contains "
         << "the string value\n" << string1
         << "\nThe length of this string is "
         << strlen(string1) << " characters" << endl;

cout << "\nType in a sequence of characters for string2: ";
 cin.getline(string2, MAXELS);

strcpy(string1, string2);

cout << "After copying string2 to string1, "
     << "the string value in string1 is:\n" << string2
     << "\nThe length of this string is "
     << strlen(string1) << " characters" << endl;

return 0;
}
```

以下是程序15.5产生的示例输出：

```
Hello is less than Hello there

The length of string1 is 5 characters
The length of string2 is 11 characters

After concatenation, string1 contains the string value
Hello there World!
The length of this string is 18 characters

Type in a sequence of characters for string2: It's a wonderful day
After copying string2 to string1, the string value in string1 is:
It's a wonderful day
The length of this string is 20 characters
```

## 字符处理函数

除了C字符串操作函数之外，所有C++编译器都包含第14.2节中介绍过的字符处理函数，为方便起见，这些函数在表15.3中再次列出。这些函数的原型位于头文件 ctype 中，任何使用这些函数的程序都应包含该头文件。

### 表15.3 字符库函数（需要头文件 string 和 ctype）

| 函数原型 | 描述 | 示例 |
|---|---|---|
| int isalpha(charExp) | 如果 charExp 求值为字母，则返回 true（非零整数）；否则返回 false（零整数）。 | isalpha('a') |
| int isalnum(charExp) | 如果 charExp 求值为字母或数字，则返回 true（非零整数）；否则返回 false（零整数）。 | isalnum(key); |
| int isupper(charExp) | 如果 charExp 求值为大写字母，则返回 true（非零整数）；否则返回 false（零整数）。 | isupper('A') |
| int islower(charExp) | 如果 charExp 求值为小写字母，则返回 true（非零整数）；否则返回 false（零整数）。 | islower('a') |
| int isdigit(charExp) | 如果 charExp 求值为数字（0 到 9），则返回 true（非零整数）；否则返回 false（零整数）。 | isdigit('5') |
| int isascii(charExp) | 如果 charExp 求值为 ASCII 字符，则返回 true（非零整数）；否则返回 false（零整数）。 | isascii('a') |
| int isspace(charExp) | 如果 charExp 求值为空格，则返回 true（非零整数）；否则返回 false（零整数）。 | isspace(' ') |
| int isprint(charExp) | 如果 charExp 求值为可打印字符，则返回 true（非零整数）；否则返回 false（零整数）。 | isprint('a') |

### 表15.3 字符库函数（需要头文件 string 和 cctype）（续）

| 函数原型 | 描述 | 示例 |
|---|---|---|
| int isctrl(charExp) | 如果 charExp 求值为控制字符，则返回 true（非零整数）；否则返回 false（零整数）。 | isctrl('a') |
| int ispunct(charExp) | 如果 charExp 求值为标点字符，则返回 true（非零整数）；否则返回 false（零整数）。 | ispunct('!') |
| int isgraph(charExp) | 如果 charExp 求值为除空白外的可打印字符，则返回 true（非零整数）；否则返回 false（零整数）。 | isgraph(' ') |
| int toupper(charExp) | 如果 charExp 求值为小写字符，则返回其大写等价形式；否则，返回未修改的字符代码。 | toupper('a') |
| int tolower(charExp) | 如果 charExp 求值为大写字符，则返回其小写等价形式；否则，返回未修改的字符代码。 | tolower('A') |

由于表15.3列出的所有 istype() 函数在字符满足条件时返回非零整数（解释为布尔真值），在条件不满足时返回零整数（解释为布尔假值），因此这些函数可以在 if 语句中使用。例如，请看以下代码段：

```
char ch;
ch = cin.get();  // get a character from the keyboard

if(isdigit(ch))
    cout << "The character just entered is a digit" << endl;
else if(ispunct(ch))
    cout << "The character just entered is a punctuation mark" << endl;
```

请注意，字符函数作为条件包含在 if 语句中。这是可能的，因为该函数返回布尔真（非零）或假（零）值。
程序15.6展示了在 ConvertToUpper() 函数中使用 toupper() 函数，该函数将所有小写字符串字符转换为大写形式。

## 程序15.6

```
#include <iostream>
using namespace std;

void ConvertToUpper(char []);  // function prototype

int main()
{
    const int MAXCHARS = 100;
    char message[MAXCHARS];

    cout << "\nType in any sequence of characters: ";
    cin.getline(message,MAXCHARS);

    ConvertToUpper(message);

    cout << "The characters just entered in uppercase are: "
         << message << endl;

    return 0;
}

// this function converts all lowercase characters to uppercase
void ConvertToUpper(char message[])
{
    for(int i = 0; message[i] != '\0'; i++)
        message[i] = toupper(message[i]);

    return;
}
```

程序15.6运行时的输出如下：

```
Type in any sequence of characters: this is a test OF 12345.
The characters just entered in uppercase are: THIS IS A TEST OF 12345.
```

请注意，toupper() 库函数仅转换小写字母；所有其他字符不受影响。

## 转换函数

最后一组标准字符串库函数，列于表15.4中，用于在C字符串与整数和双精度数据类型之间进行转换。这些函数的原型位于头文件 cstdlib 中，任何使用这些函数的程序都必须包含该头文件。程序15.7展示了使用 atoi() 和 atof() 函数的方法。

### 表15.4 字符串转换函数（需要头文件 cstdlib）

| 函数原型 | 描述 | 示例 |
|---|---|---|
| int atoi(stringExp) | 将 stringExp（一个 ASCII 字符串）转换为整数。转换在第一个非整数字符处停止。 | atoi("1234") |
| double atof(stringExp) | 将 stringExp（一个 ASCII 字符串）转换为双精度数。转换在第一个无法解释为双精度的字符处停止。 | atof("12.34") |
| char[] itoa(integerExp) | 将 integerExp（一个整数）转换为字符数组。为返回字符分配的空间必须足够大以容纳转换后的值。 | itoa(1234) |

程序15.7产生以下输出：

```
The string "12345" as an integer number is: 12345
This number divided by 3 is: 4115
The string "12345.96" as a double number is: 12345.96
This number divided by 3 is: 4115.32
```

