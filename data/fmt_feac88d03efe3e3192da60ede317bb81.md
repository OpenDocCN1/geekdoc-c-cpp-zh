
上述代码编译时报错“Undefined label target_pt”。`goto` 语句只能在函数内部跳转。它不能转移控制到另一个函数。

- 34. 函数调用和 `goto` 语句都可以用于从一个点转移到另一个点。那么，为什么 `goto` 语句不能用于转移控制到另一个函数？

转移到另一个函数并不简单。如果要从一个函数（即调用函数）转移到另一个函数（即被调用函数），将执行以下两个任务以及其他活动：

1. 保存调用之前调用函数中的所有计算：在调用之前，调用函数中执行的所有计算都需要保存，以便从函数返回时执行。为了保存所有计算，在执行被调用函数之前，将调用函数内部声明的所有局部变量进行保存。
2. 保存调用点：给出函数调用的点，以便在执行被调用函数后返回该点。可以通过转储寄存器的内容（特别是 `IP` 寄存器）来保存调用点。指令指针（`IP`）寄存器是一个指向要执行语句内存位置的 16 位寄存器。当从被调用函数返回时，恢复指令指针的内容，以便执行函数调用后面的语句。

执行这些额外任务需要时间，这就是为什么函数调用是耗时的。在同一个函数内部转移控制只需要操作指令指针的内容，不需要执行上述任务。

- 35. 函数提供的输入意味着参数。参数也是一个函数。因此，我们可以通过提供参数为函数提供输入吗？

是的，可以通过创建命令行参数为 `main` 函数提供输入。

### Functions

确定以下代码段的输出。假设已经包含了所需的标准头文件，且没有由于它们导致的原型错误。如果需要，用户定义函数的原型已显式列出。

```c
36. main() {
    int a;
    a=printf("Hello")+printf("Readers!!");
    printf("\n%d characters printed.",a);
}
```

```c
37. main()
{
    int a=10,b=20,c;
    c=add(a,b);
    printf("The result after addition is %d",c);
}
int add(int a, int b)
{
    return a+b;
}
```

```c
38. main()
{
    int add(int,int),a,b;
    a=b=10;
    printf("The result of addition is %d",add(a,b));
}
int add(int a, int b)
{
    return a+b;
}
```

```c
39. int add(int,int);
main()
{
    int a=10,b=10,c;
    c=add(a,b);
    printf("The result after addition is %d",c);
}
int add(int a, int b)
{
    return a+b;
}
```

```c
40. main()
{
    int add(int,int),a,b,c;
    a=10,b=20;
    c=add(a,b);
    printf("The result of addition is %d",add(a,b));
}
int add(int a, int b)
{
    return a+b;
}
```

```c
41. main()
{
    int add(int,int),a,b,c;
    a=10,b=20;
    c=add(a,b);
    printf("The result of addition is %d",c);
}
int add(int a, int b)
{
    return a+b;
}
```

# 8.60 Functions

```c
42. void fun(int a)
{
    printf("The value of a inside fun is %d\n",a);
}
main() {
    int a=10;
    b=fun(a);
    printf("The value of b after call to fun is %d",b);
}
```

```c
43. int fun(int a)
{
    printf("The value of a inside fun is %d",a);
}
main() {
    int a=10;
    b=fun(a);
    printf("The value of b after call to fun is %d",b);
}
```

```c
44. int fun(int a)
{
    printf("The value of a inside fun is %d\n",a);
    a+=2;
}
main() {
    int a=10;
    b=fun(a);
    printf("The value of b after call to fun is %d",b);
}
```

```c
45. int add(int,int)
main() {
    int a=10;b=20;
    c=add(a,b);
    printf("The result after addition is %d",c);
}
add(int a, int b) {
    a+=b;
}
```

```c
46. int add(int,int)
main()
{
    int a=10,b=20;
    c=add(a,b);
    printf("The result after addition is %d",c);
}
int add(int a, int b)
{
    a+b;
    return;
}
```

