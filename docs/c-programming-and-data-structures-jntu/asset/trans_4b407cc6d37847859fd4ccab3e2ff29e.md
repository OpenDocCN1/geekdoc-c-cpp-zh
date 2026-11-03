

## 2. 标准差的计算

在统计学中，标准差用于衡量数据相对于其均值的离散程度。计算 n 个项的标准差的公式为

$s = \sqrt{\text{方差}}$

其中 $\text{方差} = \frac{1}{n} \sum_{i=1}^{n} (x_i - m)^2$

并且 $m = \text{均值} = \frac{1}{n} \sum_{i=1}^{n} x_i$

计算标准差的算法如下：

- 1. 读取 n 个项。
- 2. 计算这些项的总和与均值。
- 3. 计算方差。
- 4. 计算标准差。

带有示例输出的完整程序如图 8.8 所示。

```c
/* --------------------------------------------------------------- */
/* PROGRAM TO CALCULATE STANDARD DEVIATION */
/* --------------------------------------------------------------- */
#include <math.h>
#define MAXSIZE 100
main()
{
    int i,n;
    float value[MAXSIZE], deviation,
          sum,sumsqr,mean,variance,stddeviation;
    sum = sumsqr = n = 0;
    printf("Input values: input -1 to end\n");
    for (i = 1; i <= MAXSIZE; i++)
    {
        scanf("%f", &value[i]);
        if (value[i] == -1)
            break;
        sum += value[i];
        n += 1;
    }
    mean = sum/(float)n;
    for (i = 1 ; i <= n; i++)
    {
        deviation = value[i] - mean;
        sumsqr += deviation * deviation;
    }
    variance = sumsqr/(float)n;
    stddeviation = sqrt(variance);

    printf("\nNumber of items : %d\n",n);
    printf("Mean : %f\n", mean);
    printf("Standard deviation : %f\n", stddeviation);
}
```

### 输出

```text
Input values: input -1 to end
65 9 27 78 12 20 33 49 -1
Number of items : 8
Mean : 36.625000
Standard deviation : 23.510303
```

### 图 8.8 计算标准差的程序

## 3. 评估一次测验

一份包含 25 道多项选择题的测验被用于一批 3 名学生。正确答案和学生的回答如下表所示：

| 题号 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 正确答案 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 学生 1 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 学生 2 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 学生 3 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

评估学生答案的算法如下：

- 1. 将正确答案读入一个数组。
- 2. 读取一名学生的回答并统计正确答案的数量。
- 3. 对每位学生重复步骤 2。
- 4. 打印结果。

实现该算法的程序如图 8.9 所示。该程序使用了以下数组：

- key[i] — 存储题目的正确答案
- response[i] — 存储学生的回答
- correct[i] — 用于标记回答正确的题目。

```c
/*
******************************* */
/*      PROGRAM TO EVALUATE A MULTIPLE-CHOICE TEST      */
/*
******************************* */

#define STUDENT 3
#define ITEMS 25
main()
{
    char key[ITEMS+1], response[ITEMS+1];
    int count, i, student,n,
        correct[ITEMS+1];

    /* Reading of Correct answers */
    printf("Input key to the items\n");
    for(i=0; i < ITEMS; i++)
    {
        scanf("%c", &key[i]);
    }
    /* Evaluation begins */
    for(student = 1; student <= STUDENT; student++)
    {
        /*Reading student responses and counting correct ones*/
        count = 0;
        printf("\n");
        printf("Input responses of student--%d\n", student);
        for(i=0; i < ITEMS ; i++)
        {
            scanf("%c", &response[i]);
        }
        for (i = 0; i < ITEMS; i++)
            correct[i] = 0;
        for(i=0; i < ITEMS; i++)
        {
            if(response[i] == key[i])
            {
                count = count + 1;
                correct[i] = 1;
            }
        }
        /* printing of results */
        printf("\n");
        printf("Student--%d\n", student);
        printf("Score is %d out of %d\n", count, ITEMS);
        printf("Response to the items below are wrong\n");
        n = 0;
        for(i=0; i < ITEMS ; i++)
        {
            if(correct[i] == 0)
            {
                printf("%d", i+1);
                n = n +1;
            }
        }
        if(n == 0)
        {
            printf("NIL\n");
        }
        printf("\n");
    } /* Go to next student */
    /* Evaluation and print ends */
}
```

### 输出

```text
Input key to the items
abcdabcdabcdabcdabcdabcda
Input responses of student-1
abcdabcdabcdabcdabcdabcda
Student-1
Score is 25 out of 25
Response to the following items are wrong
NIL
Input responses of student-2
abcdcbaabcdabcd... 
Student-2
Score is 14 out of 25
Response to the following items are wrong
5 6 7 8 17 18 19 21 22 23 25
Input responses of student-3
aaaaaaaaaaaaaaaaaaaaaaaaaa
Student-3
Score is 7 out of 25
Response to the following items are wrong
2 3 4 6 7 8 10 11 12 14 15 16 18 19 20 22 23 24
```

