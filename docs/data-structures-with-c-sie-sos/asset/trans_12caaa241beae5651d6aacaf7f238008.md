

4, 8, 6, 15, 9, 5, 4, 13, 8, 5, 11, 9, 9, 13, 7, 10, 6. 11

在这样的数组中，访问的基本单位通常是单个元素。连续元素的组通常没有任何特殊含义。

出于上述原因，已开发出各种字符串操作，这些操作通常不用于其他类型的数组。本节讨论这些面向字符串的操作。下一节展示这些操作在文字处理中的应用。（除非另有说明或暗示，我们假设字符型变量是动态的，其长度可变，由变量使用的上下文决定。）

### 子字符串

从给定字符串中访问子字符串需要三个信息：（1）字符串的名称或字符串本身，（2）子字符串在给定字符串中第一个字符的位置，（3）子字符串的长度或子字符串最后一个字符的位置。我们将此操作称为SUBSTRING。具体地，我们写

```
SUBSTRING(string, initial, length)
```

以表示字符串S从位置K开始且长度为L的子字符串。

### 示例 3.4

(a) 使用上述函数，我们有：

```
SUBSTRING('TO BE OR NOT TO BE', 4, 7) = 'BE OR N'
SUBSTRING('THE END' , 4, 4) = ' END'
```

### 程序 3.1

```
/* Code showing the implementation of SUBSTRING function in C */
#include <stdio.h>
#include <conio.h>

void main()
{
char S[80]=("TO BE OR NOT TO BE");
char *SUBSTR(char*,int,int);
clrscr();

printf("STRING = %s",S);
printf("\n\nSUBSTRING(S,4,7) = %s",SUBSTR(S,4,7));
getch();
}

char *SUBSTR(char *STR,int i,int j)
{
int k,m=0;
char STRRES[80];
for(k=i-1;k<=i+j-1-1;k++)
{
    STRRES[m]=STR[k];
    m=m+1;
}
STRRES[m]='\0';
return(STRRES);
}
```

输出：
STRING = TO BE OR NOT TO BE
SUBSTRING(S, 4, 7) = BE OR N

### 索引

索引，也称为模式匹配，是指查找字符串模式P在给定文本T中首次出现的位置。我们将此操作称为INDEX，并写

```
INDEX(text, pattern)
```

如果模式P在文本T中不出现，则INDEX被赋值为0。参数“text”和“pattern”可以是字符串常量或字符串变量。

### 示例 3.5

(a) 假设T包含文本
'HIS FATHER IS THE PROFESSOR'
那么，
INDEX(T, 'THE')、INDEX(T, 'THEN')和INDEX(T, ' THE')
的值分别为7、0和14。

### 程序 3.2

```
/* Code showing the implementation of INDEX function in C */
#include <stdio.h>
#include <conio.h>
#include <string.h>
void main()
{
char T[80]=("HIS FATHER IS THE PROFESSOR");
int INDEX(char*,char*);
clrscr();
printf("T = %s",T);
printf("\n\nINDEX(T,'THE') = %d",INDEX(T,"THE"));
printf("\n\nINDEX(T,'THEN') = %d",INDEX(T,"THEN"));
printf("\n\nINDEX(T,' THE ') = %d",INDEX(T," THE "));
getch();
}

int INDEX(char *STR1,char *STR2)
{
 int m,n;
 int index,flag;
 for(m=0;m<strlen(STR1);m++)
 {
 index=m;
 flag=1;
 for(n=0;n<strlen(STR2);n++)
 {
 if(STR1[m+n]==STR2[n])
 ;
 else
 {
 flag=0;
 break;
 }
 }
 if(flag==0)
 continue;
 else
 return(index);
 }
 if(m==strlen(STR1))
 return(-1);
}
```

**输出：**
T = HIS FATHER IS THE PROFESSOR

INDEX(T,'THE') = 6

INDEX(T,'THEN') = -1

INDEX(T,' THE ') = 13

备注：由于0是C语言中的有效索引位置，我们使用-1表示模式与文本不匹配的情况。

### 连接

设S1和S2为字符串。回顾（第3.2节），S1和S2的连接，我们用S1//S2表示，是由S1的字符后跟S2的字符组成的字符串。

### 示例 3.6

(a) 假设S1 = 'MARK'且S2 = 'TWAIN'。那么：
S1//S2 = 'MARKTWAIN' 但 S1// ' ' //S2 = 'MARK TWAIN'

(b) 在C语言中，连接使用strcat函数执行，如下所示：
strcat(S1,S2); //Concatenates strings S1 and S2 and stores
the result in S1
strcat()函数是string.h头文件的一部分；因此必须在预处理时包含它。

### 程序 3.3

```
/* Code showing string concatenation in C */
#include <stdio.h>
#include <conio.h>
#include <string.h>

void main()
{
char S1[80]=("MARK");
char S2[80]=("TWAIN");
clrscr();

printf("S1 = %s",S1);
printf("\nS2 = %s",S2);
printf("\nS1//S2 = %s",strcat(S1,S2));
strcpy(S1,"MARK");
printf("\nS1//' '//S2 = %s",strcat(strcat(S1," "),S2));

getch();
}
```

输出：
S1 = MARK
S2 = TWAIN
S1//S2 = MARKTWAIN
S1//' '//S2 = MARK TWAIN

### 长度

字符串中的字符数称为其长度。我们将写

### LENGTH(string)

用于表示给定字符串的长度。

### 示例 3.7

