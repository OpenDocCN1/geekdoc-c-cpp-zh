

## 面向对象程序设计 C++ 简化

```cpp
char ch;
clrscr( );
file.open("num.txt", ios::in);
cout << "file contents";
endl(cout);
while(file.eof( ) == 0)
{
    file.get(ch);
    cout.put(ch);
}
endl(cout);
cout << "Reversing contents";
endl(cout);
file.clear( );
file.seekg(0, ios::end);
count = file.tellg( );
while(x <= count)
{
    file.seekg(-x, ios::end);
    file.get(ch);
    cout.put(ch);
    x ++;
}
cout << endl;
file.close( );
getch( );
}
```

**OUTPUT:**

```text
file contents
Love is blind
I Love programming
Reversing contents
gnimmargorp evoL I
dnilb si evoL
```

**EXPLANATION:** Initially file is opened in the read mode and displayed. The file then reaches the end of file and error bit is set. It is a must to clear this end-of-file bit otherwise after setting the pointer to last character of the file we won't be able to read from the file. Number of characters in the file is then found out as:

```cpp
file.seekg(0, ios::end);
count = file.tellg();
```

Now to display reverse contents of the file we start from 1 and continue till `x <= count`. We read first character from end when `x = 1` as:

```cpp
file.seekg(-x, ios::end);
file.get(ch);
```

Which is displayed using `cout.put(ch)`. As `x` increments we have the second character and so on.

```cpp
/* PROG 12.15 RANDOM ACCESS DEMO, PRINTING NAME "PARI" */

#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main()
{
    fstream file;
    char ch;
    clrscr();
    file.open("alpha.txt", ios::out);
    file << "ABCDEFGHIJKLMNOPQRST\n";
    file.close();
    file.open("alpha.txt", ios::in);
    // file character is at 0 pos
    // 16th byte from beginning
    file.seekg(15, ios::beg);
    file.get(ch);
    cout << ch; // prints P
    // first character from the beginning
    file.seekg(0, ios::beg);
    file.get(ch);
    cout << ch; // prints A
    // 3rd character from end, i.e., at -3, 'R'
    file.seekg(-3, ios::end);
    file.get(ch);
    cout << ch; // prints R
    // 10th character from current position
    // including current pos 'I'
    file.seekg(-10, ios::cur);
    file.get(ch);
    cout << ch; // prints I
}
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_605_0.png)

**Figure 12.7.** *Output screen of the program 12.17.*

**EXPLANATION:** We have assumed that file `silly` does not exist. The `ios::nocreate` does not open the file if it is not already existing and instead gives error. The error in opening is checked using `file.fail()` which returns true if there is some error in opening the file. As file does not exist, if condition is true so `cout` displays “File opening error” and program terminates.

```cpp
/* PROG 12.18 READING AND WRITING NUMERIC DATA */

#include <iostream.h>
#include <fstream.h>
#include <conio.h>
void main( )
{
    int i;

    clrscr( );

    ofstream file("num.txt");
    for(i = 1; i <= 10; i++)
        file << i << endl;
    file.close( );
    ifstream file1("num.txt");
    while(1)
    {
        file1 >> i;
        if(file1.eof( ) != 0)
            break;
        cout << i << endl;
    }
    file1.close( );
}
```

**OUTPUT:**

```text
1
2
3
4
5
6
7
8
9
10
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_606_0.png)

**Figure 12.8.** *Output screen of program 12.18.*

**EXPLANATION:** The program is simple. We input 10 numbers into the file and later display it back. Note there is no special function available in C++ for handling numbers using files.

## 12.7 命令行参数

在迄今为止我们使用过的所有程序中，我们都以无参数的方式编写了 `main()`，但实际上 `main()` 确实接受参数并且也有返回类型。`main()` 在 C++ 中的原型为：

```cpp
int main(int argc, char * argv[])
```

或

```cpp
int main(int argc, char ** argv)
```

传递的参数数量被收集到参数 `argc` 中，其代表 argument count。每个参数的值存储在字符串数组 `argv` 中，其代表 argument value。所有参数的类型均为字符串，无论它们是 int、float 还是字符。默认情况下，如果未指定任何函数的返回类型，则假定为 `int`；因此 `main()` 前的 `int` 是可选的。为更好地理解，请参阅以下示例。

