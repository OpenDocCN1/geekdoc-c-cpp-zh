

# 292 模块化与函数

```c
int var1, var2, var3, sum;
var1 = 10;
var2 = 20;
var3 = 30;
sum = funcsum(&var1, &var2, &var3); /* 将地址作为参数传递 */

printf("var1 = %d var2 = %d var3 = %d sum = %d\n",
var1, var2, var3, sum);

return 0;

int funcsum(int *varx, int *vary, int *varz) /* 定义参数 */
{
    /* 特定指针 */
    int sum1;
    sum1 = *varx + *vary + *varz; /* 通过指针访问值 */

    return sum1;
}
```

输出: var1 = 10 var2 = 20 var3 = 30 sum = 60

图 5.6 显示了主程序中变量的状态及其内存地址。变量 var1、var2 和 var3 的地址被作为参数传递。由于主程序中函数调用的参数是地址，因此函数原型必须将参数声明为指针数据类型。原型中的参数数据类型为 `int *`、`int *` 和 `int *`。在函数头中，数据类型必须与原型中的数据类型匹配。因此，函数头中参数的数据类型是 `int *`、`int *` 和 `int *`，这与原型中指定的数据类型一致。

我们在标准输入函数中使用已经见过指针传递。当函数需要通过参数列表返回值时，必须给它一个地址，它将值返回到该地址。我们已经在使用库输入例程时看到了这一点。例如：

```c
int a, b, errflg;
...
errflg = scanf("%d %d", &a, &b);
```

# 5.3 计算函数 293

| var1 | var2 | var3 | sum |
|---|---|---|---|
| 10 | 20 | 30 | 60 |
| 154862 | 186458 | 258348 | |

| varx | vary | varz | sum1 |
|---|---|---|---|
| 154862 | 186458 | 258348 | 60 |

图 5.6 在 main 和 funcsum 中的存储分配

当调用库输入例程时，涉及到变量 a 和 b 地址的传递。输入例程读取数据并将值放在 a 和 b 的程序存储器中，并将控制权返回给程序，如图 5.7a 和 5.7b 所示（假设数据值分别为 27 和 63）。

注意，传递给输入函数的地址用于告诉它将输入数据放在哪里。用于函数返回的状态标志在函数内部设置，并将其副本传回调用例程。输入成功时，状态标志值为 1。

第 5.2.4 节中输出二次方程解的函数可以修改为返回解而不是输出。由于返回

| a | b | errflg |
|---|---|---|
| uuuuuuuuu | uuuuuuuuu | uuuuuuuuu |
| 591250 | 591254 | 591258 |

输入期间

| 591250 | 591254 | uuuuuuuuu |

图 5.7a 输入期间

# 模块化与函数

| a | b | errflg |
|---|---|---|
| 27 | 63 | 1 |
| 591250 | 591254 | 591258 |

输入后

```c
main( )
{
    scanf(" %d %d %d", &a, &b, &c);
}
```

图 5.7b 输入后

返回语句只能返回一个值，且用于状态码，可以通过如下方式传递地址将方程的解返回给调用程序：

```c
int quadratic(float, float, float, float *, float *);

int main()
{
    float a, b, c, x1, x2;
    int status = quadratic(a, b, c, &x1, &x2);

    return 0;
}
```

```c
int quadratic(float x, float y, float z, float *addrx1, float *addrx2)
{
    int flag;
    float sqval;
    flag = 2; /* 假设有两个实数解 */

    if(x == 0)
        flag = 0; /* 不是二次方程 */
}
```

```c
else if(y * y < 4 * x * z)
    flag = -1;
else if( y * y == 4 * x * z)
{
    flag = 1;
    *addrx1 = - y / (2 * x);
}
else
{
    sqval = (b * b - 4 * a * c);
    *addrx1 = (-y + sqrt(sqval)) / (2 * x);
    *addrx2 = (-y - sqrt(sqval)) / (2 * x);
}
return flag;
```

在此示例中，a、b 和 c 按值传递，而 x1 和 x2 传递地址以便返回值。这在图 5.8 中显示了方程 $x^2 + 5x + 4 = 0$。

