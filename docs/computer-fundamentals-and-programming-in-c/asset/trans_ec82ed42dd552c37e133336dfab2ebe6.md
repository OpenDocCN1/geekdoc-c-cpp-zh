

```c
printf("Enter a string");
gets(istr);
if((slen=strlen(istr))==0)
    break;          /* terminate */
strcpy(tstr,istr);          /* make a copy */
i = 0;
while(i < slen)              /* translate loop */
{
    if(tstr[i] >= 'A' && tstr[i] <= 'Z')
        tstr[i] += 'a'-'A';
    else if(tstr[i] >= 'a' && tstr[i] <= 'z')
        tstr[i] += 'A'-'a';
    i++;                      /* to next character */
}
printf("Original string = %s\n",istr);
printf("Transformed string = %s\n",tstr);
}
return 0;
}
```

## 输出

Enter string abDefgXYZ
Original string = abDefgXYZ
Transformed string = AbDEfGxyz
Enter string ab   CD   123
Original string = ab   CD   123
Transformed string = AB   cd   123

这个程序也可以写成如下形式，其中使用 '\0' 字符作为工具。

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char istr[128]; /* input buffer */
    char tstr[128]; /* translated string here */
    int i;
    int slen;       /* string length */
    while(1)
    {
        printf("Enter a string");
        gets(istr);
        if(strlen(istr)==0) break; /* terminate */
        strcpy(tstr,istr);         /* make a copy */
        i = 0;
        while(tstr[i]!='\0')       /* translate loop */
        {
            if(tstr[i] >= 'A' && tstr[i] <= 'Z')
                tstr[i] += 'a'-'A';
            else if(tstr[i] >= 'a' && tstr[i] <= 'z')
                tstr[i] += 'A'-'a';
            i++;                    /* to next character */
        }
        printf("Original string = %s\n",istr);
        printf("Transformed string = %s\n",tstr);
    }
    return 0;
}
```

下面的程序检查用户给定的字符串是否为回文。在该程序中，比较第一个字符 s[0] 和最后一个字符 s[n-1]。然后比较第二个字符 s[1] 和倒数第二个字符 s[n-2]，依此类推。此过程将持续到字符串长度的一半。如果在任何比较过程中发现字符不同，则该字符串不是回文。否则，它就是回文。

```c
#include <stdio.h>
#include <string.h>
int main()
{
    int n,i,j,chk=1;
    char s[30];
    printf("\n Enter the string:");
    scanf("%[^\n]s",s);
    n=strlen(s)-1;
    for(i=0,j=n;i<n/2;i++,j--)
        if(s[i]!=s[j])
        {
            chk=0;
            break;
        }
    if(chk==1)
        printf("String is Palindrome");
    else
        printf("String is not Palindrome");
    return 0;
}
```

这里，变量 chk 用于检查比较结果。或者，前面的程序可以按如下方式实现：

```c
#include <stdio.h>
#include <string.h>
int main()
{
    int n,i,j;
    char s[30],t[30];
    printf("\n Enter the string:");
    scanf("%[^\n]s",s);
    n=strlen(s)-1;
    for(i=0,j=n;j>=0;i++,j--)
        t[i]=s[j];
    t[i]='\0';
    if(strcmp(s,t)==0)
        printf("String is Palindrome");
    else
        printf("String is not Palindrome");
    return 0;
}
```

在上面的示例中，用户给定的字符串被反转并存储在另一个数组中。然后使用 `strcmp()` 库函数比较两个字符串，以测试它们是否相等。如果 `strcmp()` 的结果为 0，则用户输入的字符串是回文。

示例运行：

(a) Enter the string : madam

    String is Palindrome

(b) Enter the string: india

    String is not Palindrome

下面的程序删除句子中的一个单词。这里使用的逻辑是：从句子中提取每个单词到字符串 `w` 中。除最后一个单词由 NUL 字符终止外，单词之间以空格分隔。每个单词都与要删除的单词进行比较。如果匹配，则该单词不会被连接到目标字符串 `t` 中；否则，它会被连接。

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char s[50],w[20],t[50],d[20];
    int i,j;
    printf("\n Enter the sentence: \n");
    gets(s);
    printf("\n Enter the word to be deleted:");
    scanf("%s",d);
    i=0;
    while(s[i]!='\0')
    {
        j=0;
        while(1)
        {
            if(s[i]==' '||s[i]=='\0')
                break;
            w[j++]=s[i++];
        }
        w[j]='\0';
        if(strcmp(w,d)!=0)
        {
            strcat(t,w);
            strcat(t," ");
        }
        if(s[i]!='\0')
            i++;
    }
    printf("\n After deletion the sentence is as follows...\n");
    puts(t);
    return 0;
}
```

