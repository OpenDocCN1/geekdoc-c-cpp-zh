

## 使用循环访问数组元素的示例：

```
#define NUMLABS 10

int main(void)
{
 int i;
 float labScores[NUMLABS];

 for(i = 0; i < NUMLABS; i++)
 {
   printf("Enter lab #%d score -> ", i + 1);
   scanf("%f", &labScores[i]);
 }

 //PROCESS DATA
 for(i = 0; i < NUMLABS; i++)
 {
   printf("Lab #%d score: %.2f\n", i + 1, labScores[i]);
 }

 return(0);
}
```

## 索引范围检查

大小为 NUMLABS 的数组的有效索引值范围是 0 到 NUMLABS 减 1。如果在程序执行期间尝试访问此范围之外的索引，会发生什么情况？

例如，如果我们尝试访问 labScores[10]，而对于声明大小为 10 的数组，唯一有效的索引值是 0 - 9，会怎样？这里描述的场景意味着这个潜在问题是一个运行时错误。编译器不会，也无法，检测索引范围检查问题。

由于这是一个运行时错误，它可能有多种不同形式。尝试访问数组边界之外的索引可能会产生哪些后果？

| 可能的观察结果 | 可能发生此情况的原因 |
| :--- | :--- |
| 没有问题，程序按预期工作。 | 超出数组限制并进入未为数组目的保留的内存，可能未为任何其他目的保留。 |
| 程序执行，但结果不符合预期。 | 超出数组限制并进入未为数组目的保留的内存，可能为任何其他目的保留，并且对同一内存的多次编辑可能会留下存储了意外值。 |
| 程序崩溃。 | 超出数组限制并尝试访问不存在或程序无权访问的内存。 |

## 超出数组定义限制的示例

```
int x[5] = {8, 4, 5, 2, 3};
```

| | 8 | 4 | 5 | 2 | 3 |
|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | |

| | 8 | 4 | 5 | 2 | 3 |
|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | |

| | 8 | 4 | 5 | 2 | 3 |
|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | |

## 数组与函数（函数间通信）

- 如果数组仅限于声明它们的函数内使用，那么它们对我们来说用途有限。与用户定义的函数共享数组数据有两种方法，我们可以**发送一个元素**，或者**多个元素**，或者**整个数组**。

### 在每种方法中，我们必须了解以下内容：

- 函数声明、函数调用和函数定义在语法上如何变化。
- 传递的值是**按值传递**还是**按地址传递**，以及是否可以使用非默认方法。

### 传递单个元素

您可以像传递任何其他变量一样将单个元素传递给函数，只要数组元素类型与函数参数类型匹配，就可以成功地将其传递给函数。

```
#define SIZE 5

int calcFactorial(int);

int main(void)
{
 int num = 8;
 int data[SIZE] = {2, 4, 6, 3, 5};

 printf("Result: %d\n", calcFactorial(num));

 printf("Result: %d\n", calcFactorial(data[2]));

 return(0);
}

int calcFactorial(int x)
{
 int xFact = 1;

 while(x > 1)
 {
 xFact *= x--;
 }

 return(xFact);
}
```

### 示例：给定一个已初始化的整数数组，打印数组中每个整数的平方。

```
#define ARRAYSIZE 5
void print_square(int);
int main(void)
{
   int lcv;
   int base[ARRAYSIZE] = {3, 7, 2, 4, 5};
   for(lcv = 0; lcv < ARRAYSIZE; lcv++)
   {
      print_square(base[lcv]);
   }
   printf("\n");
   return(0);
}
void print_square(int x)
{
   printf("%d squared = %d\n", x, x * x);
}
```

- 从前面的程序中观察到：
  - 将数组的单个元素传递给函数时，必须指定数组名称，后跟在 [ ] 大括号中传递的值的特定索引。

### 按值传递回顾

- 回顾一下，如果我们将单个变量传递给函数，传递的只是变量值的副本，因此对该副本的更改不会改变调用函数中的变量。
- 数组的单个元素如何传递给函数？接下来的第一个示例演示了第 4 章中展示的按值传递技术。第二个示例试图演示数组的单个元素是按值传递还是按地址传递。
  - 如果在最后的打印语句中 x[1] 应为 24，那么我们将得出该元素是按值传递的结论。
  - 如果在最后的打印语句中 x[1] 应为 3，那么我们将得出该元素是按地址传递的结论。

