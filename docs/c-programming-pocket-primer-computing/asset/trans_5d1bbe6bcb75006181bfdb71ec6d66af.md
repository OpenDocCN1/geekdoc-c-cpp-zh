
清单 3.12 显示了 MaxAndMinValue.c 的内容，该内容展示了如何在 C 中使用简单的循环（带条件逻辑）来查找数组中的最大值和最小值。

### LISTING 3.12: MaxAndMinValue.c

```
    #include <stdio.h>

    int main()
    {
        int numbers[] = {15, 3, 99, -4, 25, 8};
        int min=numbers[0], max=numbers[0];
        int count=sizeof(numbers)/sizeof(numbers[0]);

        for(int i=0; i<count; i++)
        {
            if(min > numbers[i])
            {
                min = numbers[i];
            }

            if(max < numbers[i])
            {
                max = numbers[i];
            }
        }

        printf("Array: ");
        for(int i=0; i<count; i++)
        {
            printf("%d ", numbers[i]);
        }
        printf("\n");

        printf("Max:  %d\n",max);
        printf("Min:  %d\n",min);
        return 0;
    }
```

清单 3.12 包含一个 main() 函数，该函数使用 6 个整数初始化 numbers 数组，随后是整数变量 min 和 max，两者均初始化为 numbers[0] 的值。

第一个循环包含条件逻辑，如果当前元素小于 `min` 则更新 `min` 的值，如果当前元素大于 `max` 则更新 `max` 的值。第二个循环显示 `numbers` 数组中元素的数值，然后显示 `min` 和 `max` 的值。启动清单 3.12 中的 C 程序的输出如下：

```
Array: 15 3 99 -4 25 8

Max:  99

Min:  -4
```

## 从数组中删除元素

清单 3.13 显示了 `DeleteArrayElement.c` 的内容，展示了如何在 C 程序中使用 for 循环从数字数组中删除一个元素。

### LISTING 3.13: DeleteArrayElement.c

```
#include <stdio.h>

int main()
{
    int pos = 4;
    int numbers[] = {15, 3, 99, -4, 25, 8};
    int count=sizeof(numbers)/sizeof(numbers[0]);

printf("Initial: ");
for(int i=0; i<count; i++)
{
    printf("%d ",numbers[i]);
}
printf("\n");

printf("Removed: %d\n",numbers[pos]);
for(int i=pos; i<count-1; i++)
{
    numbers[i] = numbers[i+1];
}
numbers[count-1] = 0;

printf("Updated: ");
for(int i=0; i<count; i++)
{
    printf("%d ",numbers[i]);
}
printf("\n");

return 0;
}
```

清单 3.13 包含一个 main() 函数，该函数使用 6 个整数初始化 numbers 数组，随后是整数变量 pos，指定将要删除的 numbers 数组的索引位置。

第一个循环显示 numbers 数组的内容，随后第二个循环执行删除操作。该循环本质上将位置 pos 右侧的元素“左移”一个位置。例如，由于 pos[4] 将被删除，我们可以用 pos[5] 替换其值。接下来，用 pos[6] 的值替换 pos[5]。重复此过程，直到到达 numbers 数组中最后一个（最右侧）元素。

最后的循环显示 numbers 数组的更新内容。启动清单 3.13 中的 C 程序的输出如下：

```
Initial: 15 3 99 -4 25 8
Removed: 25
Updated: 15 3 99 25 8 0
```

## 字符串和 for 循环

清单 3.14 显示了 ForLoopStr.c 的内容，展示了如何在 C 程序中使用简单的 for 循环显示文本字符串中的字符。此代码示例包含 C 中指针使用的预览，该内容要到第 5 章才会详细讨论。如有需要，请在阅读完第 5 章的材料后再跳过此代码示例。

### LISTING 3.14: ForLoopStr.c

```
#include <stdio.h>
#include <string.h>

int main()
{
    char *str = "hello";
    char *p = str;
    int len = strlen(str);

    printf("First Loop\n");
    printf("---------\n");
    for(int i=0; i<len; i++)
    {
        printf("i : %c\n", str[i]);
    }

    printf("\nSecond Loop\n");
printf("---------\n");
for(int i=0; i<len; i++)
{
    printf("i : %s\n", p);
    ++p;
}

return 0;
}
```

