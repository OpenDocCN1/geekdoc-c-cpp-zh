
## 输出 2

输入字符串一：C programming
输入字符串二：C Programming
字符串 "C programming" 和 "C Programming" 不相同。

## 输出 3

输入字符串一：C Programming
输入字符串二：C Programming
字符串 "C Programming " 和 "C Programming" 不相同。

在程序 3 中可以看出，函数 `strcmp` 接收两个字符指针作为输入。第一个指针指向第一个字符串的起始字符，而第二个指针指向第二个字符串的起始字符。它返回一个整数值，该值可以是零、正数或负数。

函数 `strcmp` 首先比较两个字符串中索引为 0 处存储的字符。如果两个字符串在索引 0 处的字符不相同，则函数返回字符串二中字符的 ASCII 值与字符串一中字符的 ASCII 值之差。如果两个字符串在索引 0 处的字符相同，我们将索引值加 1，并重复比较过程，直到发现不匹配为止。如果返回的差值为正数，则说明字符串一大于字符串二；如果返回的差值为负数，则说明字符串一小於字符串二。如果没有 ASCII 值不匹配的情况，则返回零，并且这两个字符串被认为是相等的。在程序 3 中，ASCII 值的字符串是大小写敏感的；因此，字符 *V* 不等于 *v*。

图 4 展示了这三种输出是如何产生的：

![](img/5d422ba7108ffdf64376be51eaf0c459_223_0.png)

在图 4 的第一种情况中可以看到，函数未发现不匹配。这导致函数返回值为零，表明字符串一和字符串二相同。在第二种情况下，函数在第三个字符处发现了不匹配。字符串 *s_str1* 中索引 *Z* 处存储的字符是小写字母 *p*，而在字符串 *s_str2* 中，它是大写字母 *P*。因此，函数返回小写字母 *p*（112）和大写字母 *P*（80）的 ASCII 值之差。由于结果值大于零，这表明字符串一在字典中排在字符串二之后。类似地，在第三种情况下，不匹配发生在第六个字符处。函数返回一个负值，表明字符串一在字典中排在字符串二之前。下一节将讨论如何将字符串二附加到字符串一的末尾。

## 附加两个字符串

许多应用程序都需要将一个字符串附加到另一个字符串的末尾。此操作称为字符串连接。执行第二个字符串对第一个字符串的连接操作时，会修改第一个字符串，而第二个字符串保持不变。程序 4 演示了如何附加两个字符串：

## 程序 4

```c
/* Program to append strings */
#include<stdio.h>
#define MAX 25

/* Function to append two strings */
char *strcat(char *s_str1, char *s_str2)
{
	int i_ctr1,i_ctr2, i_len1,i_len2;

	/* Find length of both strings */
	i_len1 = strlen(s_str1);
	i_len2 = strlen(s_str2);

	/* Check that length of source is big enough to hold both strings */
	if (MAX >= i_len1 + i_len2 + 2)
	{
		s_str1[i_len1] = ',';
		/* Transfer characters from string 2 to 1 */
		for ( i_ctr1 = i_len1+1, i_ctr2=0; i_ctr2 < i_len2; i_ctr1++,
			i_ctr2++)
			s_str1[i_ctr1] = s_str2[i_ctr2];
		s_str1[i_ctr1]='\0';
		return s_str1;
	}
	else
		return NULL;
}
/* End of Function */

/* Beginning of main function */
main()
{
	/* Declare character array */
	char s_str1[MAX], s_str2[MAX];
	char *p_result, c_temp;
	int i_len;

	/* Read strings */
	printf("\nEnter a string one : ");
	scanf("%[^\n]",&s_str1);
	c_temp=getchar();

        printf("\nEnter a string two : ");
        scanf("%[^\n]", &s_str2);

        p_result = strcat(s_str1, s_str2);
        if (p_result == NULL)
        {
            printf("\nStrings cannot be concatenated ");
        }
        else
        {
            printf("\n\nThe modified strings are \"%s\" and \"%s\".", s_str1, s_str2);
        }
        return;
    } /* End of function main */
```

**输出 1：**
输入字符串一：Proud to
输入字符串二：be Indian
修改后的字符串为 "Proud to be Indian" 和 "be Indian"。

**输出 2：**
输入字符串一：Please see that
输入字符串二：you do not fall
字符串无法连接

在程序 4 中可以看出，函数 `strcat` 接收两个字符指针作为输入，并返回第一个字符串的字符指针。图 5 展示了程序 4 输出 1 中执行连接操作的内存表示：

![](img/5d422ba7108ffdf64376be51eaf0c459_225_0.png)

