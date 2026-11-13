

{
    k++;
    j++;
}
if(pat[j]=='\0')
{
    copy_loop=k;
    while(rep_pat[rep_index] != '\0')
    {
        new_str[n] = rep_pat[rep_index];
        rep_index++;
        n++;
    }
}
new_str[n] = str[copy_loop];
i++;
copy_loop++;
}
new_str[n]='\0';
printf("\n The new string is : ");
puts(new_str);
getch();
return 0;
}

### 输出

输入字符串：How Are You?
输入要替换的模式：ARE
输入替换模式：are
新字符串是：How are you?

## 4.3 字符串数组

到目前为止，我们已经看到字符串是一个字符数组。例如，如果我们说 char name[] = "Mohan"，那么 name 是一个字符串（字符数组），它有五个字符。

现在，假设一个班级有 20 名学生，我们需要一个字符串来存储所有 20 名学生的姓名。如何实现？这里，我们需要一个字符串的字符串或字符串数组。这样的字符串数组将存储 20 个独立字符串。字符串数组声明为 char names[20][30]；

在这里，第一个索引将指定需要多少个字符串，第二个索引将指定每个单独字符串的长度。因此，这里我们将为 20 个名字分配空间，每个名字最长可为 30 个字符。

让我们来看看字符串数组的内存表示。如果我们有一个声明为 char name[5][10] = { "Ram", "Mohan", "Shyam", "Hari", "Gopal" } 的数组；

然后在内存中，数组将按图 4.13 所示存储。

| name[0] | R | A | M | '\0' | | | | |
|---|---|---|---|---|---|---|---|---|
| name[1] | M | O | H | A | N | '\0' | | |
| name[2] | S | H | Y | A | M | '\0' | | |
| name[3] | H | A | R | I | '\0' | | | |
| name[4] | G | O | P | A | L | '\0' | '\0' | |

图 4.13 二维字符数组的内存表示

```
Step 1: [INITIALIZE] SET I=0
Step 2: Repeat Step 3 while I< N
Step 3: Apply Process to NAMES[I]
[END OF LOOP]
Step 4: EXIT
```

通过声明数组 names，我们分配了 50 字节。但实际占用的内存是 27 字节。因此，我们看到大约一半的已分配内存被浪费了。图 4.14 显示了一个从字符串数组中处理单个字符串的算法。在第 1 步中，我们将索引变量 i 初始化为零。在第 2 步中，执行 while 循环，直到访问数组中的所有字符串。在第 3 步中，处理每个单独的字符串。

图 4.14 从字符串数组中处理单个字符串的算法

## 编程示例

### 10. 编写一个程序对学生姓名进行排序。

```
#include <stdio.h>
#include <conio.h>
#include <string.h>
int main()
{
char names[5][10], temp[10];
int i, n, j;
clrscr();
printf("\n Enter the number of students : ");
scanf("%d", &n);
for(i=0;i<n;i++)
{
printf("\n Enter the name of student %d : ", i+1);
gets(names[i]);
}
for(i=0;i<n;i++)
{
for(j=0;j<n-1-i;j++)
{
if(strcmp(names[j], names[j+1])>0)
{
strcpy(temp, names[j]);
strcpy(names[j], names[j+1]);
strcpy(names[j+1], temp);
}
}
}
printf("\n Names of the students in alphabetical order are : ");
for(i=0;i<n;i++)
puts(names[i]);
getch();
return 0;
}
```

### 输出

输入学生人数：3
输入第 1 名学生的姓名：Goransh
输入第 2 名学生的姓名：Aditya
输入第 3 名学生的姓名：Sarthak
按字母顺序排列的学生姓名为：Aditya Goransh Sarthak

### 11. 编写一个程序读取多行文本，然后统计文本中的字符数、单词数和行数。

```
#include <stdio.h>
#include <conio.h>
int main()
{
    char str[1000];
    int i=0, word_count = 1, line_count = 1, char_count = 1;
    clrscr();
    printf("\n Enter a ** to end");
    printf("\n***************************************");
    printf("\n Enter the text : ");
    scanf("%c", &str[i]);
    while(str[i] != '*')
    {
        i++;
        scanf("%c", &str[i]);
    }
    str[i] = '\0';
    i=0;
    while(str[i] != '\0')
    {
        if(str[i] == '\n' || i==79)
            line_count++;
        if(str[i] == ' ' && str[i+1] == ' ')
            word_count++;
        char_count++;
        i++;
    }
    printf("\n The total count of words is : %d", word_count);
    printf("\n The total count of lines is : %d", line_count);
    printf("\n The total count of characters is : %d", char_count);
    return 0;
}
```

