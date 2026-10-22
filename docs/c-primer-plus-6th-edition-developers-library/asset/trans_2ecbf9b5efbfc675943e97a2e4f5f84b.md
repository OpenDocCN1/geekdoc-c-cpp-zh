

+   2.
+   	a. 显示字符 H。
+   	b. 如果系统使用 ASCII，则发出警报声。
+   	c. 将光标移动到下一行的开头。
+   	d. 退格。

3. count <essay >essayct or else count >essayct <essay

4. 没有一个是有效的。

5. 它是 `getchar()` 和 `scanf()` 返回的一个信号（一个特殊值），用于表明它们已经检测到了文件末尾。

+   6.
+   	a. 输出如下：
+   	If you qu

注意，字符 I 与字符 i 是不同的。还要注意，i 没有被打印出来，因为循环在检测到它时就退出了。

+   b. ASCII 码的输出如下：
+   	HJacrt hjacrt

第一次循环时，ch 的值是 H。ch++ 会先使用该值（打印），然后再递增（变为 I）。接着，++ch 会先递增该值（变为 J），再使用它（打印）。之后，读取下一个字符（a），并重复这个过程。这里需要注意的重要一点是，递增操作影响的是 ch 在被赋值之后的值；它们并不会以某种方式导致程序在输入队列中向前移动。

7. C 的标准 I/O 库将各种不同的文件形式映射为可以等价处理的统一流。

8. 数值输入会跳过空格和换行符，但字符输入不会。假设你有如下代码：

```
int score;
char grade;
printf("Enter the score.\n");
scanf("%s", &score);
printf("Enter the letter grade.\n");
grade = getchar();
```

## 第9章复习题答案

+   1. 形参（formal parameter）是在被调用函数中定义的变量。实参（actual argument）是函数调用中出现的值；该值被赋给形参。你可以把实参看作形参在函数被调用时被初始化的值。

+   2.
+   a. void donut(int n)
+   b. int gear(int t1, int t2)
+   c. int guess(void)
+   d. void stuff_it(double d, double *pd)

+   3.
+   a. char n_to_char(int n)
+   b. int digits(double x, int n)
+   c. double * which(double * p1, double * p2)
+   d. int random(void)

+   4.

```
int sum(int a, int b)
{
    return a + b;
}
```

+   5. 将整个函数中的 int 替换为 double：

```
double sum(double a, double b)
{
    return a + b;
}
```

+   6. 这个函数需要使用指针：

```
void alter(int * pa, int * pb)
{
    int temp;
    temp = *pa + *pb;
    *pb = *pa - *pb;
    *pa = temp;
}
```

或者

```
void alter(int * pa, int * pb)
{
    *pa += *pb;
    *pb = *pa - 2 * *pb;
}
```

7. 是的；`num` 应该声明在 `salami()` 的参数列表中，而不是花括号后面。另外，应该是 `count++`，而不是 `num++`。

8. 下面是一种解法：

```
int largest(int a, int b, int c)
{
    int max = a;
    if (b > max)
        max = b;
    if (c > max)
        max = c;
    return max;
}
```

9. 下面是一个最简程序；`showmenu()` 和 `getchoice()` 函数分别为 a 和 b 两部分提供了可行的解法。

```
#include <stdio.h>
void showmenu(void);    /* declare functions used */
int getchoice(int, int);
int main()
{
    int res;

    showmenu();
    while ((res = getchoice(1,4)) != 4)
    {
        printf("I like choice %d.\n", res);
        showmenu();
    }
    printf("Bye!\n");
    return 0;
}
void showmenu(void)
{
    printf("Please choose one of the following:\n");
    printf("1) copy files          2) move files\n");
    printf("3) remove files        4) quit\n");
    printf("Enter the number of your choice:\n");
}

int getchoice(int low, int high)
{
    int ans;
    int good;
    good = scanf("%d", &ans);
    while (good == 1 && (ans < low || ans > high))
    {
        printf("%d is not a valid choice; try again\n", ans);
        showmenu();
        scanf("%d", &ans);
    }
    if (good != 1)
    {
        printf("Non-numeric input. ");
        ans = 4;
    }
    return ans;
}
```

