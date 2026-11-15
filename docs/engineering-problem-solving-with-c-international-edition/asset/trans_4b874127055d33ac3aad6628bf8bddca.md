

## 实践！

假设整型变量 sum 包含值 65，双精度变量 average 包含值 12.368，字符型变量 ch 包含值 'b'。显示以下语句生成的输出行（或多行）（使用 \n 表示空格）：

- 1. printf("Sum = %5i; Average = %7.1f \n", sum, average);
- 2. printf("Sum = %4i \n Average = %6.4f \n", sum, average);
- 3. printf("Sum and Average \n%\n %6.1f \n", sum, average);
- 4. printf("Character is %c; Sum is %c \n", ch, sum);
- 5. printf("Character is %i; Sum is %i \n", ch, sum);
- 6. printf("%7.2f is the average; \n", average);
   printf("%8d is the sum \n", sum);
- 7. printf("%7.2f is the average: ", average);
   printf("%8d is the sum \n", sum);

## scanf 函数

scanf 函数允许你在程序执行时从键盘输入值。例如，假设一个程序计算在指定时间过去后新增森林面积的英亩数。如果经过的时间是程序中的常量，我们就必须更改常量的值，然后重新编译和重新执行程序，才能获得不同时间段的输出。或者，如果我们使用 scanf 函数读取时间段，就不需要重新编译程序；我们只需重新执行它，并从键盘输入所需的时间段。

scanf 函数的第一个参数是控制字符串，用于指定要从键盘输入值的变量的类型。类型说明符如表 2.7 所示；因此，例如，整型变量的说明符为 %i 或 %d；说明符

| 变量类型 | 格式说明符 |
|---|---|
| | 整型值 |
| int | %i, %d |
| short | %hi, %hd |
| long int | %li, %ld |
| unsigned int | %u |
| unsigned short | %hu |
| unsigned long | %lu |
| | 浮点型值 |
| float | %f, %e, %E, %g, %G |
| double | %lf, %le, %lE, %lg, %lG |
| long double | %Lf, %Le, %LE, %Lg, %LG |
| | 字符型值 |
| char | %c |

对于 float 变量，说明符为 %f、%e 和 %g；对于 double 变量，说明符为 %lf、%le 和 %lg。使用正确的说明符非常重要。例如，如果使用 %i 说明符读取 double 变量的值，将会发生错误。scanf 函数的其余参数是与控制字符串中的说明符对应的内存位置。这些内存位置由地址运算符 & 指示。该运算符是一个一元运算符，用于确定与其关联的标识符的内存地址。因此，如果要通过键盘输入的值是一个整数，并要存储在变量 year 中，我们可以使用以下语句读取该值：

```
scanf("%i",&year);
```

地址运算符的优先级与其他一元运算符相同；如果同一语句中有多个一元运算符，它们从右到左结合。scanf 语句中常见的错误是为标识符省略地址运算符。

如果我们希望从键盘读取多个值，可以使用如下语句：

```
scanf("%i %c",&distance,&unit_length);
```

执行此语句时，程序将从键盘读取两个值，并将它们转换为一个整型值和一个字符型值。这些值必须至少用一个空格分隔；它们可以在同一行上，也可以在不同行上。为了提示程序用户输入这些值，scanf 语句通常前面有一个 printf 语句，用于描述用户应从键盘输入的信息：

```
printf("Enter the distance and the units (m for meters, f for " "feet): \n");
```

```
scanf("%i %c",&distance,&unit_length);
```

printf 语句的控制字符串以换行符说明符结尾，因此用户输入的值将出现在提示文本之后的行（或多行）上。因此，在执行前面的语句并且用户响应提示后，屏幕上的信息示例为

Enter the distance and the units (m for meters, f for feet): 10 m

如果用户输入的字符无法成功转换为 scanf 语句中转换说明符指示的值的类型，结果取决于系统。这些转换错误包括为整型值输入 14.2 这样的值、在大值中包含逗号以及忘记用空格分隔值。虽然 scanf 函数的主要目的是从键盘读取输入，但它还返回一个等于成功转换次数的值。该值在后续章节的程序中使用。

