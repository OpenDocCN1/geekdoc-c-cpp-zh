
```c
x = 100;
y = 200;
printf("Before exchange : x = %d\t y = %d\n\n", x, y);
exchange(&x,&y);  /* call */
printf("After exchange  : x = %d\t y = %d\n\n", x, y);
}
exchange (int *a, int *b)
{
  int t;
  t = *a;   /* Assign the value at address a to t */
  *a = *b;  /* put b into a */
  *b = t;   /* put t into b */
}
```

```text
Output

Before exchange  : x = 100   y = 200
After exchange   : x = 200   y = 100
```

图 6.11 将指针作为函数参数传递

你可能会注意到以下几点：

- 1. 函数参数被声明为指针。
- 2. 在函数体中使用解引用后的指针。
- 3. 调用函数时，地址作为实际参数传递。

使用指针访问数组元素在 C 语言中非常常见。在例 6.4 中，我们使用指针遍历数组元素。我们也可以在设计第 12 章讨论的用户自定义函数时使用这种技术。让我们考虑例 5.6 中讨论的对整数数组排序的问题。

函数 sort 可以像下面所示那样使用指针（而不是数组索引）来编写：

```c
void sort (int m, int *x)
{
  int i, j, temp;
  for (i=1; i<=m-1; i++)
    for (j=1; j<=m-i; j++)
      if (*(x+j-1) > *(x+j))
      {
        temp = *(x+j-1);
        *(x+j-1) = *(x+j);
        *(x+j) = temp;
      }
}
```

注意，我们使用指针 x（而不是数组 x[]）来接收所传递数组的地址，因此指针 x 可用于访问数组元素（如第 6.10 节所述）。该函数可用于对整数数组进行排序，如下所示：

```c
int score[4] = {45, 90, 71, 83};
sort(4, score);  /* Function call */
```

调用函数必须使用以下原型声明。

```c
void sort (int, int *);
```

这告诉编译器，接收数组的形式参数是指针，而不是数组变量。指针参数常用于字符串函数。考虑将一个字符串复制到另一个字符串的函数 copy。

```c
copy(char *s1, char *s2)
{
    while( (*s1++ = *s2++) != '\0' )
        ;
}
```

这将 s2 的内容复制到字符串 s1 中。参数 s1 和 s2 是指向字符串的指针，它们的初始值由调用函数传入。例如，调用语句

```c
copy(name1, name2);
```

会将 name1 的第一个元素的地址赋给 s1，并将 name2 的第一个元素的地址赋给 s2。

注意，*s2++ 的值是 s2 在自增之前所指向的字符。由于后缀 ++，只有在取得当前值之后，s2 才会自增。类似地，只有在赋值完成之后，s1 才会自增。

每个字符在被复制后都会与 '\0' 进行比较，因此一旦复制了 '\0'，复制就会终止。

## 6.14 返回指针的函数

到目前为止，我们已经看到，函数可以通过其名称返回单个值，或通过指针参数返回多个值。由于指针是 C 语言中的一种数据类型，我们也可以让函数向调用函数返回一个指针。考虑以下代码：

```c
int *larger (int *, int *);  /* prototype */
main ()
{
    int a = 10;
    int b = 20;
    int *p;
    p = larger(&a, &b);  /*function call */
    printf ("%d", *p);
}
int *larger (int *x, int *y)
{
    if (*x>*y)
        return (x);  /* address of a */
    else
        return (y);  /* address of b */
}
```

函数 larger 接收变量 a 和 b 的地址，使用指针 x 和 y 判断哪一个更大，然后返回其所在位置的地址。返回值随后被赋给调用函数中的指针变量 p。在这种情况下，返回的是 b 的地址并将其赋给 p，因此输出将是 b 的值，即 20。注意，返回的地址必须是调用函数中某个变量的地址。返回指向被调用函数中局部变量的指针是错误的。

## 6.15 指向函数的指针

函数和变量一样，也有类型和内存中的地址位置。因此，可以声明指向函数的指针，然后将其用作另一个函数中的参数。指向函数的指针声明如下：

```c
type (*fptr) ();
```

这告诉编译器，fptr 是指向函数的指针，该函数返回 type 类型的值。*fptr 周围的括号是必需的。请记住，像下面这样的语句

```c
type *gptr();
```

会将 gptr 声明为返回指向 type 的指针的函数。

我们可以通过简单地将函数名赋给指针，使函数指针指向特定函数。例如，以下语句

```c
double mul(int, int);
double (*p1)();
p1 = mul;
```

将 p1 声明为指向函数的指针，将 mul 声明为函数，然后使 p1 指向函数 mul。要调用函数 mul，我们现在可以使用带参数列表的指针 p1。也就是说，

```c
(*p1)(x,y) /* Function call */
```

等价于

```c
mul(x,y)
```

注意 *p1 周围的括号。

