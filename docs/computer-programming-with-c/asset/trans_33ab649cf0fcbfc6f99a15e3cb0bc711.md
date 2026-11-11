
## 草稿区

该程序执行以下步骤：

- 1. 将数组 a 的前 m 个元素复制到名为 temp 的临时数组中。
- 2. 将数组 a 中的位置向左移动 m 位。这将覆盖数组 a 中的前 m 个位置。
- 3. 将数组 temp 中存储的 m 个位置复制为数组 a 的最后 m 个位置。

例如，假设我们需要将下图所示的数组 a 旋转 2 位

![](img/57c0d966bb33c67a5a188e6bf39e4e02_292_0.png)

按照步骤 1，我们将把数组 a 的前两个元素复制到数组 temp 中，如下所示：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_292_1.png)

复制操作完成后，我们将数组 a 的元素向左移动两个位置。因此，数组 a 的新状态如下所示：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_292_2.png)

最后一步，我们将数组 temp 复制到数组 a 的最后两个位置，如下所示：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_292_3.png)

程序会打印结果数组，如输出所示。

## 已解示例 6.7

编写一个执行字符串复制操作的程序。从用户处接收数组 a 中的字符串作为输入，然后将数组 a 中的字符串复制到另一个数组 b 中。

```c
#include<stdio.h>
void main()
{
    int len=0,i,k;
    char a[100],b[100];
    /*Input string in a from the user*/
    printf("Enter a source string: ");
```

```c
lenB++;
}
/*Copy string a in array c*/
for(i=0;i<=lenA-1;i++)
{
c[i]=a[i];
}
/*Append string b to array c after the last character*/
k=0;
for(i=lenA;b[k]!='\0';i++)
{
c[i]=b[k];
k++;
}
/*Store NULL character in array c*/
c[i]='\0';
printf("Concatenation of strings is: %s",c);
}
```

### 输出

Enter first string:Com
Enter second string:puter
Concatenation of strings is: Computer

## 已解示例 6.9

编写一个程序，从用户处接收一个字符串作为输入，并将该字符串转换为大写。例如，如果用户输入的字符串为 hello123，则输出必须是 HELLO123。注意，字符串中的数字部分不应受到影响；只有小写字母必须转换为大写。

```c
#include<stdio.h>
void main()
{
char a[100];
printf("Enter a string in lower case: ");
scanf("%s",a);
/*Subtract 32 from the ASCII value only if the a[i] is in lower case*/
for(int i=0;a[i]!='\0';i++)
{
if(a[i]>=97 &&a[i] <=122)
{
    a[i] = a[i]-32;
}
}
printf("Upper Case is: %s\n",a);
}
```

### 输出

Enter a string in lower case: hello123
Upper Case is: HELLO123

## 草稿区

小写字符的 ASCII 值从 97 到 122，而大写字符的 ASCII 值从 65 到 90。这意味着我们可以通过从其 ASCII 值中减去 32，将任何小写字符转换为大写字符（ASCII 值参见附录 1）。

因此，我们遍历数组 a，并如下所示从其 ASCII 值中减去 32：

```c
for (int i=0;a[i]!='\0';i++)
{
    if(a[i]>=97 &&a[i] <=122)
    {
        a[i] = a[i]-32;
    }
}
```

注意，减法是在 if 块内执行的，以确保不会对输入字符串中可能存在的特殊字符、数字等执行减法。这样，我们确保只有小写字符会因转换为大写而受到影响，而数组 a 中的数字、特殊符号或已有的大写符号不会受到影响。

## 已解示例 6.10

编写一个程序，从用户处接收一个句子作为输入，并确定某个特定字符在句子中出现的频率。该程序应从用户处接收一个句子以及一个字符作为输入，并打印该字符在句子中出现的次数。

例如，如果用户输入的句子为‘I like Cricket’，字符为‘i’，则程序的输出必须是 3，因为字符‘i’在输入句子中出现了 3 次，如图 6.45 所示。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_296_0.png)

**图 6.45：** I like cricket

注意，程序应统计该字符在输入句子中以大写或小写形式出现的次数，而不论用户输入该字符时使用何种大小写。

```c
#include<ctype.h>
#include<stdio.h>
void main()
{
    int i,count=0;
    char a[100];
    char ch;
    printf("Enter a sentence:");
    gets(a);
    printf("Enter a character:");
    scanf("%c",&ch);
        for(i=0;a[i]!='\0';i++)
        {
            if(toupper(a[i])==toupper(ch))
            {
                count++;
            }
        }
    printf("Character %c occurs %d times in the sentence.\n",ch,count);
}
```

```
Output
Enter a sentence:I like Cricket
Enter a character:i
Character i occurs 3 times in the sentence.
```