## 2.5 应用问题求解：根据骨骼长度估计身高

在本节中，我们使用本章介绍的新语句来解决与法医人类学相关的问题。还记得章节开头的讨论，骨骼遗骸可用于确定一个人身份的信息。我们现在考虑根据骨骼长度估计成年人的身高。

成年骨骼通常包含 206 块骨骼，从最长的骨骼（股骨，髋关节和膝关节之间的腿骨）到中耳中最小的骨骼（锤骨、砧骨和镫骨）。仅手部就包含 54 块骨骼。常用于估计身高的骨骼包括股骨、胫骨（连接膝盖和脚踝的两块骨骼中较大的一块）和肱骨（连接肩膀和手肘）。骨骼由韧带、肌腱、肌肉和软骨支撑，它们共同为心脏、肺和大脑等身体器官提供保护。骨骼约占体重的三分之一。

股骨是人体中最长的骨骼。其长度可用于估计人的身高；身高也可通过肱骨来估计。有多种不同的方程可用于根据骨骼长度估计成年人的身高。这些方程通常是通过对已知身高人群的骨骼进行大量测量，然后找到数据的最小二乘线性模型得出的。（此技术在下一章中详细描述。）许多此类方程专门针对男性或女性得出。我们将用于此问题的方程如下，其中骨骼长度以英寸为单位：

- 根据股骨长度估计身高：
  - 女性身高 = 股骨长度 × 1.94 + 28.7
  - 男性身高 = 股骨长度 × 1.88 + 32
- 根据肱骨长度估计身高：
  - 女性身高 = 肱骨长度 × 2.8 + 28.2
  - 男性身高 = 肱骨长度 × 2.9 + 27.9

编写一个 C 程序，提示用户输入同一人的股骨长度和肱骨长度。程序将根据每根骨骼分别计算男性和女性的身高，并打印这些值。

### I. 问题描述

根据股骨长度和肱骨长度估计人的身高。

### 2. 输入/输出描述

下图显示，程序的输入是两根骨骼的长度，输出是根据每个输入确定的身高。因为我们不知道骨骼来自男性还是女性，因此我们将计算两种身高估计值。

![](img/02c4582f051c5b51776411c92b079035_71_0.png)

### 3. 手算示例

假设股骨长度为 15 英寸，肱骨长度为 12 英寸。那么身高估计值为：

femur_height_female = femur_length × 1.94 + 28.7 = 57.8 in = 4.82 ft = 4 ft 9.8 in
femur_height_male = femur_length × 1.88 + 32 = 60.2 in = 5.02 ft = 5 ft 0.24 in
humerus_height_female = humerus_length × 2.8 + 28.2 = 61.8 in = 5.15 ft = 5 ft 1.8 in
humerus_height_male = humerus_length × 2.9 + 27.9 = 62.7 in = 5.23 ft = 5 ft 2.76 in

### 4. 算法开发

算法开发的第一步是将问题求解分解为一组按顺序执行的步骤。

### 分解大纲

- 1. 读取股骨和肱骨的长度。
- 2. 计算身高估计值。
- 3. 打印身高估计值。

该程序结构简单，因此可以直接将分解转换为 C 语言。

```
/*
 * Program chapter2_2
 *
 * This program estimates a person's height from the length
 * of the femur and from the length of the humerus.
 */
#include <stdio.h>
#include <math.h>

int main(void)
{
   /* Declare variables.  */
   double femur, femur_ht_f, femur_ht_m, humerus, humerus_ht_f,
          humerus_ht_m;

   /* Get user input from the keyboard.  */
   printf("Enter Values in Inches. \n");
   printf("Enter femur length:  \n");
   scanf("%lf",&femur);
   printf("Enter humerus length:  \n");
   scanf("%lf",&humerus);

   /* Compute height estimates.  */
   femur_ht_f = femur*1.94 + 28.7;
   femur_ht_m = femur*1.88 + 32;
   humerus_ht_f = humerus*2.8 + 28.2;
   humerus_ht_m = humerus*2.9 + 27.9;
```

