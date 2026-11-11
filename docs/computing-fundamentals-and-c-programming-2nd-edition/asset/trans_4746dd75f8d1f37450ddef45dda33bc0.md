

当项目数量为偶数时，有两个中间值。因此，偶数个项目的中位数被指定为这两个中间值的平均值。

求中位数的主要步骤如下：

- 1. 将项目读入数组，同时记录项目的数量。
- 2. 将项目按递增顺序排序。
- 3. 计算中位数。

程序和示例输出如图 9.10 所示。所使用的排序算法如下：

- 1. 比较列表中的前两个元素，例如 a[1] 和 a[2]。如果 a[2] 小于 a[1]，则交换它们的值。
- 2. 比较 a[2] 和 a[3]；如果 a[3] 小于 a[2]，则交换它们。
- 3. 继续此过程，直到比较并交换最后两个元素。
- 4. 重复上述步骤 n–1 次。

在反复遍历数组的过程中，最小的元素会“冒泡”到顶部。由于这种冒泡效应，该算法称为冒泡排序。下面以四个项目为例说明冒泡效应。

![](img/11b034a94fc590add0a7808250a38792_331_0.png)

在第一次遍历中，比较三对项目，并在需要时进行交换。应当注意，数字 80（项目中最大的数）在第一次遍历结束时已被移到底部。这意味着元素 80（新列表中的最后一项）无需再考虑。因此，第二次遍历只需要比较两对。这一次，数字 65（第二大值）已被向下移动。请注意，每次遍历都会将最小值 10 向上提升一级。

每进行一次遍历，所需的步骤数就减少一步。当一次遍历只包含一个步骤时，整个过程结束。如果列表包含 **n** 个元素，则涉及的比较次数为 **n(n−1)/2**。

**程序**

```c
#define N 10
main( )
{
    int i,j,n;
    float median,a[N],t;
    printf("Enter the number of items\n");
    scanf("%d", &n);
    /* Reading items into array a */
    printf("Input %d values \n",n);
    for (i = 1; i <= n ; i++)
        scanf("%f", &a[i]);
    /* Sorting begins */
    for (i = 1 ; i <= n-1 ; i++)
    {
        /* Trip-i begins */
        for (j = 1 ; j <= n-i ; j++)
        {
            if (a[j] <= a[j+1])
            {
                /* Interchanging values */
                t = a[j];
                a[j] = a[j+1];
                a[j+1] = t;
            }
            else
                continue ;
        }
    } /* sorting ends */
    /* calculation of median */
    if ( n % 2 == 0)
        median = (a[n/2] + a[n/2+1])/2.0 ;
    else
        median = a[n/2 + 1];
    /* Printing */
    for (i = 1 ; i <= n ; i++)
```

**程序**

```c
#include <math.h>
#define MAXSIZE 100
main( )
{
    int i, n;
    float value[MAXSIZE], deviation,
          sum,sumsqr,mean,variance,stddeviation;
    sum = sumsqr = n = 0 ;
    printf("Input values: input -1 to end \n");
    for (i=1; i< MAXSIZE ; i++)
    {
        scanf("%f", &value[i]);
        if (value[i] == -1)
            break;
        sum += value[i];
        n += 1;
    }
    mean = sum/(float)n;
    for (i = 1 ; i<= n; i++)
    {
        deviation = value[i] - mean;
        sumsqr += deviation * deviation;
    }
    variance = sumsqr/(float)n ;
    stddeviation = sqrt(variance) ;
    printf("\nNumber of items : %d\n",n);
    printf("Mean : %f\n", mean);
    printf("Standard deviation : %f\n", stddeviation);
}
```

**输出**

```text
Input values: input -1 to end
65 9 27 78 12 20 33 49 -1
Number of items : 8

Mean : 36.625000
Standard deviation : 23.510303
```

*图 9.11 计算标准差的程序*

## 3. 评估测试 [LO 9.2, H]

向一批 3 名学生进行了一次包含 25 道多项选择题的测试。正确答案和学生作答情况如下表所示：

| 题号 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 正确答案 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 学生 1 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 学生 2 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 学生 3 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

评估学生答案的算法如下：

- 1. 将正确答案读入一个数组。
- 2. 读取一名学生的作答并统计正确答案的数量。
- 3. 对每名学生重复步骤 2。
- 4. 打印结果。

实现该算法的程序如图 9.12 所示。该程序使用以下数组：

- `key[i]` — 存储题目的正确答案
- `response[i]` — 存储学生的作答
- `correct[i]` — 用于标识回答正确的题目

**程序**

