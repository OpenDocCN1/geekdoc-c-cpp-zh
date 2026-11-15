
## 6.5 应用问题求解：地震事件检测

- 地震仪
- 里氏震级
- 地震事件
- 短时功率
- 长时功率
- 阈值
- 数据窗口

名为**地震仪**的特殊传感器用于收集地球运动信息。这些地震仪可用于被动环境，在该环境中，它们记录地球的运动，包括地震和潮汐运动。通过使用多个地震仪的数据来分析地震引起的地面运动，可以确定地震的震中和地震强度。强度通常使用**里氏震级**来测量，这是一个从1到10的等级，以美国地震学家C. F. Richter的名字命名。

编写一个程序，从名为 `seismic1.txt` 的数据文件中读取一组地震仪数据。文件的第一行包含两个值——文件中随后的地震仪数据读数的数量，以及连续测量之间发生的时间间隔（以秒为单位）。这个时间间隔是一个浮点值，我们假设所有测量之间都有相同的时间间隔。在读取并存储数据测量值后，程序应使用功率比来识别可能的地震，也称为**地震事件**。在特定时间点，该比率是**短时功率**测量值除以**长时功率**测量值的商。如果比率大于给定的**阈值**，则可能在该时间点发生了事件。给定数据测量中的特定点时，短时功率是使用指定点加上紧邻指定点之前的少量点的测量值的平均功率，即平均平方值。长时功率是使用指定点加上紧邻指定点之前的较多点的测量值的平均功率。（用于计算的一组点有时称为**数据窗口**。）阈值通常大于1，以避免在恒定数据中检测事件，因为如果数据值都相同，短时功率等于长时功率。假设短时功率和长时功率的测量数量从键盘读取。将阈值设置为1.5。

### 1. 问题描述

使用来自数据文件的一组地震仪测量值来确定可能地震事件的位置。

### 2. 输入/输出描述

输入是名为 `seismic1.txt` 的数据文件以及用于短时功率和长时功率的测量数量。输出是一份给出潜在地震事件时间的报告。

![](img/02c4582f051c5b51776411c92b079035_331_0.png)

### 3. 手算示例

假设数据文件包含以下数据，其中包括随后的点数（11）和点之间的时间间隔（0.01），随后是对应于序列值 x0, x1, ... x10 的 11 个值：

```
11 0.01
1 2 1 1 1 5 4 2 1 1 1
```

如果短时功率测量使用两个样本，长时功率测量使用五个测量值，那么我们可以从窗口中最右侧的点开始计算功率比：

```
1   2   1   [1   1]   5   4   2   1   1   1
short window
long window
```

点 x4：短时功率 = (1 + 1)/2 = 1，长时功率 = (1 + 1 + 1 + 4 + 1)/5 = 1.6，比率 = 1/1.6 = 0.63。

```
1   2   1   1   [1   5]   4   2   1   1   1
short window
long window
```

点 x5：短时功率 = (25 + 1)/2 = 13，长时功率 = (25 + 1 + 1 + 1 + 4)/5 = 6.4，比率 = 13/6.4 = 2.03。

```
1   2   1   1   1   [5   4]   2   1   1   1
short window
long window
```

点 x6：短时功率 = (16 + 25)/2 = 20.5，长时功率 = (16 + 25 + 1 + 1 + 1)/5 = 8.8，比率 = 20.5/8.8 = 2.33。

```
1   2   1   1   1   5   [4   2]   1   1   1
short window
long window
```

点 x7：短时功率 = (4 + 16)/2 = 10，长时功率 = (4 + 16 + 25 + 1 + 1)/5 = 9.4，比率 = 10/9.4 = 1.06。

```
1 2 1 1 1 5 4 2 1 1 1
          short window
long window
```

点 x8：短时功率 = (1 + 4)/2 = 2.5。
长时功率 = (1 + 25 + 16 + 4 + 1)/5 = 9.4，
比率 = 2.5/9.4 = 0.27。

```
1 2 1 1 1 5 4 2 1 1 1
              short window
long window
```

点 x9：短时功率 = (1 + 1)/2 = 1，
长时功率 = (1 + 1 + 4 + 16 + 25)/5 = 9.4，
比率 = 1/9.4 = 0.11。