### 例 6.7 编写一个将函数指针用作函数参数的程序。

图 6.12 显示了一个在给定值范围内打印函数值的程序。打印由函数 table 完成，它通过求值由 main 传递给它的函数来实现。

在 table 中，我们如下将参数 f 声明为指向函数的指针：

```c
double (*f)();
```

该函数返回的值是 double 类型。当在以下语句中调用 table 时

```c
table (y, 0.0, 2.0, 0.5);
```

我们将指向函数 y 的指针作为 table 的第一个参数传递。注意，y 后面没有参数列表。

在 table 执行期间，语句

```c
value = (*f)(a);
```

调用 f 所指向的函数 y，并将参数 a 传递给它。因此，函数 y 在 0.0 到 2.0 的范围内以 0.5 为间隔进行求值。

类似地，调用

```c
table (cos, 0.0, PI, 0.5);
```

将指向 cos 的指针作为其第一个参数传递，因此函数 table 在 0.0 到 PI 的范围内以 0.5 为间隔计算 cos 的值。

程序

```c
#include <math.h>
#define PI 3.1415926
double y(double);
double cos(double);
double table (double(*f)(), double, double, double);

main()
{
    printf("Table of y(x) = 2*x*x-x+1\n\n");
    table(y, 0.0, 2.0, 0.5);
    printf("\nTable of cos(x)\n\n");
    table(cos, 0.0, PI, 0.5);
}
double table(double(*f)(),double min, double max, double step)
{
    double a, value;
    for(a = min; a <= max; a += step)
    {
        value = (*f)(a);
        printf("%5.2f %10.4f\n", a, value);
    }
}
double y(double x)
{
    return(2*x*x-x+1);
}
```

输出

y(x) = 2*x*x-x+1 的表

| x | y(x) |
|---|---|
| 0.00 | 1.0000 |
| 0.50 | 1.0000 |
| 1.00 | 2.0000 |
| 1.50 | 4.0000 |
| 2.00 | 7.0000 |

cos(x) 的表

| x | cos(x) |
|---|---|
| 0.00 | 1.0000 |
| 0.50 | 0.8776 |
| 1.00 | 0.5403 |
| 1.50 | 0.0707 |
| 2.00 | -0.4161 |
| 2.50 | -0.8011 |
| 3.00 | -0.9900 |

图 6.12 函数指针的使用

## 兼容性与强制类型转换

声明为指针的变量不仅仅是指针类型变量。它还是指向特定基本数据类型的指针，例如字符。因此，指针始终与一种类型相关联。我们不能将一种类型的指针赋给另一种类型的指针，尽管两者的值都是内存地址。这称为指针的不兼容性。

所有指针变量都存储内存地址，这些地址是兼容的，但不兼容的是它们所指向的底层数据类型。我们不能对不同类型的指针使用赋值运算符。然而，我们可以像对基本类型那样，通过使用强制类型转换运算符，在不兼容的指针类型之间进行显式赋值。例如：

```c
int x;
char *p;
p = (char *) x;
```

在这种情况下，我们必须确保所有使用指针 p 的操作都正确应用强制类型转换。

有一个例外。这个例外就是 void 指针（void *）。void 指针是一种通用指针，可以表示任何指针类型。所有指针类型都可以赋给 void 指针，而 void 指针也可以在不进行强制类型转换的情况下赋给任何指针。void 指针的创建方式如下：

```c
void *vp;
```

请记住，由于 void 指针没有对象类型，因此不能对它进行解引用。

## 6.16 指针与结构

我们知道，数组名表示其第零个元素的地址。结构变量数组的名称也是如此。假设 product 是一个 struct 类型的数组变量。名称 product 表示其第零个元素的地址。考虑以下声明：

```c
struct inventory
{
    char name[30];
    int number;
    float price;
} product[2], *ptr;
```

该语句将 product 声明为包含两个元素的数组，每个元素的类型为 struct inventory，并将 ptr 声明为指向 struct inventory 类型数据对象的指针。赋值

```c
ptr = product;
```

会将 product 的第零个元素的地址赋给 ptr。也就是说，指针 ptr 现在将指向 product[0]。其成员可以使用以下表示法访问。

```c
ptr -> name
ptr -> number
ptr -> price
```

符号 -> 称为箭头运算符（也称为成员选择运算符），由减号和一个大于号组成。注意，ptr-> 只是 product[0] 的另一种写法。当指针 ptr 增加一时，它便指向下一条记录，即 product[1]。下面的 for 语句将打印 product 数组所有元素的成员值。

```c
for(ptr = product; ptr < product+2; ptr++)
    printf ("%s %d %f\n", ptr->name, ptr->number, ptr->price);
```

我们也可以使用表示法

```c
(*ptr).number
```

来访问成员 number。*ptr 周围的括号是必需的，因为成员运算符 '.' 的优先级高于运算符 *。
