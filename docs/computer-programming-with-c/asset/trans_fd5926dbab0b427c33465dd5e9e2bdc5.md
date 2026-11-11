
```c
int r,c,i,j;
printf("Enter the order of the matrix ");
scanf("%d%d",&r,&c);
int a[100][100],b[100][100], Res[100][100];
printf("Enter Matrix a\n");
    for(i=0;i<=r-1;i++)
    {
        for(j=0;j<=c-1;j++)
        {
            scanf("%d",&a[i][j]);
        }
    }
    printf("Enter Matrix b\n");
        for(i=0;i<=r-1;i++)
        {
            for(j=0;j<=c-1;j++)
            {
                scanf("%d",&b[i][j]);
            }
        }
    /*perform addition*/
    printf("Addition is \n");
        for(i=0;i<=r-1;i++)
        {
            for(j=0;j<=c-1;j++)
            {
                Res[i][j]=a[i][j]+b[i][j];
                printf("%d",Res[i][j]);
            }
            printf("\n");
        }
    }/*end of main*/
```

**输出：**

```text
Enter the order of the matrix 2 2
Enter Matrix a
10 20
25 15
Enter Matrix b
5   6
10  5
Addition is
15  26
35  20
```

### 6.4.2 矩阵乘法程序：示例

作为示例，让我们编写一个程序，从用户处输入两个矩阵 a 和 b，并执行 a 与 b 的乘法，将结果存储在另一个矩阵 Res 中。设矩阵 a 有 r1 行和 c1 列，矩阵 b 有 r2 行和 c2 列。此外，我们知道，只有当第一个矩阵的列数与第二个矩阵的行数相同时，才能执行两个矩阵的乘法。因此，仅当 c1 的值与 r2 相同时，我们才执行矩阵乘法，如代码所示。在开始乘法过程之前，我们从用户处输入具有 r1 行和 c1 列的矩阵 a，以及具有 r2 行和 c2 列的矩阵 b，如代码所示。

假设矩阵 a 和 b 的阶为 3X3，并且用户在两个矩阵中分别输入如图 6.34 所示的值。

**具有 3 行 3 列的二维数组 “a”**

|   | 0 | 1 | 2 |
|---|---:|---:|---:|
| 0 | 10 | 20 | 30 |
| 1 | 50 | 60 | 70 |
| 2 | 90 | 100 | 110 |

**具有 3 行 3 列的二维数组 “b”**

|   | 0 | 1 | 2 |
|---|---:|---:|---:|
| 0 | 5 | 8 | 3 |
| 1 | 6 | 2 | 70 |
| 2 | 12 | 10 | 5 |

**图 6.34：** 两个矩阵的用户输入数据

此外，我们知道，如果矩阵 a 的阶为 r1Xc1，矩阵 b 的阶为 r2Xc2，那么由 a 与 b 相乘得到的结果矩阵 Res 的阶将为 r1Xc2。因此，Res 矩阵始终按行从 0 迭代到 r1−1，按列从 0 迭代到 c2−1，如图 6.35 所示。

```c
for(i=0;i<=r1-1;i++)
{
    for(j=0;j<=c2-1;j++)
    {
        Res[i][j]=0;
        for(k=0;k<=c1-1;k++)
        {
            Res[i][j]+=a[i][k]*b[k][j];
        }
    }
}

// Order of result matrix is r1Xc2
// Initial value of sum=0
// Loop used to calculate sum of products
// k is used as column index for matrix a and row index of matrix b
```

**图 6.35：** 矩阵乘法

为了理解乘法过程，让我们计算 Res[0][0] 的值，它是结果矩阵的第一个元素。Res[0][0] 的值将按如下方式计算：

Res[0][0] = a[0][0]*b[0][0] + a[0][1]*b[1][0] + a[0][2]*b[2][0];

代入图 6.34 中的值，可得

Res[0][0] = 10*5 + 20*6 + 30*12
Res[0][0] = 530

因此，对于第 i 行第 j 列的元素，我们可以按如下方式计算 Res[i][j]：

Res[i][j] = a[i][0]*b[0][j] + a[i][1]*b[1][j] + a[i][2]*b[2][j];

注意，在计算乘积之和时，第一个矩阵的列号在第一项中为 0，在第二项中为 1，在第三项中为 2。类似地，第二个矩阵 b 的行号在第一项中为 0，在第二项中为 1，在第三项中为 2。此外，在计算乘积之和时，第一个矩阵的列号/第二个矩阵的行号范围为 0 到 2。因此，我们有一个最内层 for 循环，它对 k = 0、k = 1 和 k = 2 的值运行，这些值迭代第一个矩阵的列和第二个矩阵的行。变量 k 的 for 循环必须恰好运行三次，因为第二个矩阵的行数为 3（这也与第一个矩阵的列数相同）。因此，使用变量 k 递增第一个矩阵的列号/第二个矩阵的行号的最内层 for 循环如图 6.35 所示。

执行矩阵乘法的完整源代码如下所示：