```
1 2 1 1 1 5 4 2 1 1 1
                    short window
long window
```

点 x10：短时功率 = (1 + 1)/2 = 1，
长时功率 = (1 + 1 + 1 + 4 + 16)/5 = 4.6，
比率 = 1/4.6 = 0.22。

使用先前计算的比率，可能的地震事件发生在点 x5 和 x6。由于点之间的时间间隔为0.01秒，与地震事件对应的时间为0.05秒和0.06秒。（我们假设文件中的第一个点发生在0.0秒。）

### 4. 算法开发

我们首先开发分解大纲，因为它将解决方案分为一系列顺序步骤：

### 分解大纲

- 1. 从数据文件读取地震数据，并从键盘读取功率测量数量。
- 2. 计算功率比并打印可能的地震事件时间。

步骤1涉及读取数据文件并将信息存储在数组中。由于我们不知道数组的确切大小，需要在数组定义中指定最大大小。我们将从键盘读取功率计算的测量数量。步骤2涉及计算功率比并将其与阈值进行比较，以确定是否发生了可能的事件。由于我们需要为每个可能的事件位置计算两个功率测量值，我们将功率测量实现为一个函数。现在可以开发主函数和功率函数的伪代码细化：

```
Refinement in Pseudocode
main:
    set threshold to 1.5
    read npts and time-interval
    read the values into sensor array
    read short-window, long-window from keyboard
    set k to long-window - 1
    while k <= npts-1
        set short-power to power(sensor,short-window,k)
        set long-power to power(sensor,long-window,k)
        set ratio to short-power/long-power
        if ratio > threshold
            print k : time-interval
        increment k by 1
power(x,length,n):
    set xsquare to zero
    set k to n
    while k >= n-length+1
        add x[k] * x[k] to xsquare
    return xsquare/length
```

我们现在准备将伪代码转换为C。

```
/*----------------------------------------------------------*/
/* Program chapter6_5                                      */
/*                                                          */
/* This program reads a seismic data file and then          */
/* determines the times of possible seismic events.         */
/*----------------------------------------------------------*/
#include <stdio.h>
#define FILENAME "seismic1.txt"
#define MAX_SIZE 1000
#define THRESHOLD 1.5
int main(void)
{
    /* Declare variables and function prototypes. */
    int k, npts, short_window, long_window;
    double sensor[MAX_SIZE], time_incr, short_power,
           long_power, ratio;
    FILE *file_ptr;
    double power_w(double *ptr, int n);
    /* Read sensor data file. */
    file_ptr = fopen(FILENAME,"r");
    if (file_ptr == NULL)
        printf("Error opening input file. \n");
    else
    {
        fscanf(file_ptr,"%d %lf",&npts,&time_incr);
        if (npts > MAX_SIZE)
            printf("Data file too large for array. \n");
        else
        {
            /* Read data into an array. */
            for (k=0; k<npts-1; k++)
                fscanf(file_ptr,"%lf",&sensor[k]);

            /* Read window sizes from the keyboard. */
            printf("Enter number of points for short window: \n");
            scanf("%d",&short_window);
            printf("Enter number of points for long window: \n");
            scanf("%d",&long_window);

            /* Compute power ratios and search for events. */
            for (k=long_window-1; k<npts-1; k++)
            {
                short_power = power_w(&sensor[k],short_window);
                long_power = power_w(&sensor[k],long_window);
                ratio = short_power/long_power;
                if (ratio > THRESHOLD)
                    printf("Possible event at %f seconds \n",
                           time_incr*k);
            }
            /* Close file. */
            fclose(file_ptr);
        }
    }
    /* Exit program. */
    return 0;
}

/*--------------------------------------------------------------*/
/* This function computes the average power in a specified */
/* window of a double array. */
/*--------------------------------------------------------------*/
double power_w(double *ptr, int n)
{
    /* Declare and initialize variables. */
    int k;
    double xsquare=0;

    /* Compute sum of values squared in the array x. */
    for (k=0; k<=n-1; k++)
        xsquare += *(ptr+k)*(*(ptr+k));

    /* Return the average squared value. */
    return xsquare/n;
}