```c
47. int add(int a,int b)
{
    return a+b;
}
main()
{
    int c;
    c=add(10, 20);
    printf("The result after addition is %d",c);
}
```

```c
48. int add(int a,int b=12)
{
    return a+b;
}
main()
{
    int c;
    c=add(10, 20);
    printf("The result after addition is %d",c);
}
```

```c
49. int add(int a,int b)
{
    return a+b;
}
main()
{
    int c;
    c=add(10,20);
    printf("The result after addition is %d",c);
}
```

```c
50. int add(int a=12,int b)
{
    return a+b;
}
main()
{
    int c;
    c=add(10,20);
    printf("The result after addition is %d",c);
}
```

# 8.62 Functions

```c
51. swap(int a,int b)
{
    a*=b;b*=a;
    printf("The values of a and b swap are %d%d\n",a,b);
}
main()
{
    int a=10,b=20;
    printf("This is illustration of pass by value\n");
    printf("The values of a and b before swap are %d %d\n",a,b);
    swap(a,b);
    printf("The values of a and b after swap are %d %d\n",a,b);
}
```

```c
52. swap(int *a,int *b)
{
    *a=$*b;*b**a;
    printf("The values of a and b swap are %d %d\n",a,b);
}
main()
{
    int a=10,b=20;
    printf("This is illustration of reference\n");
    printf("The values of a and b before swap are %d %d\n",a,b);
    swap(&a,&b);
    printf("The values of a and b after swap are %d %d\n",a,b);
}
```

```c
53. int sum_diff(int a,int b)
{
    int sum=a+b;
    int diff=a-b;
    return sum;
}
main()
{
    int a=20,b=10;
    printf("Sum is %d and Difference is %d\n",sum_diff(a,b));
}
```

```c
54. int sum_diff(int a,int b)
{
    int sum=a+b;
    int diff=a-b;
    return sum;
}
main()
{
    int a=20,b=10;
    printf("Sum is %d and Difference is %d\n",sum_diff(a,b));
}
```

```c
55. int sum_diff(int a, int b)
{
    int sum=a+b;
    int diff=a-b;
    return sum;
}
main()
{
    int a=20,b=10;
    printf("Sum is %d and Difference is %d\n",sum_diff(a,b));
}
```

```c
56. void sum_diff(int a, int b, int *sum, int *diff)
{
    *sum=a+b;
    *diff=a-b;
}
main()
{
    int a=20,b=10,sum,diff;
    sum_diff(a,b,&sum,&diff);
    printf("Sum is %d and Difference is %d\n",sum,diff);
}
```

```c
57. int func1()
{
    return printf("Control1\n");
}
int func2()
{
    return printf("Control2\n");
}
main()
{
    printf("%d %d\n",func1(),func2());
}
```

```c
58. int func1()
{
    return printf("Control1\n");
}
int func2()
{
    return printf("Control2\n");
}
main()
{
    printf("%d%d\n",func1()+func2());
}
```

# 8.64 Functions

```c
59. int fact(int no)
{
    if(no==1)
        return 1;
    else
        return no*fact(no-1);
}
main()
{
    int temp;
    temp=fact(4);
    printf("The value of factorial of 4 is %d", temp);
}
```

```c
60. main()
{
    printf("Infinite Recursion\n");
    main();
}
```

```c
61. check_ptr(int ptr[2])
main()
{
    int arr[2][3]={1,2,3,4,5,6};
    printf("Size of arr in main is %d\n",sizeof(arr));
    check_ptr(arr);
}
check_ptr(int arr[2])
{
    printf("Size of arr in check is %d\n",sizeof(arr));
}
```

```c
62. int add(int a, int b)
{
    return a+b;
}
main()
{
    int (*ptr)(int,int);
    ptr=add;
    printf("The result of addition is %d\n",ptr(2,3));
    printf("The result of addition is %d",(*ptr)(2,3));
}
```