| main() | a | b | c | x1 | x2 | status |
|---|---|---|---|---|---|---|
| 1.0 | 5.0 | 4.0 | -1.0 | -4.0 | 2 |
| quadratic() | x | y | z | addrx1 | addrx2 | flag |
|---|---|---|---|---|---|---|
| 1.0 | 5.0 | 4.0 | 154862 | 186458 | 2 |

解引用

指针传递（call-by-pointer）中，函数通过其参数接收指针。指针是参数的地址。要访问这些指针包含的数据，必须解引用。在指针变量前使用解引用运算符（*）来访问函数中包含的值。

# 296 模块化与函数

```c
int funcsum(int *varx, int *vary, int *varz)
{
    int sum;
    sum = *varx + *vary + *varz;
    return sum;
}
```

通过在这些变量前面放置星号（*）来解引用变量 varx、vary 和 varz。指针 varx 是地址，其内容为 10。指针 vary 是地址，其内容为 20。最后，指针 varz 是地址，其内容为 30。在赋值语句 `sum = *varx + *vary + *varz` 中，*varx 被替换为 10，*vary 被替换为 20，*varz 被替换为 30。赋值给变量 sum 的结果是 60。星号（*）告诉计算机将值视为地址，找到该地址，并在那里获取（或存储）值。

如果在输出语句、赋值语句的右侧或任何需要值的地方解引用地址，则使用该地址的值。

```c
int x = 14;                   /* 14 存储在地址 A1 */
func(&x);                    /* 函数调用 */
int func(int *addrx)          /* addrx 的值为 A1 */
{
    int y;
    printf("%d", *addrx);      /* 打印 14 */
    if(*addrx > 0)             /* 比较 14 和 0 */
    {
        y = *addrx;           /* 将 14 赋值给 y */
        printf("%d", y);      /* 打印 14 */
    }
    return 0;
}
```

如果在赋值语句的左侧或任何需要存储地址的地方解引用地址，则值将存储在函数调用参数的存储器中。

```c
int x, y;
x = 14;                      /* 14 存储在地址 A1 */
y = 27;                      /* 27 存储在地址 A2 */
func(&x, &y);               /* 函数调用 */
```

```c
int func(int *addrx, int *addry)   /* addrx 的值为 A1 */
{
    /* addry 的值为 A2 */
    int z;
    scanf("%d", addrx, &z);               /* 输入 x 和 z 的值
                                     addrrx 没有改变但 x 不再
                                     是 14 */

    *addry = z;                             /* z 的值存储在 y 中，
                              addry 没有改变但 y 不再
                              是 27 */

    return 0;
}
```

解引用指针告诉在何获取或存储值。如果指针变量指向的值在函数中被更改，更改将反映在参数中。以下程序显示了函数中参数的变化如何改变 main 函数中对应的参数值。这在按值传递时不会。如果函数中的参数被解引用，通过指针传递参数会导致参数副作用。以下程序显示了这种影响。

在以下代码中，参数在 funcsum 函数中更改：

```c
int funcsum(int *, int *, int *);

int main()
{
    int var1 = 10;
    int var2 = 20;
    int var3 = 30;
    int sum;

    sum = funcsum(&var1, &var2, &var3);

    printf("var1 = %d var2 = %d var3 = %d sum = %d\n", var1, var2, var3, sum);
    printf("sum = %d\n", var1 + var2 + var3);

    return 0;
}
```

# 298 模块化与函数

```c
int funsum(int *varx, int *vary, int *varz)
{
    int sum1;
    *varx += 10;
    *vary += 15;
    *varz += 20;
    sum1 = *varx + *vary + *varz;
    return sum1;
}
```

输出: var1 = 20 var2 = 35 var3 = 50 sum = 105

图 5.9 显示了变量在函数中更改后的状态。当作为指针传递给函数参数时，函数有权访问调用函数使用的参数存储位置。通过函数参数进行的任何更改将反映在主程序的参数中。在此代码中，指针 varx、vary 和 varz 被解引用，其值被更改了。*varx += 10、*vary += 15 和 *varz += 20 语句将函数中 var1 从 10 变为 20，var2 从 20 变为 35，var3 从 30 变为 50。

![](img/8356e6c3bfe3b10354682c60b1e74b1d_317_0.png)

