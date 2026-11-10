

```
result1 = fpointer(4, 5);
result2 = fpointer(6, 2);
```

下面的程序说明了上述事实。

### 示例

```c
33. int (*fpointer)(int, int);

/* Define a pointer to a function */
int add(int, int);    /* Define a few functions. */
int sub(int, int);
int main()
{
    fpointer = add;
        /* Put the address of 'add' in 'fpointer' */
    printf("%d \n", fpointer(4, 5));
            /* Execute 'add' and print results */
    fpointer = sub;        /* Repeat for 'sub' */
    printf("%d \n", fpointer(6, 2));
    return 0;
}
int add(int a, int b)
{
    return(a + b);
}
int sub(int a, int b)
{
    return(a - b);
}
```

## 13.16.4 将函数传递给另一个函数

函数指针可以作为函数的调用参数进行传递。下面的代码展示了如何传递一个指向函数的指针，该函数返回 `double` 类型并接受两个 `double` 类型参数。假设某个计算可以由不同的函数来完成。考虑

$$\sum_{k=m}^{n} f(k)$$

其中，在一种情况下 f(K) = xᵏ/K!，在另一种情况下 f(K) = 1/xᵏ。

f(K) = xᵏ/K! 可以如下实现。

```c
double exp_term(double b, double x)
{
    return(pow(x,b)/fact(b));
}
double fact(double a)
{
    double f=1.0;
    for(;a>0;a--)
        f*=a;
    return f;
}
```

f(K) = 1/xᵏ 可以如下实现。

```c
double by_term(double b, double x)
{
    return(1/pow(x,b));
}
```

```c
double sum(double f(double,double), int m, int n)
{
    int K;
    double s = 0.0;
    double x;
    printf("\n ENTER THE VALUE OF x");
    scanf("%lf",&x);
    for(K=m; K<=n; ++K)
        s+=f(K,x);
    return s;
}
```

现在，求和函数可以如下实现。

当函数作为参数出现时，编译器会将其解释为指针。以下是该函数的等价声明。

```c
double sum(double (*f)(double), int m, int n)
{
    ... same as above
}
```

这里，`double (*f)(double)` 是一个指向函数的指针，该函数接受一个 `double` 类型的参数并返回一个 `double` 类型的值。

括号非常重要，因为 `()` 比 `*` 结合得更紧密。如果参数写成 `double *f(double)` 而不是 `double (*f)(double)`，那么这表示 f 是一个函数，它接受一个 `double` 类型的参数并返回一个指向 `double` 的指针。

在 `sum` 函数体内，语句

`s += f(K)`

可以替换为

`s += (*f)(K)`

这里显式地解引用了函数指针。

这里，

f 表示指向函数的指针。

*f 表示函数本身。

(*f)(K) 是对该函数的调用。

图 13.15 描述了函数指针表示法中每个部分的含义。

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_385_0.png)

图 13.15 函数指针表示法的含义

现在，这些函数的原型应该是什么样的？这里使用的相应函数的原型如下：

- `double by_term(double);` (i)
- `double exp_term(double);` (ii)
- `double fact(double);` (iii)
- `double sum(double (*f)(double), int, int);` (iv)

对于将函数作为形式参数的函数原型 (iv)，有几种等价的原型声明：

- `double sum(double (*)(double), int, int);`
- `double sum(double f(double), int, int);`
- `double sum(double f(double x), int m, int n);`

现在，考虑 `sum()` 函数的调用语句。

```c
int main()
{
    printf("\n SUM OF COMPUTATION 1: %lf:",
           sum(exp_term,0,3));

    printf("\n SUM OF COMPUTATION 2: %lf",
           sum(by_term,0,4));

    return 0;
}
```

`sum(exp_term, 0, 4)` 计算以下级数的和。

$$s = \frac{x^0}{0!}+\frac{x^1}{1!}+\frac{x^2}{2!}+\frac{x^3}{3!}+\frac{x^4}{4!} = 1+x+\frac{x^2}{2!}+\frac{x^3}{3!}+\frac{x^4}{4!}$$

`sum(by_term, 0, 4)` 计算以下级数的和。

$$s = \frac{1}{x^0}+\frac{1}{x^1}+\frac{1}{x^2}+\frac{1}{x^3}+\frac{1}{x^4} = 1+\frac{1}{x}+\frac{1}{x^2}+\frac{1}{x^3}+\frac{1}{x^4}$$

以下是完整的程序。

### 示例

```c
34. #include <stdio.h>
#include <math.h>
double fact(double a)
{
    double f=1.0;
    for(;a>0;a--)
        f*=a;
    return f;
}
double exp_term(double b, double x)
{
    return(pow(x,b)/fact(b));
}
double by_term(double b, double x)
{
    return(1/pow(x,b));
}
double sum(double f(double,double), int m, int n)
{
    int k;
    double s = 0.0;
    double x;
    printf("\n ENTER THE VALUE OF X ");
    scanf("%lf",&x);
    for(k=m; k<=n; ++k)
        s+=f(k,x);
    return s;
}
int main()
{
    printf("\n SUM OF COMPUTATION 1: %lf:",
           sum(exp_term,0,3));

    printf("\n SUM OF COMPUTATION 2: %lf",
           sum(by_term,0,4));
    return 0;
}
```

### 输出