在图 5 中可以看到，连接操作完成后，s_str1 被修改，而 s_str2 保持不变。下一节将讨论如何反转字符串的内容。

## 反转字符串

字符串反转操作交换第一个索引元素的内容与最后一个索引元素的内容，第二个索引元素的内容与倒数第二个索引元素的内容，依此类推，直到到达中间索引为止。程序 5 演示了如何反转字符串：

## 程序 5

```c
/* Program to reverse a string */
#include<stdio.h>
#include<string.h>

/* Function to reverse a string */
char *strrev(char *s_str)
{
/* Declare front counter, back counter and length */
int i_fctr, i_bctr, i_len;
char c_temp;

i_len= strlen(s_str);

/* Reverse the string */
for ( i_fctr=0, i_bctr= i_len-1;  i_fctr< i_len/2; i_fctr++,  i_bctr--)
{
c_temp= s_str[i_fctr];
s_str[i_fctr]= s_str[i_bctr];
s_str[i_bctr]= c_temp;
}
s_str[i_len]='\0';
return s_str;
}
/* End of function */

/* Beginning of main function */
main()
{
/* Declare character array */
char s_str[25];

/* Read data in array */
printf("\nEnter a string : ");
scanf("%[^\n]" , &s_str );

strrev(s_str);

/* Print reversed string */
printf("\nThe reversed string: %s\n",s_str);
return;
}
/* End of function main */
```

**输出：**

输入字符串：Good Morning
反转后的字符串：gniMrooM dooG

在程序 5 中可以看出，函数 `strrev` 接收一个字符指针作为输入，并返回相同字符串的字符指针。图 6 展示了操作执行前后字符串的内存表示：

![](img/5d422ba7108ffdf64376be51eaf0c459_227_0.png)

**图 6：反转操作示例**

在图 6 中可以看到，除了 NULL 字符外，所有索引的内容都发生了变化。如果字符串长度为奇数，则中间索引的内容也将保持不变。下一节将讨论如何将给定的字符串转换为小写字符串。

## 将字符串转换为小写

在编辑文本时，大小写转换是对字符串进行的一种常见操作。我们可以将大写字符串转换为小写字符串，反之亦然。也有可能将字符串转换为标题大小写（规范大小写）。我们利用 ASCII 值来执行大小写转换操作。程序 6 演示了如何将任意大小写的给定字符串转换为小写字符串：

## 程序 6

```c
/* Program to illustrate case conversion of string */

#include<stdio.h>

/*  Function to convert case */
char   *strlower(char *s_str)
{

    int i_ctr,i_len;
    i_len = strlen(s_str);

    for ( i_ctr=0; i_ctr < i_len; i_ctr++)
    {
        if ( s_str[i_ctr] >= 'A' && s_str[i_ctr] <= 'Z')
            s_str[i_ctr] = s_str[i_ctr] + 32;
    }
    s_str[i_ctr]='\0';
    return s_str;
}
/*  End of Function */

/*  Beginning of main function */
main()
{
    /*  Declare character array */
    char s_str[25];

    /*  Read data in array */
    printf("\nEnter a string : ");
    scanf("%[^\n]",&s_str);

    strlower(s_str);
    /* Print string */
    printf("\nThe lower case string: %s\n",s_str);
    return;
}
/* End of function main */
```

**输出：**

输入字符串：PROUD TO BE INDIAN
小写字符串：proud to be indian

在程序 6 中可以看出，函数 `strlower` 接收一个字符指针作为输入，并返回相同字符串的字符指针。图 7 展示了操作执行前后字符串的内存表示：

![](img/5d422ba7108ffdf64376be51eaf0c459_228_0.png)

在图 7 中可以看到，除了 NULL 字符外，所有字符都变成了小写字符。请注意，只有当字符是大写字母时，该字符的 ASCII 值才会被修改。在所有其他情况下，字符串内的字符不会被修改。

前面讨论的字符数组都是一维的。在这样的数组中只能存储一个名称。实际场景需要我们同时存储许多名称。例如，用于生成学生成绩单的应用程序可能需要存储班级中所有学生的姓名。要实现此功能，我们需要多维字符数组。下一节将讨论多维字符数组的概念。

## 10.6 字符串数组

字符串数组指的是多维字符数组。我们已经在第 9 章中了解到，多维数组使用两个索引。定义字符串数组的语法如下：

```c
char s_student_name[3][15];
```

上述定义有助于存储三个学生的姓名，每个姓名最大长度为 14 个字符。多维字符数组也可以在编译时初始化。在运行时初始化多维字符数组的语法如下：

```c
char s_student_name[3][15]={ "Jain Harshit","Aroklar Vidita","Jain Navya"};
```