```
void passTest(int);
int main(void)
{
    int x = 32;
    printf("Before x = %d\n", x);
    passTest(x);
    printf("After x = %d\n", x);
    return(0);
}
```

```
void passTest(int);
int main(void)
{
    int x[3] = {16, 24, 32};
    printf("Before x[1] = %d\n", x[1]);
    passTest(x[1]);
    printf("After x[1] = %d\n", x[1]);
    return(0);
}
```

```
void passTest(int g)
{
    printf("Before g = %d\n", g);
    g = g / 8;
    printf("After g = %d\n", g);
}
```

```
void passTest(int g)
{
    printf("Before g = %d\n", g);
    g = g / 8;
    printf("After g = %d\n", g);
}
```

### 上面程序的输出：

从输出可以看出，数组的单个元素被视为传递给函数的单个变量，也就是说，数组的单个元素是按值传递的。

- 是否可以对数组的单个元素使用按地址传递？

### 示例：按地址传递 x[1] 元素。

```
#include <stdio.h>
void passTest(int*);
int main(void)
{
 int x[3] = {16, 24, 32};
 printf("Before x[1] = %d\n", x[1]);
 passTest(&x[1]);
 printf("After x[1] = %d\n", x[1]);
 return(0);
}
void passTest(int *g)
{
 printf("Before g = %d\n", *g);
 *g = *g / 8;
 printf("After g = %d\n", *g);
}
```

### 示例：通过将两个元素都按地址传递给函数来交换数组的两个元素。

```
#define SIZE 10
void swapValues(int*, int*);
int main(void)
{
 int x[SIZE] = {3, 4, 5, 1, 2, 9, 8, 7, 6, 0};
 printf("x[4] = %d x[5] = %d\n", x[4], x[5]);
 swapValues(&x[4], &x[5]);
 printf("x[4] = %d x[5] = %d\n", x[4], x[5]);
 return(0);
}
void swapValues(int *ax, int *ay)
{
 int temp;
 temp = *ax;
 *ax = *ay;
 *ay = temp;
}
```

### 传递整个数组

- 如果我们有一个大小为 10 的数组，需要将所有 10 个元素传递给函数，该怎么办？

### 选项 #1，传递每个元素

```
void fun(int, int, int, int, int, int, int, int, int, int);
```

### 选项 #2，传递整个数组

```
void fun(int[]);
```

在语法方面还有更多内容，最终结果可能会让人感到惊讶，关于我们对所使用传递技术的结论。

| 代码 | 说明 |
|------|-------------|
| #include <stdio.h><br>void passTest(int[]);<br>int main(void)<br>{<br> int x[3] = {16, 24, 32};<br> printf("Before x[1] = %d\n", x[1]);<br> passTest(x);<br> printf("After x[1] = %d\n", x[1]);<br> return(0);<br>}<br>void passTest(int y[])<br>{<br> printf("Before y[1] = %d\n", y[1]);<br> y[1] = y[1] / 8;<br> printf("After y[1] = %d\n", y[1]);<br>} | 当将整个数组传递给函数时，您只需列出数组的名称。<br><br>**请勿包含以下任何内容：**<br><br>* 函数声明和定义中看到的方括号。<br>* 数组声明中使用的数组大小。<br>* 数组的数据类型。我们在函数调用中何时列出过参数的类型？<br><br>**左侧程序的输出：**<br><br>**结论 – 整个数组是按地址传递的。** |

- **注释：**
  - 请考虑这一点；如果数组按值传递，则需要完整复制存储数组副本所需的内存。这将是内存使用效率非常低的做法。与传递数组副本相比，语言传递数组的地址。**是否有可能按值传递整个数组？** 不可能。
  - 用户定义的函数调用中没有第 4 章中的 `&` 运算符？**数组名称已经引用内存地址！**
  - **数组名称代表哪个内存地址？** 数组只跟踪它们在内存中的起始位置，而不跟踪结束位置！
  - **索引值代表什么？** 提供的索引值将与数组名称代表的地址相加，以定位数组内所需的元素。索引本质上充当数组在计算机内存中起始位置的偏移量。

