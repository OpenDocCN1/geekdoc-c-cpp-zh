
## 示例

0100 1001（十进制数 73）  
将上述二进制数左移 4 位，得到数字  
1001 0000（十进制数 144）

## 右移

在表达式 `n >> d` 中，数字 *n* 向右移动 *d* 位。向右移位时，最右边的位将丢失，并在左侧填充 0。

### 示例

0100 1001（十进制数 73）  
将上述二进制数右移 4 位，得到数字  
0000 0100（十进制数 4）

## 4 位字长的右旋转

将以下数字 13 右旋转 1 位  
13 的二进制形式为：1101

![](img/dad8bddd927fabdab2417ecbf1eb24eb_110_0.png)

右旋转 1 位后

![](img/dad8bddd927fabdab2417ecbf1eb24eb_110_1.png)

## 右旋转的主要逻辑

- 1. 将数字右移 *n* 位
- 2. 将数字左移 32 - *n* 位
- 3. 对上述结果进行按位或

## 算法

开始

- **步骤 1：** 读取一个数字 *x*
- **步骤 2：** 读取要旋转的位数 *n*
- **步骤 3：** 调用 `rightrot` 函数  
  `result ← rightrot(x, n)`
- **步骤 4：** 打印结果

停止

## 将 x 旋转 n 位的算法

开始

- **步骤 1：** 将 *x* 右旋转 *n* 位  
  `a ← x >> n;`  
  `b ← x << (32 - n); /* assuming 32-bit machine */`
- **步骤 2：** 返回 `(a | b)`

停止

## 程序

```c
#include<stdio.h>
unsigned int rightrot(int, int); /* prototype declaration */
void main()
{
    int x, n;
    unsigned int result;
    printf("Enter the number to be right rotated \n");
    scanf("%d",&x);
    printf("Enter the number of bits to be right rotated \n");
    scanf("%d",&n);
    result=rightrot(x,n); /* call to function rightrot(x,n) */
    printf("The number %d after right rotation by %d bit positions is %u",x,n,result);
}

unsigned int rightrot(int x, int n)
{
    unsigned int a,b;
    a=x >> n;       /* right shift by n bits */
    b=x << (32-n);      /* left shift by 32-n bits */
    return (a | b);        /* bitwise OR a and b */
}
```

### 示例输出 1

```text
Enter the number to be right rotated
8
Enter the number of bits to be right rotated
2
The number 8 after right rotation by 2-bit positions is 2
```

### 结论

数字 8 的 32 位二进制形式表示为

```text
0000 0000   0000 0000   0000 0000   0000 1000
After rotating 2 bits
0000 0000   0000 0000   0000 0000   0000 0010
```

### 示例输出 2

```text
Enter the number to be right rotated
9
Enter the number of bits to be right rotated
31
The number 9 after right rotation by 31-bit positions is 18
```

### 结论

数字 9 的 32 位二进制形式表示为

```text
0000 0000    0000 0000    0000 0000    0000 1001
After rotating 31 bits
0000 0000    0000 0000    0000 0000    0001 0010
```

### 示例输出 3

```text
Enter the number to be right rotated
16
Enter the number of bits to be right rotated
5
The number 16 after right rotation by 5-bit positions is
2147483648
```

### 学习成果

- 能够处理函数和参数传递。
- 能够识别旋转函数的重要性并找到可能的应用。

## 学期作业 13

### 问题定义

设计并开发一个函数 `isprime(x)`，它接受一个整数参数，如果该参数是素数则返回 1，否则返回 0。该函数将使用简单的除法检查方法来确定给定数字是否为素数。在 main 中根据用户输入的不同值调用此函数，并打印适当的消息。

### 目标

- 能够将寻找素数的纸笔方法映射为算法，然后编写 C 代码。
- 理解函数的用法。
- 理解如何优化逻辑进而优化处理时间。

### 相关理论

### 素数

只能被 1 和自身整除的数称为素数。例如 2、3、5、7、11 等不能被除 1 和自身以外的任何数整除，因此它们都是素数。但 4、6、8、16 等数可以被 2 整除，因此它们是非素数。

