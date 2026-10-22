

+   4. a. scanf("%d", &x) == 1
+   b. x != 5
+   c. x >= 20

5. 第 4 行：应为 list[10]。
第 6 行：逗号应为分号。
第 6 行：i 的范围应为 0 到 9，而不是 1 到 10。
第 9 行：逗号应为分号。
第 9 行：>= 应为 <=。否则，当 i = 1 时，循环会运行相当长一段时间。
第 10 行：在第 9 行和第 10 行之间应再有一个闭合大括号。一个大括号关闭复合语句，一个大括号关闭程序。中间应有一行 return 0;。

下面是一个修正后的版本：

```
#include <stdio.h>
int main(void)
{
	int i, j, list[10]; /* line 3 */
	for (i = 0; i < 10; i++) /* line 6 */
	{
		list[i] = 2*i + 3; /* line 7 */
		for (j = 1; j <= i; j++) /* line 8 */
			printf("%d", list[j]); /* line 9 */
		printf("\n"); /* line 10 */
	}
	return 0;
}
```

6. 这里有一种方法：

```
#include <stdio.h>
int main(void)
{
	int col, row;
	for (row = 1; row <= 4; row++)
	{
		for (col = 1; col <= 8; col++)
		{
			printf("$");
		}
		printf("\n");
	}
}
```

```
return 0;
}
```

+   7.
+     a. 它会产生以下输出：
+       Hi! Hi! Hi! Bye! Bye! Bye! Bye! Bye!
+     b. 它会产生以下输出：
+       ACGM

因为代码将 int 值加到 char 值上，编译器可能会警告可能丢失有效数字。

+   8.
+     a. 它会产生以下输出：
+       Go west, youn
+     b. 它会产生以下输出：
+       Hp!xftu-!zpvo
+     c. 它会产生以下输出：
+       Go west, young
+     d. 它会产生以下输出：
+       $o west, youn

9. 你应该得到以下输出：

```
31|32|33|30|31|32|33|
***
1
5
9
13

***
2 6
4 8
8 10

***
======
=====
====
===
==
```

+   10.
+     a. mint
+     b. 10 个元素

+   c. 类型为 double 的值

+   d. 第 ii 行是正确的；mint[2] 是一个类型为 double 的值，&mint[2] 是它的位置。

## 11.

因为第一个元素的索引为 0，所以循环范围应为 0 到 SIZE - 1，而不是 1 到 SIZE。这样修改后，第一个元素会被赋值为 0 而不是 2。因此应这样重写循环：

```
for (index = 0; index < SIZE; index++)
    by_twos[index] = 2 * (index + 1);
```

同样，第二循环的限制也应更改。此外，应使用数组名配合数组索引：

```
for( index = 0; index < SIZE; index++)
    printf("%d ", by_twos[index]);
```

糟糕的循环限制的一个危险之处在于程序可能能工作；然而，由于它将数据放置在不应该放置的位置，它可能在未来某个时间无法工作，形成一种编程定时炸弹。

## 12.

它应将返回类型声明为 long，并且应有一个返回语句返回 long 值。

## 13.

将 num 类型转换为 long 可确保计算作为 long 计算进行，而不是作为 int 计算。在使用 16 位 int 的系统上，两个 int 的乘法会将结果截断为 int 后再返回，可能丢失数据。

```
long square(int num)
{
    return ((long) num) * num;
}
```

## 14.

以下是输出：

```
1: Hi!
k = 1
k is 1 in the loop
Now k is 3
k = 3
k is 3 in the loop
Now k is 5
k = 5
k is 5 in the loop
Now k is 7
k = 7
```

## 第 7 章复习题答案

+   1. 真：b。

+   2. a. number >= 90 && number < 100
+   b. ch != 'q' && ch != 'k'
+   c. (number >= 1 && number <= 9) && number != 5
+   d. !(number >= 1 && number <= 9) 是一个选择，但 number < 1 || number > 9 更易于理解

3. 第 5 行：应为 scanf("%d %d", &weight, &height);。不要忘记 scanf() 中的那些 &。此外，此行之前应有一行提示输入。

第 9 行：意思是 (height < 72 && height > 64)。然而，表达式的第一部分是不必要的，因为 height 必须小于 72 才能在首先到达 else if 时成立。因此，简单的 (height > 64) 就足够了。但第 6 行已经保证了 height > 64，所以根本不需要测试，if else 应该只是 else。

