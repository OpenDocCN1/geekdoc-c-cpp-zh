
```c
Program
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
int main()
{
    int arr[],i,j,n,x,temp;
    clrscr();
    printf("Enter the number of elements in the array:");
    scanf("%d",&n);
    arr=(int*)malloc(sizeof(int)*n);
    for(i=0;i<n;i++) {
        printf("Enter a number:");
        scanf("%d",&arr[i]);
    }
    for(i=0;i<n;i++) {
        for(j=i+1;j<n;j++) {
            if(arr[i]>arr[j]) {
                temp=arr[i];
                arr[i]=arr[j];
                arr[j]=temp;
            }
        }
    }
    printf("\nElements of array after sorting:\n");
    for(i=0;i<n;i++) {
        printf("%d\n",arr[i]);
    }
    i=0;
    j=0;
    while(i<n) {
        if(arr[i]==arr[n-1]) {
            for(x=j;x<n-1;x++) {
                arr[x]=arr[x+1];
            }
            n--;
        } else {
            i++;
        }
        j++;
    }
}
```

# 9.12 计算机概念与 C 语言编程

## 输出

输入数组的元素个数:5

输入一个数字:3

输入一个数字:3

输入一个数字:4

输入一个数字:4

排序后的数组元素:

3

3

4

4

6

移除重复元素后的数组元素:

3

3

4

4

6

![](img/38c1ca180054ae68e900b256db416b54_269_0.png)

# 示例 9.6 编写一个查找数组中第 k 小元素的程序。

1. 设置数组的大小 `n`。
2. 存储 `n` 个元素并按升序排序数组元素。
3. 读取并排序数组元素。
4. 打印排序后数组的第 `k` 个元素。

程序见图 9.6。

```c
Program
#include <stdio.h>
#include <conio.h>
void main()
{
    int arr[],i,j,n,temp,k;
    clrscr();
    printf("Enter the number of elements in the array:\n");
    scanf("%d",&n);
    arr=(int*)malloc(sizeof(int)*n);
    for(i=0;i<n;i++)
    {
        printf("Enter a number:\n");
        scanf("%d",&arr[i]);
    }
    for(i=0;i<n;i++)
    {
        for(j=i+1;j<n;j++)
```

（续）

```c
{
        if(arr[i]>arr[j]){
            temp=arr[i];
            arr[i]=arr[j];
            arr[j]=temp;
        }
    }
    printf("\nElements of array after sorting:\n");
    for(i=0;i<n;i++)
        printf("\n%d",arr[i]);
}
    printf("\nWhich smallest element do you want?\n");
    scanf("%d",&k);
    if(k<=n)
        printf("\nDesired smallest element is %d.",arr[k-1]);
    else
        printf("\nPlease enter a valid value for finding the smallest element\n");
    getch();```

## 输出

输入数组的元素个数:5

输入一个数字:33

输入一个数字:32

输入一个数字:46

输入一个数字:47

排序后的数组元素:

32

33

46

47

想要哪个元素？

目标元素是 46。

图 9.6 查找数组中第 k 小元素的程序

# 9.5 二维数组

到为止我们讨论了可以存储值列表的数组变量。也有需要存储值表格的情况。考虑下表，显示了四位女性对三种商品的销售情况：

| 商品 1 | 商品 2 | 商品 3 |
|---|---|---|
| 女士 1 | 310 | 275 | 365 |
| 女士 2 | 210 | 190 | 325 |
| 女士 3 | 405 | 235 | 240 |
| 女士 4 | 260 | 300 | 380 |

# 9.14 计算机概念与 C 语言编程

表格共有 12 个值，每行一个。我们可以将其视为四行三列的矩阵。每行代表某个特定女性的值，每列代表某个特定商品的值。在数学中，我们使用下标 $v_{ij}$ 表示矩阵中的某个值。这里 $v_{ij}$ 代表第 $i$ 行第 $j$ 列的值。例如，在表中，$v_{23}$ 代表 325。

C 允许我们使用二维数组定义此类项目。上面的表格可以在 C 中定义为：

```c
int v[4][3];
```

二维数组声明如下：

```c
type array_name[row_size][column_size];
```

注意，与其他使用括号分离大小的语言不同，C 将每个项目放在自己的括号中。二维数组存储在内存中，如图 9.7 所示。与一维数组一样，数组的每个维度的索引从 0 到最大值减一；第一个索引选择行，第二个索引选择该行中的列。