### 程序逻辑

现在让我们看看如何检查一个数是否为素数。

- 考虑数字 16，它不能被 9、10、11、12、13、14 整除——这些数都大于 16/2。但 16 能被 2、4、8 整除，而这些数小于或等于 16/2。
- 因此要记住的第一点是：一个数 $n$ 不能被大于 $n/2$ 的数整除。
- 因此，要检查给定数字 $n$ 是否为素数，只需用 2、3、4、5、…、$n/2$ 去除 $n$ 即可。

### 算法

```text
Step 1: [Start of algorithm]
Step 2: [Read the value of n]
    Read n
Step 3: [Check for validation]
    Check n = 0 or n = 1 then
    print n is neither prime nor composite goto step 6
Step 4: [Call the function]
    j = isprime(n)
Step 5: Check j = 1 then
    print the number n is prime
        otherwise print the number n is not prime
Step 6: [End of Algorithm]
    Stop
```

### 被调用函数 `int isprime(int x)` 的算法

```text
Step 4.1: Repeat for i = 2 to x/2
        check x % i = 0 then
            return 0
            otherwise
                continue next i
Step 4.2: Return 1
```

### 流程图

![](img/dad8bddd927fabdab2417ecbf1eb24eb_117_0.png)

### 函数的流程图

![](img/dad8bddd927fabdab2417ecbf1eb24eb_118_0.png)

### 程序

```c
#include<stdio.h>
#include<process.h>
void main()
{
    int j,n;
    int isprime(int x);  /* Function prototype */
    printf("Enter the number:\n");
    scanf("%d",&n);
    if(n==0||n==1)
    {
        printf("The number %d is neither prime nor composite\n",n);
        exit(0);
    }
    j = isprime(n);
    if(j==1)
        printf("The given number is prime\n");
    else
        printf("Number is not prime\n");
}

// Function to check whether the given value is prime or not

int isprime(int x)  /* Function definition */
{
    int i;  /* Local declaration */
    for(i=2;i<=x/2;i++)
    {
        if(x%i==0)
        {
            return 0;  /* Number is not a prime */
        }
    }
    return 1;  /* Number is prime */
}
```

### 示例输出

- 1. 输入数字：  
  7  
  给定的数是素数
- 2. 输入数字：  
  10  
  给定的数不是素数
- 3. 输入数字：  
  16  
  给定的数不是素数
- 4. 输入数字：  
  0  
  数字 0 既不是素数也不是合数
- 5. 输入数字：  
  1  
  数字 1 既不是素数也不是合数

### 学习成果

- 能够处理函数和传递参数。
- 能够优化逻辑和代码。

## 学期作业 14

### 问题定义

设计、开发并执行一个 C 并行程序，利用埃拉托色尼筛法算法确定并打印小于 100 的素数。

### 目标

- 学习并行编程和函数的概念。
- 理解使用埃拉托色尼筛法算法寻找素数的底层逻辑，并为此编写程序。

### 编码前提条件

### OpenMP（Open Multi-Processing）

**OpenMP**（Open Multi-Processing）是一个 API（应用程序编程接口），在大多数处理器架构和操作系统上支持 C、C++ 和 Fortran 的多平台共享内存多处理编程，包括 Linux、Unix、AIX、Solaris、Mac OS X 和 Microsoft Windows 平台。它由一组影响运行时行为的编译器指令、库例程和环境变量组成。OpenMP 使用可移植、可扩展的模型，为程序员提供简单灵活的接口，用于开发从标准台式计算机到超级计算机等平台上的并行应用。

### 指令

- `#pragma omp parallel for`
- 并行构造形成一组线程并开始并行执行。
- `#pragma omp parallel for [clause[[,] clause] ...]` 换行
- for 循环

OpenMP 可执行指令应用于其后的结构化块或一个 OpenMP 构造。“结构化块”是顶部只有一个入口、底部只有一个出口的单个语句或复合语句。