清单 3.14 包含一个 main() 函数，将字符指针 str 初始化为硬编码字符串，然后将字符指针 p 初始化为 str 的地址。第一个循环使用语法 (char)str[i] 显示 str 中的每个字符。

第二个循环也显示 substrings of str，这次使用语法 (char *)p。指针 p 从 str 的地址开始，在 for 循环的每次迭代中，指针 p 的地址通过代码片段 ++p 增加（也可以与之前的代码片段合并）。随着指针 p 在 str 的每个位置推进，输出为更短的子字符串。清单 3.14 的输出如下：

### 第一个循环

```
---------
i : h
i : e
i : l
i : l
i : o
```

### 第二个循环

```
---------
i : hello
i : ello
i : llo
i : lo
```

## 统计一行文本中的单词数

清单 3.15 显示了 CountWords.c 的内容，说明了如何统计一行文本中的单词数（单词由空格或制表符分隔）。

### LISTING 3.15: CountWords.c

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int main()
{
    char str1[] = " This is a  String";
    int i=0, wCount=0;

    int len1 = strlen(str1);

    // skip over leading whitespace
    for(i=0; i<len1; i++)
    {
        if((str1[i]!=' ')&&(str1[i]!='\t'))
        {
            break;
        }
    }

    for(; i<len1; i++)
    {
        // found a whitespace => found a word
        if((str1[i]==' ')||(str1[i]=='\t'))
        {
wCount++;
}

// handle the case where there are
// multiple whitespaces between words
}

wCount++;

printf("Line of Text:  %s\n",str1);
printf("Word Count:  %d\n",wCount);

return 0;
}
```

清单 3.15 包含一个 main() 函数，将字符字符串 str1 初始化为硬编码字符串，然后初始化一些标量值。第一个循环跳过任何初始空白字符（可以是简单的空格或制表符）。

第二个循环在 str1 中遇到空白字符时每次递增变量 wCount。其基本假设是空白字符的出现意味着存在新单词。然而，如果单词之间存在多个空白字符，则需要修改此代码以跳过这些“额外”的空白字符，其方式与跳过初始空白字符类似（留作练习）。启动 CountWords 的输出如下：

```
Line of Text:  This is a  String
Word Count:  6
```

## 使用嵌套 for 循环

清单 3.16 显示了 `NestedForLoop.c` 的内容，展示了如何在 C 程序中使用嵌套 for 循环。

### LISTING 3.16: NestedForLoop.c

```
#include <stdio.h>

int main()
{
   int max=5;

   for(int i=0; i<max; i++)
   {
      printf("(i,j): ");
      for(int j=0; j<max; j++)
      {
         printf("%d %d ", i, j);
      }
      printf("\n");
   }

   return 0;
}
```

清单 3.16 包含一个 `main()` 函数，其中嵌套循环遍历 0 到 4 之间的数字，并使用 `printf()` 函数显示当前 (i,j) 位置（其中 i 是外层循环的索引，j 是内层循环的索引）。清单 3.16 的输出如下：

```
(i,j): 0,0 0,1 0,2 0,3 0,4
(i,j): 1,0 1,1 1,2 1,3 1,4
(i,j): 2,0 2,1 2,2 2,3 2,4
(i,j): 3,0 3,1 3,2 3,3 3,4
(i,j): 4,0 4,1 4,2 4,3 4,4
```

下一节将向您展示如何在 C 程序中使用 while 循环。

## 使用 while 循环

清单 3.17 显示了 WhileLoop.c 的内容，展示了如何使用 while 循环在 C 中打印一列整数。

### LISTING 3.17: WhileLoop.c

```
#include <stdio.h>

int main()
{
   int i=0, max=5;
   while(i<=max)
   {
      printf("i : %d\n", i);
      ++i;
   }

   return 0;
}
```

清单 3.17 包含一个 main() 函数，将变量 i 和 max 分别初始化为值 0 和 5。下一段代码是一个 while 循环，只要 i 的值小于或等于 5 就执行。在循环体内部，printf() 函数显示 i 的当前值，之后 i 的值递增。启动清单 3.17 的输出如下：

```
i : 0
i : 1
i : 2
i : 3
i : 4
```