示例运行：

Enter the sentence: Ram is a good boy
Enter the word to be deleted:good
After deletion the sentence is as follows...
Ram is a boy

下面的程序将一个人的姓名作为输入，并打印名字和中间名（如果有）的首字母，以及原样打印姓氏。例如，将 Raj Kumar Santoshi 打印为 R.K. Santoshi。

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char s[50],w[20],d[20];
    int i,j;
    printf("\n Enter the full name :");
    gets(s);
    i=0;
    while(s[i]!='\0')
    {
        j=0;
        while(1)
        {
            if(s[i]==' '||s[i]=='\0')
                break;
            w[j++]=s[i++];
        }
        w[j]='\0';
        if(s[i]==' ')
        {
            printf("%c",w[0]);
            printf("%c",'.');
        }
        if(s[i]=='\0')
            printf("%s",w);
        if(s[i]!='\0')
            i++;
    }
    return 0;
}
```

这里也使用了前一个程序中应用的逻辑。提取每个单词，并打印单词的首字母 `w[0]`。如果遇到 `\0`，则该单词必定是姓氏，并按原样打印。

## 检查你的进度

- 1. 下面数组中元素‘A’的索引是多少？

  `char myArray[] = {'m', 'y', 'A', 'r', 'r', 'a', 'y'};`

  **输出 2**

- 2. 下列程序的输出将是什么？

  - (a)

    ```c
    #include <stdio.h>
    int main()
    {
        char s1[]="Oxford";
        char s2[]="University";
        s1=s2;
        printf("%s",s1);
        return 0;
    }
    ```

    输出：会出现编译错误，提示“it cannot be a modifiable 'lvalue'”或“Incompatible types in assignment”。

  - (b)

    ```c
    #include <stdio.h>
    #include <string.h>
    int main()
    {
        char p[]="string";
        char t;
        int i,j;
        for(i=0,j=strlen(p);i<j;i++)
        {
            t=p[i];
            p[i]=p[j-i];
            p[j-i]=t;
        }
        printf("%s",p);
        return 0;
    }
    ```

    输出：无输出

  - (c)

    ```c
    #include <stdio.h>
    int main()
    {
        char names[5][20]={"pascal","ada","cobol","fortran","perl"};
        int i;
        char *t;
        t=names[3];
        names[3]=names[4];
        names[4]=t;
        for(i=0;i<5;i++)
            printf("%s",names[i]);
        return 0;
    }
    ```

    输出：编译器错误：“Lvalue required”或“Incompatible types in assignment”

  - (d)

    ```c
    #include <stdio.h>
    int main()
    {
        int i;
        char a[]="\0";
        if(printf("%s\n",a))
            printf("Ok here \n");
        else
            printf("Forget it\n");
        return 0;
    }
    ```

    输出：Ok here

  - (e)

    ```c
    #include <stdio.h>
    int main()
    {
        char p[]="%d\n";
        p[1] = 'c';
        printf(p,65);
        return 0;
    }
    ```

    输出：A

  - (f)

    ```c
    #include <stdio.h>
    #include <string.h>
    int main()
    {
        char str1[] = {'s','o','m','e'};
        char str2[] = {'s','o','m','e','\0'};
        while(strcmp(str1,str2))
            printf("Strings are not equal\n");
        return 0;
    }
    ```

    输出：
    "Strings are not equal"
    "Strings are not equal"
    ...

  - (g)

    ```c
    #include <stdio.h>
    #include <ctype.h>
    int main()
    {
        char p[]="The Matrix Reloaded";
        int i=0;
        while(p[i])
        {
            if(!isupper(p[i]++))
                ++i;
        }
        printf("%d", i);
        return 0;
    }
    ```

    输出：19

## 11.4 多维数组

维数超过一维的数组称为多维数组。尽管人类不容易想象超过三维的物体，但表示多维数组对计算机来说没有问题。

### 11.4.1 二维数组的声明

二维数组可以按如下方式声明：

```c
data_type array_name[size1][size2];
```

这里，data_type 是某种数据类型的名称，例如 int。另外，size1 和 size2 分别是数组第一维和第二维的大小。

下面是一个定义 8×8 整数数组的示例，类似于棋盘。请记住，因为 C 数组

