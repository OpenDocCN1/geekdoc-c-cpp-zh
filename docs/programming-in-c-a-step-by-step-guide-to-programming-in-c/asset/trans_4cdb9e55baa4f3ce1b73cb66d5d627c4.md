

另一个 **for** 与 **while** 循环的对比是，虽然 **for** 循环中的测试表达式（expr2）是可选的，但在 **while** 循环中它是必需的。如果省略 **while** 循环的控制表达式，编译器会抱怨语法错误。（要编写一个有意的无限 **while** 循环，你必须提供一个始终非零的表达式。最明显的就是 while(1)。）

如果可以把 **for** 循环改写成 **while** 循环，反之亦然，为什么两者都存在？应该选择哪一个？一般来说，当你选择 for 循环时，其三个表达式都应操作同一个变量或数据结构，使用初始化、测试、递增模式。如果它们不操作同一个变量或不遵循该模式，强行塞进 **for** 循环毫无好处，而 **while** 循环可能更清晰。（之所以一个循环比另一个更清晰，仅仅是因为，当你看到 **for** 循环时，你期望看到对单个变量的惯用初始化/测试/递增，如果你看到的 **for** 循环最终不符合该模式，你会被短暂误导。）

### 程序 4.8：求一个数的阶乘的程序

```c
void main()
{
int M,N;
long int F=1;
clrscr();
printf("enter the number\n");
scanf("%d",&N);
if(N<=0)
F=1;
else
{
for(M=1;M<=N;M++)
F*=M;
}
printf("the factorial of the number is %ld",F); getch();
}
```

### 自测题

- 12. for 循环是出口控制循环。 (True/False)
- 13. for 循环的“控制变量”不一定是整数。 (True/False)

### 4.8.1 for 循环的嵌套

for 循环的嵌套，即一个 for 语句嵌套在另一个 for 语句中，在 C 语言中是允许的。例如，两个循环可以嵌套如下：........

```c
........
for(i=1;i<10;i++)
{
.......
.......
for(j=1;j<5;j++)
{
.......
.....
}
.......
.......
}
```

## 4.9 *break* 语句和 continue 语句

*break* 语句的目的是跳出循环（**while, do while, or for loop**）或 switch 语句。当在循环内遇到 **break** 语句时，循环会立即退出，程序继续执行循环之后的下一条语句。当循环嵌套时，**break** 只会退出包含它的那个循环。也就是说，**break** 只会退出单个循环。

**语法**：`break;`

### 程序 4.9：说明 *break* 语句用法的程序。

```c
void main()
{
    int x;
    for(x=1; x<=10; x++)
    {
        if(x==5)
            break; /* break loop only if x == 5 */
        printf("%d", x);
    }
    printf("\nBroke out of loop");
}
```

```c
printf("at x =%d");
}
```

上述程序显示从 1 到 4 的数字，并在遇到 5 时打印消息“ Broke out of loop when 5 is encountered。”

### *continue* 语句

**continue** 语句用于跳过循环体的一部分来继续循环的下一轮迭代（for、**do/while** 或 **while** 循环）。*continue* 语句不适用于 **switch**，像 *break* 语句一样。与导致循环终止的 **break** 不同，**continue** 会导致循环在跳过中间的任何语句后继续下一轮迭代。

**语法：** `continue;`

### 程序 4.10：说明 *continue* 语句用法的程序。

```c
void main(){
int x;
for (x=1; x<=10; x++)
{
if(x == 5)
continue; /* skip remaining code in loop
only if x == 5 */
printf("%d\n",x);
}
printf("\nUsed continue to skip");
}
```

上述程序显示从 1 到 10 的数字，除了数字 5。

### 程序 4.11：交互输入求和整数的程序

```c
#include <stdio.h>
int main(void)
{
long num;
long sum = 0L; /* initialize sum to zero */
int status;

printf("Please enter an integer to be summed."); printf("Enter q to quit.\n");
status = scanf("%ld", &num);
while (status == 1)
{
sum = sum + num;
printf("Please enter next integer to be summed."); printf("Enter q to quit.\n");
status = scanf("%ld", &num);
}
printf("Those integers sum to %ld.\n", sum); return 0;
}
```

## 4.10 总结