这里总共有 4 个参数存储在 `argc` 中，每个命令行参数之间有一个空格。第一个参数是文件名本身，我们没有打印它；`F19.exe` 存储在 `argv[0]` 中，第二个参数 `HELLO` 存储在 `argv[1]` 中，以此类推。参数名 `argc` 和 `argv` 并非固定。它们可能是其他名称。

```cpp
/* PROG 12.20 SUM OF COMMAND LINE ARGUMENT */

#include <iostream.h>
#include <stdlib.h>
void main(int argc, char **argv)
{
    int i, sum = 0;
    for(i = 0; i < argc; i++)
        sum = sum + atoi(argv[i]);
    cout << "Sum is " << sum << endl;
}
```

**OUTPUT:**

```text
C:\TC>F20 1 2 3 4 5 6 7 8 9
Sum is 45
C:\TC>
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_608_0.png)

**Figure 12.11.** *Output screen of program 12.20.*

**EXPLANATION:** As mentioned in the previous program, the arguments supplied at command line are by default treated as strings. We run the program as:

```text
F20 1 2 3 4 5 6 7 8 9
```

Now starting from second argument, i.e., 1, each argument is converted into integer with the help of built-in function `atoi` whose prototype is given in file `stdlib.h` and summed up in variable `sum`.

/* PROG 12.21 MAX OF COMMAND LINE ARGUMENTS, FLOAT DATA */

```cpp
#include <iostream.h>
#include <stdlib.h>

void main(int argc, char **argv)
{
    int i;
    float max, t;
    max = atof(argv[1]);
    for(i = 1; i < argc; i++)
    {
        t = atof(argv[i]);
        if(max < t)
            max = t;
    }
    cout << "max is" << max << endl;
}
```

**OUTPUT:**

```text
C:\TC>f21 4.5 6.7 2.34 56.8 78.90
max is78.900002
C:\TC>
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_609_0.png)

**Figure 12.12.** *Output screen of program 12.21.*

**EXPLANATION:** Program is self-explanatory. See previous program's explanation.

```cpp
/* PROG 12.22 SORTING COMMAND LINE ARGUMENTS */

#include <iostream.h>
#include <string.h>

void main(int argc, char **argv)
{
    char *temp;
    int i, j;
    for(i = 1; i < argc; i++)
    {
        for(j = i + 1; j < argc; j++)
            if(strcmp(argv[i], argv[j]) > 0)
            {
                temp = argv[i];
                argv[i] = argv[j];
                argv[j] = temp;
            }
    }
    for(i = 1; i < argc; i++)
        cout << argv[i] << endl;
}
```

**OUTPUT:**

```text
C:\TC>F22 ONE TWO THREE FOUR
FOUR
ONE
THREE
TWO
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_610_0.png)

**Figure 12.13.** *Output screen of program 12.22.*

**EXPLANATION:**

The program is run as

```text
C:\TC>F22 ONE TWO THREE FOUR
```

As shown in above figure. The logic for sorting the string has been covered in earlier chapter.

```cpp
/* PROG 12.23 COPYING OF ONE FILE INTO ANOTHER WITH FILE NAMES SUPPLIED AS COMMAND LINE ARGUMENTS */

#include <iostream.h>
#include <fstream.h>
#include <stdlib.h>
void main(int argc, char **argv)
{
    fstream f1, f2;
    char ch;
    cout << argc << endl;
    if(argc != 3)
    {
        cout << "Usage: <filename> <source file> <dest file>";
        exit(0);
    }
    f1.open(argv[1], ios::in);
    f2.open(argv[2], ios::out);
    if(f1.fail())
    {
        cout << "File opening error";
        exit(0);
    }
    while(f1.eof() == 0)
    {
        f1.get(ch);
        f2.put(ch);
    }
    f1.close();
    f2.close();
}
```

**EXPLANATION:** In the program we take the source file and destination file as command line arguments. If number of arguments are not there, we flash an error message. Similarly, if there is error in opening the source file, flash error. If all goes well we copy file into destination character by character basis.

## 12.8 使用二进制模式工作

数值数据包括整数和浮点数以及字符数据，所有这些都以字符数据即字符串的形式处理，例如字符串 "file" 在内存中占用 4 个字节，整数 1245 在内存中占用 4 个字节，甚至 1.23 也占用 4 个字节。但这些数据存储