### 输出

输入 ** 以结束
**************
输入文本：Hi there*
单词总数为：2
行总数为：1
字符总数为：9

### 12. 编写一个程序判断字符串是否为回文。

```
#include <stdio.h>
#include <conio.h>
int main()
{
    char str[100];
    int i = 0, j, length = 0;
    clrscr();
    printf("\n Enter the string : ");
    gets(str);
    while(str[i] != '\0')
    {
        length++ ;
        i++ ;
    }
    i=0;
    j = length - 1;
    while(i < length/2)
    {
        if(str[i] == str[j])
        {
            i++;
            j--;
        }
        else
            break;
    }
    if(i>j)
        printf("\n PALINDROME");
    else
        printf("\n NOT A PALINDROME");
    return 0;
}
```

### 输出

输入字符串：madam
PALINDROME

## 4.4 指针和字符串

在 C 语言中，字符串被视为以二进制零字符（写作 '\0'）结尾的字符数组。例如，

```
char str[10];
str[0] = 'H';
str[1] = 'I';
str[2] = '!';
str[3] = '\0';
```

C 语言提供了声明和初始化字符串的两种替代方法。首先，你可以写

```
char str[10] = { 'H', 'I', '!', '\0'};
```

但这比较麻烦，需要输入更多内容。因此，C 语言允许

```
char str[10] = "HI";
```

当使用双引号时，空字符 ('\0') 会自动附加到字符串末尾。

当以这种方式声明字符串时，编译器会预留一块连续的内存（即 10 字节长）来存放字符，并将其前四个字符初始化为 HI\0。

现在，考虑下面打印文本的程序。

```
#include <stdio.h>
int main()
{
    char str[] = "Hello";
    char *pstr;
    pstr = str;
    printf("\n The string is : ");
    while(*pstr != '\0')
    {
        printf("%c", *pstr);
        pstr++;
    }
    return 0;
}
```

### 输出

字符串是：Hello

在这个程序中，我们声明一个字符指针 *pstr 以在屏幕上显示字符串。然后，我们将指针 *pstr 指向 str。接着，我们使用 while 循环打印字符串的每个字符。与使用 while 循环相比，我们可以直接使用函数 puts()，如下所示

```
int puts(const char *s);
```

在这里，const 修饰符用于确保函数不会修改源指针所指向的内容。字符串的地址作为参数传递给函数。

传递给 puts() 的参数是一个指针，它无非就是它所指向的地址，或者简单说就是一个地址。因此，编写 puts(str) 意味着传递 str[0] 的地址。同样，当我们编写 puts(*pstr) 时，我们传递的是相同的地址，因为我们已经写了 pstr = str；

考虑另一个程序，它读取一个字符串，然后扫描每个字符以统计输入的大写和小写字符数量。

```
#include <stdio.h>
int main()
{
    char str[100], *pstr;
    int upper = 0, lower = 0;
    printf("\n Enter the string : ");
    gets(str);
    pstr = str;
    while(*pstr != '\0')
    {
        if(*pstr >= 'A' && *pstr <= 'Z')
            upper++;
        else if(*pstr >= 'a' && *pstr <= 'z')
            lower++;
        pstr++;
    }
    printf("\n Total number of upper case characters = %d", upper);
    printf("\n Total number of lower case characters = %d", lower);
    return 0;
}
```

### 输出

输入字符串：How are you
大写字符总数 = 1
小写字符总数 = 8

## 编程示例

### 13. 编写一个程序将一个字符串复制到另一个字符串中。

```
#include <stdio.h>
int main()
{
    char str[100], copy_str[100];
    char *pstr, *copy_str;
    pstr = str;
    copy_str = copy_str;
    printf("\n Enter the string : ");
    gets(str);
    printf(str);
    while(*pstr != '\0')
    {
```