在 C 语言中，默认情况下语句按顺序执行，一个接一个。我们可以通过使用 *控制流构造* 来修改该顺序。C 语言具有决策能力并支持以下称为 *控制* 或 *决策* 语句的语句：**goto, if, switch**。goto 语句用于无条件地从程序中的一个点分支到另一个点。修改程序控制流的最简单方法是用 if 语句。**switch** 语句在满足要求时作为编写长 **if** 语句的简单方法。

C 中最基本的 *循环* 是 **while** 循环。**while** 循环有一个控制表达式，只要该表达式为真就执行。**do..while loop** 用于需要在执行测试之前先执行循环体的情况。**for** 循环用于重复执行一组语句固定次数。它是入口控制循环。**break** 语句用于退出任何循环。与导致循环终止的 **break** 不同，**continue** 会导致循环在跳过中间的任何语句后继续下一轮迭代。

## 4.11 终结性问题

1. 考虑以下程序段：

```c
x = 1;
y = 1;

if(n>0)
    x=x+1;
    y=y-1;
    printf("%d %d",x,y);
```

如果 n 假设为 (a) 1 和 (b) 0，x 和 y 的值会是什么。

2. 重写以下内容而不使用复合关系：

```c
if (grade<=59 && grade>=50)
    second = second +1;
```

3. 编写一个程序来检查输入的数字是奇数还是偶数。

4. 写出以下 C 程序将生成的输出：

```c
void main()
{
int i=0, x=0;
while (i<20)
{
if (i%5 == 0)
{
x+=i;
printf("%d\t",i);
}
i++;
}
printf("\nx=%d"; x);
}
```

5. 写出以下 C 程序将生成的输出：

```c
void main()
{
    int i=0,x=0;
    do
    {
        if(i%5 == 0)
        {
            x++;
            printf("%d\t",x);
        }
        ++i;
    } while (i<20);
    printf("\nx=%d",x);
}
```

## 4.12 自测题答案

- 1 labe
- .1
- 2 true
- . false
- 4. if
- 5. true
- 6. value
- 7. false
- 8. while
- 9. true
- 10. do...while
- 11. false
- 12. false
- 13. true

## 4.13 终结性问题答案

- 1. (a) x = 2, y = 0
  - (b) x = 1, y = 0

2.

```c
if (grade <= 59)
    if (grade >= 50)
        second = second + 1;
```

3.

```c
void main()
{
    int no;
    printf("enter a number\n");
    scanf("%d", &no);
    if (no % 2 == 0)
        printf("even number\n");
    else
        printf("odd number\n");
}
```

- 4. 0 5 10 15 x = 30
- 5. 1 2 3 4 x = 4

## 4.14 练习

- 1. 举例说明不同类型的 **if** 语句。
- 2. 举例说明 **switch** 语句的语法。
- 3. 编写一个程序使用 **switch** 语句检查给定的数字是奇数还是偶数。
- 4. 编写一个程序使用 **if-else** 语句找出 3 个数字中的最小值。
- 5. 编写一个程序求二次方程的根。
- 6. 比较以下语句
  - a) *while* 和 *do...while*
  - b) *break* 和 *continue*
- 7. 编写一个程序使用 **while** 循环计算给定数字各位数字之和。
- 8. 编写一个程序读取一个正整数并确定并打印其二进制等价物，使用 **do...while** 循环。
- 9. 序列中的数字
  1 1 2 3 5 8 13..........
  称为斐波那契数。编写一个程序使用 do...while 循环计算并打印前 n 个斐波那契数。
- 10. 找出以下各段中的错误，如有的话。假设所有变量都已声明并赋值。
  (a)
  ```c
  while (count !=10);
  {
  count = 1;
  sum = sum + x;
  count = count + 1;
  }
  ```
  (b)
  ```c
  do;
  total = total + value;
  scanf("%f", &value);
  while (value !=999);
  ```
- 11. 编写程序使用 for 循环打印以下输出。
  (a) 1
  (b) 1
      2 2 2 2
      3 3 3 3 3 3
      4 4 4 4 4 4 4 4
- 12. 编写一个程序读取 100 个人的年龄并统计年龄在 50 到 60 岁之间的人数。使用 for 和 continue 语句。
- 13. 编写一个程序使用嵌套 for 循环打印乘法表。