第 11 行：条件是冗余的；第二个子表达式（weight 不小于或等于 300）与第一个含义相同。简单的 (weight > 300) 就足够了。但还有更大的问题。第 11 行被附加到了错误的 if！显然，这个 else 是要与第 6 行一起使用的。根据最近的 if 规则，它将被与第 9 行的 if 关联。因此，当 weight 小于 100 且 height 在 64 或以下时，会到达第 11 行。这使得在到达此语句时 weight 不可能超过 300。

第 7 行至第 10 行：应用大括号括起来。然后第 11 行将成为第 6 行的替代，而不是第 9 行的替代。或者，如果第 9 行的 if else 被替换为简单的 else，则不需要大括号。

第 13 行：简化为 if (height > 48)。实际上，你可以完全省略这一行，因为第 12 行已经做了这个测试。

第 15 行：这个 else 与最后一个 if 关联，即第 13 行的那个。用大括号括起第 13 行和第 14 行，强制此 else 与第 11 行的 if 关联。或者，如建议的那样，简单地删除第 13 行。

下面是一个修正后的版本：

```
#include <stdio.h>
int main(void)
{
    int weight, height;  /* weight in lbs, height in inches */
    printf("Enter your weight in pounds and ");
```

```
printf("your height in inches.\n");
scanf("%d %d", &weight, &height);
if (weight < 100 && height > 64)
    if (height >= 72)
        printf("You are very tall for your weight.\n");
    else
        printf("You are tall for your weight.\n");
else if (weight > 300 && height < 48)
    printf(" You are quite short for your weight.\n");
else
    printf("Your weight is ideal.\n");

return 0;
}
```

## 4.

+   a. 1。断言为真，数值上为 1。
+   b. 0。3 不小于 2。
+   c. 1。如果第一个表达式为假，第二个为真，反之亦然；只需要一个真表达式。
+   d. 6，因为 6 > 2 的值为 1。
+   e. 10，因为测试条件为真。
+   f. 0。如果 x > y 为真，表达式的值为 y > x，在这种情况下为假，或 0。如果 x > y 为假，表达式的值为 x > y，在这种情况下为假。

## 5.

程序打印以下内容：

```
*# $ * # $ * # $ * # $ * # $ * # $ * # $ * # $ * # $ * # $ * # $ * # $ * # $
```

尽管缩进暗示了这一点，但 # 在每次循环中都会被打印，因为它不是复合语句的一部分。

## 6.

程序打印以下内容：

```
fat hat cat Oh no!
hat cat Oh no!
cat Oh no!
```

## 7.

第 5 行至第 7 行的注释应以 */ 终止，否则你可以用 // 替换 /*。表达式 'a' <= ch >= 'z' 应替换为：

```
ch >= 'a' && ch <= 'z'
```

或者，更简单、更可移植的是，你可以包含 ctype.h 并使用 islower()。顺便说一下，'a' <= ch >= 'z' 在语法上是有效的 C；它只是没有正确的含义。因为关系运算符从左到右关联，表达式被解释为 ('a' <= ch) >= 'z'。括号内的表达式具有值 1 或 0（真或假），并且此值被检查是否大于或等于 'z' 的数值代码。0 也不满足该测试，因此整个表达式始终求值为 0（假）。在第二个测试表达式中，|| 应为 &&。此外，虽然 !(ch < 'A') 在含义上既有效又正确，但 ch >= 'A' 更简单。'z' 后应跟两个闭合括号，而不是一个。同样，更简单地使用 isupper()。oc++; 语句之前应有 else。否则，它会在每个字符时递增。printf() 调用中的控制表达式应用双引号括起来。

下面是一个修正后的版本：

```
#include <stdio.h>
#include <ctype.h>
int main(void)
{
    char ch;
    int lc = 0;    /* lowercase char count */
    int uc = 0;    /* uppercase char count */
    int oc = 0;    /* other char count */

    while ((ch = getchar()) != '#')
    {
        if (islower(ch))
            lc++;
        else if (isupper(ch))
            uc++;
        else
            oc++;
    }
    printf("%d lowercase, %d uppercase, %d other", lc, uc, oc);
    return 0;
}
```

8. 不幸的是，它会无限打印同一行：

```
You are 65. Here is your gold watch.
```

问题在于这一行

```
if (age = 65)
```

将 age 设置为 65，每次循环周期都测试为真。

9. 使用给定输入的运行结果如下：

```
q
Step 1
Step 2
```