(a) 假设S = 'COMPUTER'。那么：

LENGTH (S) = 8

同样，

LENGTH ('MARC TWAIN') = 10

(b) 在C语言中，字符串长度使用strlen函数确定，如下所示：

```
x = strlen("Sunrise"); //strlen function returns an integer value
7 and assigns it to the variable X
```

与strcat类似，strlen也是string.h的一部分，因此必须在预处理时包含该头文件。

### 程序 3.4

```
/* Code showing the use of strlen () in C */
#include <stdio.h>
#include <conio.h>
#include <string.h>

void main()
{
char S1[80]={"COMPUTER"};
char S2[80]={"MARC"};
clrscr();

printf("Length(%s) = %d",S1,strlen(S1));
printf("\nLength(%s) = %d",S2,strlen(S2));

getch();
}
```

输出：
Length(COMPUTER) = 8
Length(MARC) = 4

## 3.7 文字/文本处理

在早期，计算机处理的字符数据主要由数据项组成，例如姓名和地址。如今，计算机也处理印刷材料，例如信件、文章和报告。正是在这种后一种语境下，我们使用“文字处理”这一术语。

给定一些印刷文本，通常与文字处理相关的操作如下：

- (a) 替换。将文本中的一个字符串替换为另一个字符串。
- (b) 插入。在文本中间插入一个字符串。
- (c) 删除。从文本中删除一个字符串。

上述操作可以通过使用前一节讨论的字符串操作来执行。我们将在下面分别讨论每个操作时展示这一点。这些操作中的许多都内置于大多数编程语言中，或可以轻松定义。

### 插入

假设在给定文本T中，我们想要插入一个字符串S，使S从位置K开始。我们用以下方式表示此操作：

```
INSERT(text, position, string)
```

例如，

```
INSERT ('ABCDEFG', 3, 'XYZ') = 'ABXYZCDEFG'
INSERT ('ABCDEFG', 6, 'XYZ') = 'ABCDEXYZFG'
```

此INSERT函数可以使用前一节定义的字符串操作实现，如下所示：

```
INSERT(T, K, S) = SUBSTRING(T, 1, K – 1) /// SUBSTRING(T, K, LENGTH(T) – K + 1)
```

也就是说，位置K之前的T的初始子字符串（长度为K – 1）与字符串S连接，然后结果与T的其余部分连接，该部分从位置K开始，长度为LENGTH(T) – (K – 1) = Length(T) – K + 1。（我们隐含地假设T是动态变量，且T的大小不会变得过大。）

### 删除

假设在给定文本T中，我们想要删除从位置K开始且长度为L的子字符串。我们用以下方式表示此操作：

```
DELETE(text, position, length)
```

例如，

```
DELETE( ' ABCDEFG ', 4, 2) = ' ABCFG '
DELETE( ' ABCDEFG ', 2, 4) = ' AFG '
```

我们假设如果位置K = 0，则不删除任何内容。因此，

```
DELETE( ' ABCDEFG ', 0, 2) = ' ABCDEFG '
```

这种“零情况”的重要性将在后面体现。

DELETE函数可以使用前一节给出的字符串操作实现，如下所示：

```
DELETE(T, K, L) =
SUBSTRING(T, 1, K – 1)//SUBSTRING(T, K + L, LENGTH(T) – K – L + 1)
```

也就是说，位置K之前的T的初始子字符串与从位置K + L开始的T的终端子字符串连接。初始子字符串的长度为K – 1，终端子字符串的长度为：

LENGTH(T) - (K + L - 1) = LENGTH(T) - K - L + 1

我们还假设当K = 0时，DELETE(T, K, L) = T。

现在假设给定文本T和模式P，我们想要从T中删除模式P的第一个出现。这可以通过使用上述DELETE函数来完成，如下所示：

DELETE(T, INDEX(T, P), LENGTH(P))

也就是说，在文本T中，我们首先计算INDEX(T, P)，即P在T中首次出现的位置，然后计算LENGTH(P)，即P中的字符数。回顾，当INDEX(T, P) = 0时（即，当P不在T中出现时），文本T不发生更改。

- **示例 3.8**

  (a) 假设T = 'ABCDEFG'且P = 'CD'。那么INDEX(T, P) = 3且LENGTH(P) = 2。因此
  
  DELETE ('ABCDEFG', 3, 2) = 'ABEFG'
  
  (b) 假设T = 'ABCDEFG'且P = 'DC'。那么INDEX(T, P) = 0且LENGTH(P) = 2。因此，根据“零情况，”
  
  DELETE('ABCDEFG ', 0, 2) = ' ABCDEFG '
  
  如预期。

假设将文本T和模式P读入计算机后，我们想要删除文本T中模式P的每个出现。这可以通过反复应用

DELETE(T, INDEX(T, P), LENGTH(P))

直到INDEX(T, P) = 0（即，直到P不在T中出现）。完成此任务的算法如下。

- **算法 3.1：** 文本T和模式P在内存中。此算法删除T中P的每个出现。

  1. [查找P的索引。] 设K := INDEX(T, P)。
  2. 当K ≠ 0时重复：
     (a) [从T中删除P。]
         设T := DELETE(T, INDEX(T, P), LENGTH(P))
     (b) [更新索引。] 设K := INDEX(T, P)。
     [循环结束。]
  3. 写出：T。
  4. 退出。

我们强调，每次删除后，T的长度都会减少，因此算法必须停止。然而，循环执行的次数可能超过P在原始文本T中出现的次数，如下一个示例所示。