![](img/38c1ca180054ae68e900b256db416b54_271_0.png)

| 列 0 | 列 1 | 列 2 |
|---|---|---|
| [0][0] | [0][1] | [0][2] |
| 310 | 190 | 365 |
| [1][0] | [1][1] | [1][2] |
| 405 | 235 | 240 |
| [2][0] | [2][1] | [2][2] |
| 310 | 275 | 365 |

> 示例 9.7 使用二维数组根据上述表格数据计算并打印以下信息：
>
> (a) 每个女性的销售总额。
>
> (b) 每种商品的销售总额。
>
> (c) 所有女性商品的销售总额。

程序及其输出见图 9.8。程序使用了二维变量 `value`，其中 `i` 代表行，`j` 代表商品。计算结果使用了以下方程：

- (a) 第 $m$ 位女性的总额 = $\sum value[m][j]$
- (b) 第 $n$ 个商品的总额 = $\sum value[i][n]$
- (c) 总额 = $\sum_{i=0}^{2} \sum_{j=0}^{2} value[i][j] = \sum_{j=0}^{2} item\_total[j]$

# 数组 9.15

```c
#define MAXGIRLS 4
#define MAXITEMS 3
main() {
    int value[MAXGIRLS][MAXITEMS];
    int girl_total[MAXGIRLS] , item_total[MAXITEMS];
    int i, j, grand_total;
    /*读取值并计算 girl_total ...*/
    printf("Input data\n");
    printf("Enter values, one at a time, row-wise\n");
    for (i = 0; i < MAXGIRLS; i++) {
        girl_total[i] = 0;
        for (j = 0; j < MAXITEMS; j++) {
            scanf("%d", &value[i][j]);
            girl_total[i] += value[i][j];
        }
    }
    /*计算 item_total...*/
    for (j = 0; j < MAXITEMS; j++) {
        item_total[j] = 0;
        for (i = 0; i < MAXGIRLS; i++) {
            item_total[j] = item_total[j] + value[i][j];
        }
    }
    /*计算 grand_total...*/
    grand_total = 0;
    for (i = 0; i < MAXGIRLS; i++) {
        grand_total = grand_total + girl_total[i];
    }
    /*打印结果...*/
    printf("\n GIRLS TOTALS\n\n");
    for (i = 0; i < MAXGIRLS; i++) {
        printf("Salesgirl%d = %d\n", i+1, girl_total[i]);
    }
    printf("\n ITEM TOTALS\n\n");
    for (j = 0; j < MAXITEMS; j++) {
        printf("Item%d = %d\n", j+1, item_total[j]);
    }
    printf("\nGrand Total = %d\n", grand_total);
}
```

# 9.16 计算机概念与C语言编程

```c
405 235 240
260 300 380
```

女孩总计

Salesgirl[1] = 950

Salesgirl[2] = 725

Salesgirl[3] = 880

Salesgirl[4] = 940

项目总计

Item[1] = 1185

Item[2] = 1000

Item[3] = 1310

> 图 9.8 二维数组示意图

示例 9.8 编写一个程序，计算并打印 1 到 5 的乘法表，如下：

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| 1 | 1 | 2 | 3 | 4 | 5 |
| 2 | 2 | 4 | 6 | 8 | 10 |
| 3 | 3 | 6 | 9 | 12 | 15 |
| 4 | 4 | 8 | 12 | 16 | 20 |
| 5 | 5 | 10 | 15 | 20 | 25 |

图 9.9 所示程序使用二维数组来存储表格值。每个值的计算使用嵌套循环的控制变量，如下：

```
product[i][j] = row * column
```

其中 `i` 表示行，`j` 表示列。由于索引 `i` 和 `j` 的范围是从 0 到 4，我们引入了以下转换：

```
row = i+1
column = j+1
```

程序

```c
#define ROWS 5
#define COLUMNS 5
main() {
    int row, column, product[ROWS][COLUMNS];
    int i, j;
    printf("MULTIPL TABLE\n");
    printf("----------------------\n");
    for(i = 1; i <= ROWS; i++) {
        printf("%d", i);
        for(j = 1; j <= COLUMNS; j++) {
            printf("%d", product[i-1][j-1]);
        }
        printf("\n");
    }
    printf("----------------------\n");
    printf("-----------------\n");
}
```