## 注意

由于我们需要从用户处接收一个句子作为输入，因此使用了函数 gets()。我们不能使用 scanf() 来输入句子，因为它无法将空格作为输入读取。我们使用通常的 scanf() 语句将需要确定频率的字符存储到变量 ch 中，如代码所示。

## 草稿区

我们使用 for 循环遍历整个句子，并在每次在句子中找到字符 ch 时递增变量 count 的值。注意，在执行 `a[i]` 和 `ch` 的匹配时，我们使用了函数 `toupper()`。这意味着我们强制将待比较的字符转换为大写，以确保匹配过程不区分大小写，并且用户输入数据时使用的大小写不会对比较产生任何影响。用于比较的循环如下所示：

```cpp
for(i=0;a[i]!='\0';i++)
{
    if(toupper(a[i])==toupper(ch))
    {
        count++;
    }
}
```

因此，变量 count 将表示该字符在输入句子中的频率。

## 注意

函数 `toupper()` 会在字符当前不是大写时将其转换为大写。如果字符已经是大写，则不会影响它。此外，该函数不会影响数字和特殊符号。由于我们在比较中对两侧都应用了 `toupper()`，它只是确保匹配在忽略大小写的情况下执行，这正是题目中的要求。我们也可以使用 `tolower()` 函数代替 `toupper()`；请记住，这里唯一的要求是强制将两侧统一为相同的大小写，以便它们之间的大小写差异（如果有）不会妨碍比较结果。这两个函数都定义在头文件 `ctype.h` 中，必须将该头文件包含在程序中。

## 已解示例 6.11

编写一个程序，从用户处接收一个句子作为输入，并反转句子中单词的出现顺序。注意，程序不应反转单词内部的字符。例如，如果用户输入的字符串为 "I like computer programming"，则输出必须是：

`programming computer like I`

```c
#include<stdio.h>
void main()
{
    char a[100];
int len=0,i;
printf("Enter a sentence: ");
gets(a);
printf("*****Reverse is******\n");
/* Calculate the length of the string */
for(i=0;a[i]!='\0';i++)
{
    len++;
}
for(i= len; i>=0; i--)
{
    if (i != len && a[i]!=' ')
    {
        continue;
    }
    else
    {
        /*take the variable i to the beginning of a particular word*/
        while(a[i]!=' ' && i>=1)
        {
            i--;
        }
        //print the word in forward direction
        while (i< len && a[i]!=' ')
        {
            printf("%c",a[i]);
            i++;
        }
        printf(" "); //print the space
        i--; /*reduce value of i as space is already printed*/
    }
}
}
```

### 输出

```
Enter a sentence: I like Cricket
*****Reverse is******
Cricket like I
```

## 草稿区

反转句子中单词顺序的程序工作方式如下：

### 步骤 1：计算句子的长度

使用以下 for 循环计算输入句子的长度，并将其存储在变量 len 中。

```c
for(i=0;a[i]!='\0';i++)
{
    len++;
}
```

### 步骤 2：反向遍历句子

计算出长度后，我们使用另一个 for 循环开始反向读取句子，如下所示：

```c
for(i= len; i>=0; i--)
{
    ------------
    ------------
    ------------
}
```

写在此 for 循环内的 if 块会执行 continue;，直到计数器变量 i 位于某个特定单词末尾之后。句子中的所有中间单词后面都会有一个空格，因此很明显，如果 a[i] 是空格，则意味着我们正好位于该单词末尾之后。句子中最后一个单词的情况不同，它后面没有任何空格。在这种情况下，变量 i 将越过位置 len-1（即句子中最后一个字符的位置）。因此，当 i 初始化为 len 时，意味着我们已经越过了最后一个单词。总之，如果满足以下条件，我们就位于某个特定单词之后的位置：

- 1. `a[i]` 等于空格（对于句子中的中间单词）
- 或
- 2. 变量 i 取得值 len（这意味着 i 已越过位置 len-1）。这会发生在句子的最后一个单词的情况下。

如果我们位于某个特定单词末尾之后的位置，则有步骤 3 和步骤 4 中描述的两个 while 循环。步骤 3 中的 while 循环实际上会将 i 带到单词的开头，而步骤 4 中的 while 循环会从单词开头开始打印该单词。请记住，我们不需要反转单个单词，因此当 i 位于单词末尾之后的位置时，我们首先将其带到单词的开头，并按正向打印该单词。

如果我们不在单词末尾之后的位置，则确实没有什么可做的。因此，如果检测单词结束的两个条件都为假，我们就只是继续循环，不执行任何操作。这是通过 for 循环中的 if 块完成的，如下所示：

```c
if (i!= len && a[i]!= ' ')
{
```