```c
#include<stdio.h>
void main()
{
    int a[100][100],b[100][100], Res[100][100];
    int r1,c1,r2,c2,i,j,k;
    printf("Enter the order of the matrix a ");
    scanf("%d%d",&r1,&c1);
    printf("Enter the order of the matrix b ");
    scanf("%d%d",&r2,&c2);
    if(c1==r2)
    {
        printf("Enter Matrix a\n");
        for(i=0;i<=r1-1;i++)
        {
            for(j=0;j<=c1-1;j++)
            {
                scanf("%d",&a[i][j]);
            }
        }
        printf("Enter Matrix b\n");
        for(i=0;i<=r2-1;i++)
        {
            for(j=0;j<=c2-1;j++)
            {
                scanf("%d",&b[i][j]);
            }
        }
        /*perform multiplication*/
        printf("Multiplication is\n");
        for(i=0;i<=r1-1;i++)
        {
            for(j=0;j<=c2-1;j++)
            {
                Res[i][j]=0;
                for(k=0;k<=c1-1;k++)
                {
                    Res[i][j]+=a[i][k]*b[k][j];
                }
                printf("%d ",Res[i][j]);
            }
            printf("\n");
        }
    }
    else
    {
        printf("Multiplication is not possible\n");
    }
}
/*end of main*/
```

**输出：**

```text
Enter the order of the matrix a 2 2
Enter the order of the matrix b 2 2
Enter Matrix a
10 2
1 0
Enter Matrix b
5 6
10 5
Multiplication is
70 70
5 6
```

## 6.5 字符二维数组

与任何其他二维数组类似，我们也可以创建字符二维数组。例如，语句

```c
char a[3][4];
```

创建一个具有 3 行 4 列的字符二维数组。该数组可以逐字符初始化，如图 6.36 所示。注意，我们在每一行中都显式存储了 NULL 字符 `\0`，因为在逐字符初始化的情况下，C/C++ 不会自动添加 `\0`。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_276_0.png)

**图 6.36：** 二维数组的逐字符初始化

正如 6.3 节所解释的，当字符数组以 `\0` 终止时，它也称为**字符串**。字符串的优点是我们可以直接对字符串执行输入和输出操作。如图 6.36 所示，二维数组中的每一行都以 `\0` 终止，因此我们可以将二维数组视为存储 3 个字符串的数组（而不是将其视为 12 个不同字符的数组）。

让我们将图 6.36 中的结构与单个一维字符数组进行比较。语句

```c
char b[4] = "rat";
```

创建一个名为 b 的一维数组，并在其中存储字符串 rat，如图 6.37 所示。

由于存在 NULL 字符，我们可以使用以下语句直接打印字符串 b：

```c
printf("%s",b);
```

![](img/57c0d966bb33c67a5a188e6bf39e4e02_276_1.png)

**图 6.37：** 存储在名为 b 的一维数组中的字符串

图 6.36 中指定的二维数组实际上可以视为三个不同的一维字符数组，使得每个一维数组包含一个字符串。下一个问题是：这些单独的一维数组的名称是什么？我们知道，当行索引为

```c
{"Zero","One","Two","Three","Four","Five","Six","Seven","Eight","Nine"};
int s=0,x,d, a[100];
int w;
printf("Enter a number: ");
scanf("%d",&x);
int i=0;
while(x!=0)
{
    d=x%10; //get the individual digit
    a[i]=d;
    i++;
    x=x/10;  //Use quotient for the next addition
}
/*Traverse the array in reverse direction*/
printf("The word format is: ");
for(w=i-1;w>=0;w--)
{
    printf("%s ",words[a[w]]);
}
}
```

**输出：**

Enter a number: 1265

The word format is: One Two Six Five

**语句**

```c
char words[ ][15]=
{"Zero","One","Two","Three","Four","Five","Six","Seven",
"Eight","Nine" };
```

创建一个字符串数组，它以单词形式存储每个数字，如图 6.39 所示。

**语句**

```c
printf("Enter a number: ");
scanf("%d",&x);
```

从用户处接受一个数字 x 作为输入，该数字将被转换为单词。

我们使用除以 10 的方法来提取 x 的各个数字。while 循环提取的每个数字都存储在数组 a 中。数字提取逻辑与我们在第 5 章第 5.2.4 节中设计的逻辑非常相似。因此，数字将按相反顺序提取。所以，如果输入值 x 为 1265，则数组 a 将按相反顺序包含这些数字，如图 6.40 所示。

因此，为了将每个数字转换为单词，我们必须按相反方向迭代数组（必须先访问数组的最后一个元素，这样我们才能恢复正确的顺序）。

**数组 words**

| 索引 | 值 |
|---:|---|
| 0 | "Zero" |
| 1 | "One" |
| 2 | "Two" |
| 3 | "Three" |
| 4 | "Four" |
| 5 | "Five" |
| 6 | "Six" |
| 7 | "Seven" |
| 8 | "Eight" |
| 9 | "Nine" |

*图 6.39：数组 words*

**数组 a**

| 5 | 6 | 2 | 1 |
|---:|---:|---:|---:|
| 0 | 1 | 2 | 3 |

*图 6.40：数组 a*