（续）

# 乘法表

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| 1 | 1 | 2 | 3 | 4 | 5 |
| 2 | 2 | 4 | 6 | 8 | 10 |
| 3 | 3 | 6 | 9 | 12 | 15 |
| 4 | 4 | 8 | 12 | 16 | 20 |
| 5 | 5 | 10 | 15 | 20 | 25 |

图 9.9 使用二维数组打印乘法表的程序

## 9.6 初始化二维数组

与一维数组一样，二维数组通过其声明和在大括号括起来的初始值列表进行初始化。例如，

```c
int table[2][3] = {0,0,0,1,1,1};
```

将第一行的元素初始化为零，第二行初始化为一。上面的语句可以等价地通过大括号包裹的形式写成：

```c
int table[2][3] = {{0,0,0},{1,1,1}};
```

我们也可以像下面所示将二维数组初始化为矩阵：

```c
int table[2][3] = {
    {0,0,0},
    {1,1,1}
};
```

注意上述语句的语法。在每个关闭行的大括号后面都需要逗号（最后一行除外）。当数组使用所有显式值进行完全初始化时，我们不需要需要指定第一维的大小。也就是说，语句

```c
int table [] = {
    {0, 0, 0},
    {1, 1, 1}
};
```

是允许的。

如果初始化器中缺少值，它们将被自动设置为零。例如，语句

```c
int table[2][3] = {
  {1,1},
  {2}
};
```

将第一行的前两个元素初始化为一，第二行的第一个元素初始化为二，所有其他元素初始化为零。

当所有元素都要初始化为零时，可以使用截断法。

```c
int m[3][5] = {{0}, {0}, {0}};
```

每行的第一个元素初始化为零，而其他元素自动初始化为零。以下语句也可以实现结果：

```c
int m[3][5] = {0, 0, 0};
```

| 示例 9.9 | 在四个城市（孟买、德里和马德拉斯）对四种汽车（大使号、加尔各答、菲特、海豚和马鲁蒂）的受欢迎程度进行了调查。每位受访者都被要求提供所在的城市和使用的汽车类型。编码形式的结果如表所示： |
|---|---|
| M | 1 | C | 2 | B | 1 | D | 3 | M | 2 | B |
| C | 1 | D | 3 | M | 4 | B | 2 | D | 1 | C | 3 |
| D | 4 | A | 4 | M | 1 | M | 1 | B | 3 | B |
| C | 1 | C | 1 | M | 2 | M | 4 | C | 2 |
| D | 1 | C | 2 | B | 3 | M | 1 | B | 1 |

代码代表以下信息：

- 大使号 - 1
- 德里 - 2
- 加尔各答 - 3
- 孟买 - 4

编写一个程序生成四个城市汽车受欢迎程度的表格。使用二维数组作为累加器来存储每个城市的汽车数量。例如，`frequency[i][j]` 表示 `i` 城市 `j` 型汽车的数量。`frequency` 初始化为 5x5 的数组，所有元素初始化为零。图 9.10 程序从终端读取城市代码和汽车代码。当读取到字母 X 时，统计结束。

程序

```c
main() {
    int i, j, car;
    int frequency[5][5] = {{0,0,0,0,0},{0,0,0,0,0},{0,0,0,0,0},{0,0,0,0,0},{0,0,0,0,0}};
    char city;
    printf("每位个人，输入城市代码");
    for(i = 1; i < 100; i++) {
        scanf("%c", &city);
        if (city == 'X') break;
        scanf("%d", &car);
        switch(city) {
            case 'B': frequency[i-1][1]++; break;
            case 'C': frequency[i-1][2]++; break;
            case 'D': frequency[i-1][3]++; break;
            case 'M': frequency[i-1][4]++; break;
        }
    }
    /* 统计完成并打印 */
    printf("\n");
    printf("POP TABLE\n");
    printf("City Ambassador Dolphin Maruti\n");
    for(i = 1; i <= 4; i++) {
        printf("%d ", i);
        for(j = 1; j <= 4; j++) {
            printf("%d ", frequency[i-1][j-1]);
        }
        printf("\n");
    }
    printf("-------\n");
    /* 打印结束 */
}
```

（续）

输出

每位个人，输入城市代码后输入汽车代码。
