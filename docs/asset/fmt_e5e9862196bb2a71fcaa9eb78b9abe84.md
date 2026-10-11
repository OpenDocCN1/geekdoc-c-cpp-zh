
| | B | B | B | B | B | B | B | B | B | B | \0 |

| | E | E | E | E | \0 |

| | P | P | P | P | P | P | P | P | P | P | P | P | P | \0 |

如果最大字符串长度为80个字符，在静态数组中存储这些字符串将需要 320 字节内存。使用动态数组，字符串需要 48 字节，缓冲区需要 80 字节，指针数组需要 16 字节，总共 144 字节。

### 10.5.2 将字符串作为动态数组传递给函数

在动态存储中的字符串可以通过动态指针传递给函数，并可以在函数中打印。以下代码展示了此类字符串的输出。

```
#include <stdio.h>
void funcoutput(char *);
int main() {
	char str[20] = "COMPUTATION";
	char *chrptr;
	chrptr = (char *) malloc(strlen(str) + 1);
	strcpy(chrptr, str);
	funcoutput(chrptr);
	return 0;
}
```

```
void funcout(char *strptr)
{
    printf("String: %s\n", strptr);
    return;
}
```

输出如下：

String: COMPUTATION

注意，动态存储是使用函数 `malloc()` 分配的。字符串从 `strname` 复制到动态指针 `chrptr` 指向的动态存储中。动态字符串指针被传递给函数，字符串在函数内部打印。

当字符串作为动态数组存储时，它们的指针存储在静态数组中。字符串指针数组可以传递给函数，并在函数内部对字符串进行操作。以下代码展示了动态字符的输入和输出。

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

void funinput(char *strptr[ ], int NUMSTR);
void funcout(char *strptr[ ], int NUMSTR);

int main()
{
    const int NUMSTR = 5;
    int i;
    char *strptr[NUMSTR];
    funinput(strptr, NUMSTR);
    funcout(strptr, NUMSTR);
    return 0;
}

void funinput(char *strptr[ ], int NUMSTR)
{
    const int STLNG = 80;
    int i;
    char strname[STLNG];
```

```
for(i = 0; i<NUMSTR; i++)

{

    gets(strname);

    strptr[i] = (char *)malloc(strlen(strname) + 1);

    strcpy(strptr[i],strname);

}

return;

}
```

```
void funcout(char *strptr[ ], int NUMSTR)

{

    int i;

    printf("\nOutput strings:\n");

    for(i = 0; i < NUMSTR; i++)

    {

        printf("%2d ", strlen(strptr[i]));

        puts(strptr[i]);

    }

    printf("\n");

}
```

Input strings:
AAAAAAA
BBBBBBBBBBBBBB
EEEE
PPPPPPPPPPPPPPPP

Output strings:
12 AAAAAAA
14 BBBBBBBBBBBBBBB
4 EEEE
16 PPPPPPPPPPPPP

注意输入数据包含空格，且由于末尾空格被忽略，字符串长度不同。输入函数 `gets()` 输入包括换行符在内的数据并将其存储在 `strname` 中，该缓冲区有80个字符的空间。这是一个存储变长字符串的临时缓冲区。字符串被复制到动态存储中，分配的空间足以容每个字符串。每个字符串的地址赋值给指针数组的元素。动态存储分配函数 `malloc()` 用于从空闲存储分配空间以存储每个变长字符串。字符串复制函数 `strcpy` 用于将字符串从缓冲区 `strname` 复制到 `malloc()` 函数分配的空闲存储中。之后可以使用指针数组操作字符串。

### 10.5.3 复习题

- 1. 判断下列陈述对错。
  a. 如果字符串长度差异不大，可以将其存储在平滑数组中。
  b. 为了存储长度差异很大的字符串，应该使用动态存储。
  c. 动态存储分配函数 `malloc()` 可用于分配以存储字符串。

## 10.6 示例程序

这些示例程序演示了使用指针操作单个变量以及一维和二维数组。此外，本节介绍的部分程序使用了动态存储来操作一维、二维数组以及字符串。

### 10.6.1 拉伸应力

问题创建一个表格，显示宽度为 $w$、厚度为 $t$、长度为 $l$ 的矩形钢棒在变化的拉伸负载作用下的应力。要求用户输入负载范围和增量。

数据

输入截面尺寸。
输入最小载荷、最大载荷和增量大小。

方法

计算截面积。
计算表格中值的数量。

#### 指针与动态存储

为表格分配存储空间。

根据公式计算应力

$\sigma = p/area$;

其中 $\sigma$ 是以每平方英寸为单位的压力，$p$ 是以磅为单位的负载，$area 是受拉载荷的棒截面积。

输出负载和应力。

#### 伪代码

```
输入截面尺寸宽度 w 和厚度 t

area = w* t

输入负载最小值和最大增量

表格大小 = (loadmax - loadmin) / increment + 1

从最小到请求的最大负载循环

stress = load / area

结束

打印表格