```
ENTER THE VALUE OF X 2
SUM OF COMPUTATION 1: 6.333333
ENTER THE VALUE OF X 2
SUM OF COMPUTATION 2: 1.937500
```

## 13.16.5 如何返回函数指针

返回函数指针有点棘手，但函数指针可以作为函数的返回值。在下面的示例中，有两种返回函数指针的方法，该函数接受两个 `float` 参数并返回一个 `float`。如果有人想要返回一个指向函数的指针，所需要做的只是修改所有函数指针的定义/声明。

```c
float Add(float a, float b) { return a+b; }
float Sub(float a, float b) { return a-b; }
```

`Add` 和 `Sub` 已经定义。它们返回一个 `float`，并接受两个 `float` 值。该函数接受一个 `char`，并返回一个指向函数的指针，该函数接受两个 `float` 并返回一个 `float`。`<opCode>` 指定要返回哪个函数。

```c
float(*GetPtr1(char opCode))(float, float)
{
    if(opCode == '+') return &Add;
    if(opCode == '-') return &Sub;
}
```

使用 `typedef` 的解决方案定义了一个指向函数的指针，该函数接受两个 `float` 值并返回一个 `float`。

```c
typedef float(*ptr2Func)(float, float);
```

- (ii) `calloc()` 的工作方式类似于 `malloc`，但会在可能的情况下将内存初始化为零。其原型为

  `void * calloc(size_t count, size_t eltsize)`

  该函数分配一块足够大的内存，以容纳由 `count` 个元素组成的数组，每个元素的大小为 `eltsize`。在 `calloc` 返回之前，其内容会被清零。

- (iii) `void free(void* block)` `free()` 接受一个指向先前由 `malloc()` 分配的堆块的指针，并将该块返回给堆以供重用。在 `free()` 之后，调用方不应访问该块的任何部分，也不应假定该块是有效内存。该块不应被第二次释放。

- (iv) `void* realloc(void* block, size_t size)` 接受一个现有的堆块，并尝试将其重新分配为指定大小的堆块，该大小可能大于或小于原始块的大小。它返回指向新块的指针，如果重新分配不成功，则返回 `NULL`。请务必捕获并检查 `realloc()` 的返回值。继续使用旧的块指针是一个常见错误。`realloc()` 会负责将字节从旧块移动到新块。`realloc()` 之所以存在，是因为可以使用底层特性来实现它，这比程序员能够编写的 C 代码更高效。

要使用这些函数，必须包含 `stdlib.h` 或 `alloc.h`，因为这些函数在这些头文件中声明。

## 注意

程序退出时，其所有内存都会自动释放。因此，只有在程序运行时回收内存很重要的情况下，程序才需要在执行期间使用 `free()`，通常是因为程序使用了大量内存或运行时间较长。传递给 `free()` 的指针必须是最初由 `malloc()` 或 `realloc()` 返回的同一个指针，而不仅仅是堆块中某个位置的指针。

让我们详细讨论这些函数及其用法。注意，如果没有足够的内存，`malloc` 会返回 `NULL`。由于 `malloc` 可能返回 `NULL` 而不是可用的指针，因此代码应始终检查 `malloc` 的返回值以判断其是否成功。如果调用失败，而程序解引用了由此产生的 `NULL` 指针，程序将会崩溃。带有错误检查的 `malloc` 调用通常如下所示：

```c
int *ip;
ip = (int *) malloc(sizeof(int));
if(ip == NULL)
{
    printf("out of memory\n");
    exit(0);        /* 'return' may be used */
}
```

**关于 `exit()`** 在前面的示例中，我们遇到了一种无法分配内存的情况。在这种情况下，通常最好输出错误消息并退出程序。

```c
#include <stdlib.h>
void exit(int status);
```

`exit()` 函数会停止程序，清理所有已使用的内存，并关闭当时打开的任何文件。

注意，我们需要包含 `stdlib.h` 才能使用此函数。

当分配内存时，分配函数（如 `malloc()` 和 `calloc()`）会返回一个指针。该指针的类型取决于使用的是较旧的 K&R 编译器还是较新的 ANSI 类型编译器。对于较旧的编译器，返回指针的类型为 `char`；对于 ANSI 编译器，则为 `void`。

`malloc()` 返回一个 `void` 指针（因为 `malloc` 不关心这块内存将用于什么类型），需要将其转换为适当的类型之一。`malloc` 前面的表达式 `(int*)` 被称为“强制类型转换表达式”。虽然在 ANSI/ISO C 中这不是强制要求的，但为了代码的可移植性，建议这样做。因为许多编译器尚未完全符合标准。下面的程序演示了 `malloc()` 的实际使用。

### 示例

```c
36. #include <stdlib.h>
#include <stdio.h>
int main()
{
    int * ip;
    double * dp;
    float * fp1;
    float * fp2;
    ip = (int *) malloc(sizeof(int));
    if(ip == NULL)
    {
        printf("out of memory\n");
        exit(-1);
    }
    dp = (double *) malloc(sizeof(double));
    if(dp == NULL)
    {
        printf("out of memory\n");
        exit(-1);
    }
    fp1 = (float *) malloc(sizeof(float));
    if(fp1 == NULL)
    {
        printf("out of memory\n");
        exit(-1);
    }
    fp2 = (float *) malloc(sizeof(float));
    if(fp2 == NULL)
    {
        printf("out of memory\n");
        exit(-1);
    }
```