```c
63. int add(int a, int b)
{
    return a+b;
}
int sub(int a, int b)
{
    return a-b;
}
int mul(int a, int b)
{
  return a*b;
}
int div(int a, int b)
{
  return a/b;
}
main()
{
  int (*ptr[4])(int,int) = {add,sub,mul,div};
  int i;
  for(i=0;i<4;i++)
    printf("The result of called function %d is %d\n",i,ptr[i](10,5));
}
```

```c
64. int add(int,int);
int sub(int,int);
int fun(int(*)(int,int));
main()
{
  printf("%d\n",fun(add));
  printf("%d\n",fun(sub));
}
fun (* a)(int,int)
{
  return a(2,3);
}
int add(int a, int b)
{
  return a+b;
}
int sub(int a, int b)
{
  return a-b;
}
```

```c
65. int add(int a, int b)
int sub(int a, int b)
int mult(int a, int b)
int div(int a, int b)
int (*ptr)(int,int);
main()
{
  int a=10,b=20,c;
  c=add(a,b);
  printf("The result of addition is %d",c);
  c=sub(a,b);
  printf("The result of subtraction is %d",c);
  ptr=mult(a,b);
  printf("The result of multiplication is %d",c);
  ptr=div(a,b);
  printf("The result of division is %d",c);
}
```

## 8.68 Functions

代码段的输出与解释

- 36. HelloReaders!!

打印了 14 个字符

解释：

`printf` 调用是一个空表达式（void）。`printf` 函数返回一个整数值，等于它打印的字符数。因此，`printf("Hello")` 打印 Hello 并返回5。同样，`printf("Readers!!")` 打印 Readers!! 并返回9。`printf` 函数返回的值相加，最终值赋值给整数变量 `a`。通过下一个 `printf` 语句打印 `a` 的值。

- 37. 编译错误：函数 main() 中调用未定义的函数 'add'

解释：

函数在调用之前需要被定义或声明。在给定的代码中，函数 `add` 在调用之前既没有定义也没有声明。因此，编译器将无法进行类型检查，从而抛出错误信息。

- 38. 加法结果为 20

解释：

参考答案第 3 提供的解释。

在其他函数的体内部声明一个函数是有效的。函数 `add` 在调用之前声明在 `main` 函数体内部。调用时，`add` 返回 `a` 和 `b` 值相加的结果，即 20。返回的结果由 `printf` 函数打印。

- 39. 加法结果为 20

解释：

关于函数声明位置的唯一限制是它必须在调用之前。声明可以在局部作用域内，也可以在全局作用域内。在给定的代码中，函数 `add` 被声明在全局作用域内。

- 40. 编译错误

解释：

参数列表中不允许参数简写声明，这导致了编译错误。修正后的参数列表声明如下：

```c
int add(int a, int b)
{
    ......
}
```

- 41. 编译错误

解释：

参考答案第 3 提供的解释。

函数可以声明，但不能在其他函数的体内部定义。在给定的代码中，函数 `add` 被定义在 `main` 函数体内部。这是无效的并导致了编译错误。

## Functions 8.69

- 42. 编译错误

解释：

参考章节 8.4.3.2（点 2）。

函数 `fun` 的返回类型为 `void`。它不会返回任何值。如果它不返回任何值，如何将返回值赋值给 `b` 呢？因此，编写 `b=fun(a);` 是错误的并导致编译错误。

- 43. `fun` 内部 `a` 的值为 10，调用 `fun` 后 `b` 的值为 31

解释：

函数 `fun` 的返回类型未指定，默认返回值为 `int`。函数 `fun` 预期返回一个整数，但其内部没有使用 `return` 语句来返回值。如果函数内部没有使用 `return` 语句返回 `a`，则默认返回累加寄存器（`AX`）的内容。累加寄存器的内容是最后一次计算的结果。因此，`printf fun` 输出字符串并返回一个值，在执行 `printf` 后，`printf` 函数将返回累加寄存器的内容，即 1。函数 `fun` 将返回累加寄存器的内容，赋值给变量 `b` 并打印。

尝试更改传递给函数 `printf` 的字符串字符数，并观察 `b` 的值。
