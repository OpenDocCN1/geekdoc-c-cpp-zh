

如果在指定数组时未指定大小，但指定了初始化序列，则大小定义为等于序列中的值的数量，如下所示：

```cpp
int s[]={5,0,-1,2,15,2};
double t[]={0.0,0.1,0.2,0.3};
```

数组的大小必须在声明语句中通过使用方括号内的常量或花括号内的初始化序列来指定。

数组也可以用程序语句进行初始化。例如，假设我们想要用值 0.0、0.5、1.0、1.5、...、10.0 填充一个 double 类型的数组 g。由于有 21 个值，在声明语句中列出这些值会很繁琐。因此，我们使用以下语句来定义和初始化此数组：

```cpp
/* Declare variables. */
int k;
double g[21];

...

/* Initialize the array g. */
for (k=0; k<20; k++)
    g[k] = k*0.5;
```

重要的是要认识到，此 for 语句中的条件必须指定最终下标值为 20，而不是 21，因为数组元素是 g[0] 到 g[20]。指定比最大有效下标多一个值的下标是常见的错误，此错误很难找到，因为它访问了数组外部的值。访问数组外部的值可能会产生执行错误，例如 "segmentation fault" 或 "bus error"。更常见的是，此错误在程序执行期间不会被检测到，但会导致不可预测的程序结果，因为您的程序修改了数组外部的内存位置。要小心不要超过数组下标。在我们的程序中，我们在 for 循环中选择专门使用最终值的条件，以提醒自己仔细编写条件以避免错误。因此，在此示例中，我们使用条件 k<20 而不是 k<21，尽管两者都能正常工作。另外，我们通常将 k 用作一维数组的下标。

数组常用于存储从数据文件读取的信息。例如，假设我们有一个名为 sensor3.txt 的数据文件，其中包含从地震仪收集的 10 个时间和运动测量值。要将这些值读入名为 time 和 motion 的数组，我们可以使用以下语句：

```cpp
/* Declare variables. */
int k;
double time[10], motion[10];
FILE *sensor;

...

/* Open file and read data into arrays. */
sensor = fopen("sensor3.txt","r");
for (k=0; k<9; k++)
    fscanf(sensor,"%lf %lf",&time[k],&motion[k]);
```

## 练习！

显示以下各组语句中定义的数组的内容：

- 1. int x[10]={-5,4,3};
- 2. char letters[]={'a','b','c'};
- 3. double z[4];
  ...
  z[1] = -5.5;
  z[2] = z[3] = fabs(z[1]);
- 4. int k;
  double time[9];
  ...
  for (k=0; k<8; k++)
  time[k] = (k-4)*0.1;

## 计算与输出

对数组元素的计算与对简单变量的计算方式相同，但必须使用下标来指定单个数组元素。为例示，以下程序从数据文件读取包含 100 个浮点值的数组 y，确定数组的平均值，然后将其存储在 y_ave 中。然后，程序将确定数组 y 中大于平均值的值的数量，对其进行计数并打印计数。如果此程序的目的是确定数据文件中值的平均值，则不需要数组。读取值的循环可以将每个值读入同一个变量，并在读取下一个值之前将其值加到总和中。但是，因为我们需要将每个值与平均值进行比较，以计算大于平均值的值的数量，所以需要数组来再次访问每个值。

```cpp
/*-----------------------------------------------*/
/* Program chapter5_1                            */
/*                                               */
/* This program reads 100 values from a data file and */
/* determines the number of values greater than the average. */
/*                                               */

#include <stdio.h>
#define N 100
#define FILENAME "lab1.txt"

int main(void)
{
   /* Declare and initialize variables.  */
   int k, count=0;
   double y[N], y_ave, sum=0;
   FILE *lab;

/* Open file, read data into an array, */
/* and compute a sum of the values. */
lab = fopen(FILENAME,"r");
if (lab == NULL)
printf("Error opening input file. \n");
else
{
/* Input and process data. */
for (k=0; k<=N-1; k++)
{
fscanf(lab,"%f",&y[k]);
sum += y[k];
}
/* Compute average and count values that */
/* are greater than the average. */
y_ave = sum/N;
for (k=0; k<=N-1; k++)
if (y[k] > y_ave)
count++;
/* Print count and close file. */
printf("%d values greater than the average \n",count);
fclose(lab);
}
/* Exit program. */
return 0;
}
/* ... */
```

打印数组值时使用下标来指定所需的单个值。例如，要打印前一个示例中数组 y 的第一个值和最后一个值，我们将使用以下语句：

```cpp
printf("first and last array values: \n");
printf("%f %f \n",y[0],y[N-1]);
```

要打印 y 的所有 100 个值，每行一个，我们使用以下循环：

```cpp
printf("y values: \n");
for (k=0; k<=N-1; k++)
printf("%f \n",y[k]);
```

在打印大型数组（如本例）时，我们可能希望在同一行上打印多个数字。要在打印每组五个值之前跳到新行，我们将使用以下语句：

```cpp
printf("y values: \n");
for (k=0; k<=N-1; k++)
    if (k%5 == 0)
        printf("\n %f ", y[k]);
    else
        printf("%f ", y[k]);
printf("\n");
```

类似的语句也可用于将数组值写入数据文件。例如，要使用文件指针 sensor 将 y[k] 的值打印到数据文件的一行上，我们使用以下语句：

```cpp
fprintf(sensor, "%f \n", y[k]);
```

由于包含了换行符指示符，下一个写入文件的值将位于新行上。

数组中的元素数量用于数组声明，并用于循环中以访问数组中的元素。如果元素数量发生更改，则程序中有几个位置需要修改。如果使用符号常量来指定数组的大小，则更改数组大小会简化。要更改大小，只需更改预处理器指令。这种编码建议在包含许多模块的程序中，或在多个程序员正在同一软件项目上工作的编程环境中尤其重要。以下许多程序说明了使用符号常量来定义数组大小。

表 5.1 给出了包含下标括号的更新优先级顺序。括号和圆括号在其他运算符之前结合。如果圆括号和括号在同一语句中，则从左到右结合；如果它们是嵌套的，则最内层集首先求值。

## 练习！

假设变量 k 和数组 s 已使用以下语句定义：

```cpp
int k, s[]={3,8,15,21,30,41};
```

使用手动计算，确定以下各组语句的输出：

- 1. for (k=0; k<=5; k+=2)
    printf("%d %d \n", s[k], s[k+1]);

- 2. for (k=0; k<=5; k++)
    if (s[k]%2 == 0)
        printf("%d ", s[k]);
    printf("\n");

## 函数参数

当将数组中的信息传递给函数时，通常使用两个参数；一个参数指定特定数组，另一个参数指定数组中使用的元素数量。通过指定数组的元素数量，函数变得更加灵活。例如，如果函数指定一个整数数组，则该函数可以与任何整数数组一起使用；指定元素数量的参数确保我们使用正确的大小。另外，数组中使用的元素数量可能会不同时间而异。例如，数组可能使用从数据文件读取的元素；the