### 图 8.9 评估多项选择测验回答的程序

## 4. 生产与销售分析

一家公司生产五种类别的产品，并且在一个月内每周按产品记录生产与销售的数量。公司每月月底审查其生产计划。审查可能需要以下一项或多项信息：

- (a) 每周生产和销售的价值。
- (b) 所有已生产产品的总价值。
- (c) 所有已售出产品的总价值。
- (d) 每种已生产和已售出产品的总价值。

让我们分别用两个二维数组 M 和 S 表示已生产和已售出的产品。那么，

M =

|  | M11 | M12 | M13 | M14 | M15 |
|---|---|---|---|---|---|
|  | M21 | M22 | M23 | M24 | M25 |
|  | M31 | M32 | M33 | M34 | M35 |
|  | M41 | M42 | M43 | M44 | M45 |

S =

|  | S11 | S12 | S13 | S14 | S15 |
|---|---|---|---|---|---|
|  | S21 | S22 | S23 | S24 | S25 |
|  | S31 | S32 | S33 | S34 | S35 |
|  | S41 | S42 | S43 | S44 | S45 |

其中 Mij 表示第 i 周生产的第 j 类产品的数量，Sij 表示第 i 周售出的第 j 类产品的数量。我们还可以用一维数组 C 表示每种产品的成本，如下所示：

C =

| C1 | C2 | C3 | C4 | C5 |
|---|---|---|---|---|

其中 Cj 是第 j 类产品的成本。

我们将用两个价值数组（即 Mvalue 和 Svalue）表示已生产和已售出产品的价值。那么，

Mvalue[i][j] = Mij x Cj

Svalue[i][j] = Sij x Cj

用于生成审查会议所需输出的程序如图 8.10 所示。还使用了以下附加变量：

Mweek[i] = 第 i 周生产的所有产品的价值。
= Σ j=1 到 5 Mvalue[i][j]

Sweek[i] = 第 i 周售出的所有产品的价值
= Σ j=1 到 5 Svalue[i][j]

Mproduct[j] = 该月生产的第 j 类产品的价值
= Σ i=1 到 4 Mvalue[i][j]

Sproduct[j] = 该月售出的第 j 类产品的价值
= Σ i=1 到 4 Svalue[i][j]

Mtotal = 该月生产的所有产品的总价值
= Σ i=1 到 4 Mweek[i] = Σ j=1 到 5 Mproduct[j]

Stotal = 该月售出的所有产品的总价值
= Σ i=1 到 4 Sweek[i] = Σ j=1 到 5 Sproduct[j]

```c
/***************************************************************/
/*     PRODUCTION AND SALES ANALYSIS     */
/***************************************************************/
main()
{
    int M[5][6], S[5][6], C[6],
        Mvalue[5][6], Svalue[5][6],
        Mweek[5], Sweek[5],
        Mproduct[6], Sproduct[6],
        Mtotal, Stotal, i,j,number;

    /* Input data */
    printf("Enter products manufactured week_wise\n");
    printf(" M11,M12 .... M21, M22, etc\n");
    for(i=1;i<=4; i++)
    {
        for(j=1;j<=5; j++)
        {
            scanf("%d",&M[i][j]);
        }
    }
    printf("Enter products sold week_wise\n");
    printf(" S11, S12, .... S21, S22, ....etc\n");
    for(i=1;i<=4; i++)
    {
        for(j=1;j<=5; j++)
        {
            scanf("%d",&S[i][j]);
        }
    }
    printf("Enter cost of each product\n");
    for(i=1;i<=5; i++)
    {
        scanf("%d",&C[i]);
    }
    /* Value matrices of production and sales */
    for(i=1;i<=4; i++)
    {
        for(j=1;j<=5; j++)
        {
            Mvalue[i][j] = M[i][j] * C[j];
            Svalue[i][j] = S[i][j] * C[j];
        }
    }
    /* Total value of weekly production and sales */
    for(i=1;i<=4; i++)
    {
        Mweek[i] = 0;
        Sweek[i] = 0;
        for(j=1;j<=5; j++)
        {
            Mweek[i] += Mvalue[i][j];
            Sweek[i] += Svalue[i][j];
        }
    }
    /* Monthly value of product_wise production and sales */
    for(j=1;j<=5; j++)
    {
        Mproduct[j] = 0;
        Sproduct[j] = 0;
        for(i=1;i<=4; i++)
        {
            Mproduct[j] += Mvalue[i][j];
            Sproduct[j] += Svalue[i][j];
        }
    }
    /* Grand total of production and sales values */
    Mtotal = Stotal = 0;
    for(i=1;i<=4; i++)
    {
        Mtotal += Mweek[i];
```