## 第10章复习题答案

+   1. 输出如下：
+   8 8
+   4 4
+   0 0
+   2 2

+   2. 数组 ref 有四个元素，因为初始化列表中的值的个数就是四个。

+   3. 数组名 ref 指向数组的第一个元素，即整数 8。表达式 ref + 1 指向第二个元素，即整数 4。`++ref` 这种写法不是有效的 C 表达式；`ref` 是常量，不是变量。

+   4. ptr 指向第一个元素，ptr + 2 指向第三个元素，也就是第二行的第一个元素。
+   
+   a. 12 和 16。
+   
+   b. 12 和 14（由于花括号的原因，只有 12 被放入第一行）。

+   5. ptr 指向第一行，ptr+1 指向第二行；*ptr 指向第一行中的第一个元素，*(ptr + 1) 指向第二行中的第一个元素。

无效；rootbeer 不是浮点类型。

c. rootbeer = value;

无效；rootbeer 不是浮点类型。

d. printf("%f", rootbeer);

无效；rootbeer 不是浮点类型。

e. things[4][4] = rootbeer[3];

有效。

f. things[5] = rootbeer;

无效；不能对数组进行赋值。

g. pf = value;

无效；value 不是地址。

h. pf = rootbeer;

有效。

11. int screen[800][600];

### 12.

```
a.
void process(double ar[], int n);
void processvla(int n, double ar[n]);
process(trots, 20);
processvla(20, trots);
```

```
b.
void process2(short ar2[30], int n);
void process2vla(int n, int m, short ar2[n][m]);
process2(clops, 10);
process2vla(10, 30, clops);
```

```
c.
void process3(long ar3[10][15], int n);
void process3vla(int n, int m,int k, long ar3[n][m][k]);
process3(shots, 5);
process3vla(5, 10, 15, shots);
```

### 13.

```
a.
show( (int [4]) {8,3,9,2}, 4);
```

```
b.
show2( (int [][3]){{8,3,9}, {5,4,1}}, 2);
```

## 第11章复习题答案

+   1. 如果希望结果是一个字符串，初始化中应该包含一个 `'\0'`。当然，另一种语法会自动添加空字符：
+   
+   ```
+   char name[] = "Fess";
+   ```

+   2.
+   
+   ```
+   See you at the snack bar.
+   ee you at the snack bar.
+   See you
+   e you
+   ```

+   3.
+   
+   ```
+   y
   
+   my
   
+   mmy
   
+   ummy
   
+   Yummy
+   ```

+   4. ```I read part of it all the way through.```

+   5.
+     a. ```Ho Ho Ho!!OH oH oH```
+     b. 指向字符的指针（即 `char *`）。
+     c. 初始 H 的地址。
+     d. `*--pc` 表示将指针减 1，并使用该位置处的值。`--*pc` 表示取出 `pc` 指向的值，并将该值减 1（例如，H 变为 G）。
+     e. ```Ho Ho Ho!!OH oH o```

# 注

在 `!` 和 `!` 之间有一个空字符，但通常它不会产生任何打印效果。

+   f. `while(*pc)` 检查 `pc` 是否不指向空字符（即字符串的末尾）。该表达式使用的是指针所指位置处的值。
+   
+   ```
+   while(pc - str) checks to see that pc does not point to the same location
+   that str does (the beginning of the string). The expression uses the values of the
+   pointers themselves.
+   ```

```
*st = '\0';
else
    while (getchar() != '\n')
        continue;
}
return ret_val;
}
```

10. 下面是一种解法：

```
int strlen(const char * s)
{
    int ct = 0;

    while (*s++)    // or while (*s++ != '\0')
        ct++;

    return(ct);
}
```

11. 下面是一种解法：

```
#include <stdio.h>    // for fgets(), getchar()
#include <string.h>    // for strchr();
char * s_gets(char * st, int n)
{
    char * ret_val;
    char * find;

    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n');    // look for newline
        if (find)                   // if the address is not NULL,
            *find = '\0';          // place a null character there
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```

12. 下面是一种解法：

```
#include <stdio.h>    /* for NULL definition          */
char * strblk(char * string)
{
    while (*string != ' ' && *string != '\0')
```