停止
```

#### 程序

```
/******************************************************/
/* main: 计算矩形截面 */
/* 钢棒的应力 */
/* 使用数组指针 */
/*
/******************************************************/
/* 定义常量: */
/* --无-- */
/*
/* 输入变量: */
/* width -- 钢棒的截面宽度 */
/* thick -- 钢棒的截面厚度 */
/* minload -- 应用的最小负载 */
/* maxload -- 应用的最大负载 */
/* inc -- 负载增量 */
```

```
/*
* 计算变量:
* area - 截面面积
* stress - 柱应力
*/
/*
* 输出变量:
* load - 柱上的负载
* stress - 以磅为单位的拉伸应力
* 每平方英寸
************************************************
#include <stdio.h>

int main() {
    int i, n;
    float width, thick, area, minload, maxload, inc, stress;
    float *loadptr, *stressptr;
    scanf("%f %f", &width, &thick);
    scanf("%f %f", &minload, &maxload, &inc);
    area = width * thick;
    n = (maxload - minload)/ inc + 1;
    loadptr = (float *) calloc(n, sizeof(float));
    stressptr = (float *) calloc(n, sizeof(float));
    for(i = 0; i < n; i++) {
        *loadptr = minload + i * inc;
        *stressptr = *loadptr / area;
        loadptr++;
        stressptr++;
    }
    loadptr -= n;
    stressptr -= n;
    for(i = 0; i < n; i++) {
        printf("%8.2f      %8.2f\n", *loadptr, *stressptr);
        loadptr++;
        stressptr++;
    }
    return 0;
}
```

#### 指针与动态存储

#### 输入

3 4
1000 10000 1000

#### 输出

1000.00 83.33
2000.00 166.67
3000.00 250.00
4000.00 333.33
5000.00 416.67
6000.00 500.00
7000.00 583.33
8000.00 666.67
9000.00 750.00
10000.00 833.33

### 10.6.2 高于平均温度的天数

此程序使用数组指针来操作一维数组。

#### 问题

- 输入月份名称并显示该月的平均温度。确定平均温度高于该月平均水平的天数。

#### 数据

月份名称。

#### 方法

- 输入月份名称。
- 在表格中查找该月份以确定它有多少天（忽略闰年）。
- 为每日平均温度分配空间。
- 输入平均温度。
- 计算月平均温度。
- 打印月平均温度。
- 打印高于平均水平的天数。

#### 伪代码

```
输入月份名称

在月份名称数组中定位月份并获取天数

分配数组存储

对于每一天

    输入平均温度并存储在数组中

    将平均温度加到总和

结束

naverage = sum / ndays

输出平均值
```

```
对于每一天

    比较平均温度与平均值

    统计高于平均值的数量

结束

输出计数

停止
```

#### 程序

```
/********************************************************************/
/*  main: 计算总和和平均温度                  */
/*    使用数组指针                                     */
/* *********************************************************************/\
/*  定义常量:                                            */
/*    --无--                                                  */
/*  输入变量:                                              */
/*    month[] - 月份名称                               */
/*    dacnt - float 类型数字的个数               */
/*  计算变量:                                            */
/*    sum - 数字之和                                     */
/*    average - 数字的平均值                             */
/*    ndays - 月份中的天数                        */
/* */
```

```
/*
 * 输出变量:
 */
 * count - 高于平均值的天数

 */
 * sum - 数字之和

 */
 * average - 数字的平均值

 */

/*
 * 调用的函数:
 * funcmonth - 返回该份中的天数
 */

 ************************************************************************************

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int funcmonth(char []);
int main()
{
    int i, ndays, count;
    char month[10];
    float sum, average;
    float *avgtemp;
    scanf("%s", month);
    ndays = funcmonth(month);
    avgtemp = (float*)calloc(ndays, sizeof(float));
    sum = 0.0;
    for(i = 0; i < ndays; i++)
    {
        scanf("%f", avgtemp);
        sum += *avgtemp;
        avgtemp++;
    }
    average = sum / ndays;
    printf("average temperature for %s is %.2f\n", month, average);
    count = 0;
    for(i = 0; i < ndays; i++)
    {
        if(*avgtemp > average)
            count++;
        avgtemp++;
    }
```

```
printf("%d above average\n", count);
return 0;
```

```
/******************************************************************/
/* funcmonth: 返回月份的天数 */
/******************************************************************/
/* 输入参数:                               */
/*   datamoth - 月份名称                     */
/* 输出参数:                               */
/*   --无--                                       */
/* 局部变量:                                */
/*   days[] - 每个月份的天数         */
/*   month[][] - 每个月份名称的数组 */
/*                                                  

/* 返回变量:                               */
/*   ndays - 月份中的天数         */
/******************************************************************/
```

```
int funcmonth(char datamoth[])
{
  int days[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
  char month[12][10] = {"January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"};
  int k, ndays;
  for (k = 0; k < 12; k++)
    if(strcmp(month[k], datamoth) == 0)
      ndays = days[k];
  return ndays;
}
```

#### 指针与动态存储

#### 输入

- February
3 4
1000 10000 1000

#### 输出

1000.00 83.33
2000.00 166.67
3000.00 250.00
4000.00 333.33
5000.00 416.67
6000.00 500.00
7000.00 583.33
8000.00 666.67
9000.00 750.00
10000.00 833.33

### 10.6.2 高于平均温度的天数

此程序使用数组指针来操作一维数组。

#### 问题

- 输入月份名称并显示该月的平均温度。确定平均温度高于该月平均水平的天数。

#### 数据

月份名称。

#### 方法

- 输入月份名称。
- 在表格中查找该月份以确定它有多少天（忽略闰年）。
- 为每日平均温度分配空间。
- 输入平均温度。
- 计算月平均温度。
- 打印月平均温度。
- 打印高于平均水平的天数。

#### 伪代码

```
输入月份名称

在月份名称数组中定位月份并获取天数

分配数组存储

对于每一天

    输入平均温度并存储在数组中

    将平均温度加到总和

结束

naverage = sum / ndays

输出平均值
```

```
对于每一天

    比较平均温度与平均值

    统计高于平均值的数量

结束

输出计数

停止
```