```c
#define STUDENTS 3
#define ITEMS 25
main( )
{
    char key[ITEMS+1],response[ITEMS+1];
    int count, i, student,n,
        correct[ITEMS+1];
    /* Reading of Correct answers */
    printf("Input key to the items\n");
    for(i=0; i < ITEMS; i++)
        scanf("%c",&key[i]);
    scanf("%c",&key[i]);
    key[i] = '\0';
    /* Evaluation begins */
    for(student = 1; student <= STUDENTS ; student++)
    {
    /*Reading student responses and counting correct ones*/
    count = 0;
    printf("\n");
    printf("Input responses of student-%d\n",student);
    for(i=0; i < ITEMS ; i++)
      scanf("%c",&response[i]);
    scanf("%c",&response[i]);
    response[i] = '\0';
    for(i=0; i < ITEMS; i++)
      correct[i] = 0;
    for(i=0; i < ITEMS ; i++)
      if(response[i] == key[i])
      {
        count = count +1 ;
        correct[i] = 1 ;
      }
    /* printing of results */
    printf("\n");
    printf("Student-%d\n", student);
    printf("Score is %d out of %d\n",count, ITEMS);
    printf("Response to the items below are wrong\n");
    n = 0;
    for(i=0; i < ITEMS ; i++)
      if(correct[i] == 0)
      {
        printf("%d ",i+1);
        n = n+1;
      }
    if(n == 0)
      printf("NIL\n");
    printf("\n");
    } /* Go to next student */
    /* Evaluation and printing ends */
}
```

**输出**

```text
Input key to the items
abcdabcdabcdabcdabcdabcda
Input responses of student-1
abcdabcdabcdabcdabcdabcda
Student-1
Score is 25 out of 25
Response to the following items are wrong
NIL
```

我们将生产和销售的产品价值用两个价值数组表示，即 **Mvalue** 和 **Svalue**。那么，

`Mvalue[i][j] = Mij x Cj`

`Svalue[i][j] = Sij x Cj`

生成评审会议所需输出的程序如图 9.13 所示。还使用了以下附加变量：

- **Mweek[i]** = 第 i 周生产的所有产品的价值  
  `= Σ_{j=1}^{5} Mvalue[i][j]`
- **Sweek[i]** = 第 i 周销售的所有产品的价值  
  `= Σ_{j=1}^{5} Svalue[i][j]`
- **Mproduct[j]** = 该月生产的第 j 类产品的价值  
  `= Σ_{i=1}^{4} Mvalue[i][j]`
- **Sproduct[j]** = 该月销售的第 j 类产品的价值  
  `= Σ_{i=1}^{4} Svalue[i][j]`
- **Mtotal** = 该月生产的所有产品的总价值  
  `= Σ_{i=1}^{4} Mweek[i] = Σ_{j=1}^{5} Mproduct[j]`
- **Stotal** = 该月销售的所有产品的总价值  
  `= Σ_{i=1}^{4} Sweek[i] = Σ_{j=1}^{5} Sproduct[j]`

**程序**

```c
main( )
{
    int M[5][6],S[5][6],C[6],
        Mvalue[5][6],Svalue[5][6],
        Mweek[5], Sweek[5],
        Mproduct[6], Sproduct[6],
        Mtotal, Stotal, i,j,number;
    /* Input data */
    printf (" Enter products manufactured week wise \n");
    printf (" M11,M12,--, M21,M22,-- etc\n");
    for(i=1; i<4; i++)
        for(j=1; j<5; j++)
            scanf ("%d", &M[i][j]);
      }
    }
/* Grand total of production and sales values */
    Mtotal = Stotal = 0;
    for(i=1; i<=4; i++)
    {
        Mtotal += Mweek[i];
        Stotal += Sweek[i];
    }
/****************************************
 Selection and printing of information required
 ****************************************/
    printf("\n\n");
    printf(" Following is the list of things you can\n");
    printf(" request for. Enter appropriate item number\n");
    printf(" and press RETURN Key\n\n");
    printf(" 1.Value matrices of production & sales\n");
    printf(" 2.Total value of weekly production & sales\n");
    printf(" 3.Product_wise monthly value of production &");
    printf(" sales\n");
    printf(" 4.Grand total value of production & sales\n");
    printf(" 5.Exit\n");
    number = 0;
    while(1)
    {    /* Beginning of while loop */
        printf("\n\n ENTER YOUR CHOICE:");
        scanf("%d",&number);
        printf("\n");
        if(number == 5)
        {
        printf(" GOOD BYE\n\n");
        break;
        }
        switch(number)
        {  /* Beginning of switch */
        /* VALUE MATRICES */
            case 1:
            printf(" VALUE MATRIX OF PRODUCTION\n\n");
            for(i=1; i<=4; i++)
            {
```

