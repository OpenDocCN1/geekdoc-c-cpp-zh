

## 指针简介

程序中的简单变量存储在机器特定内存位置或地址的若干字节中。例如，如果 `num` 是一个变量，那么 `&num` 就是其存储值在内存中的地址。在此上下文中，`&` 被称为 *取地址运算符*。放置在任何变量前面时，它表示该变量在内存中的地址。因此 `&num` 被视为一个常量。

*指针变量* 是存储另一个变量地址的变量。所有指针变量在任何机器上通常大小相同。指针变量可以在程序中声明，然后用于获取地址作为值。例如：

```
int num;            integer variable
int *ptr;           pointer to integer variable
ptr = &num;         address of integer variable assigned to pointer variable
```

类型说明标识所指向变量的类型，星号（`*`）将变量本身标识为指针。因此，声明：

```
int *ptr;
...
int *ptr;
```

表示 `ptr` 是一个指针变量，且它所指向的东西 `*ptr` 是 `int` 类型。

如前所述，取地址运算符 `&` 后跟变量名时，给出该变量的地址。因此 `&num` 是变量 `num` 在内存中的地址。间接运算符（有时称为解引用运算符）`*` 后跟指针变量时，给出所指向地址处存储的值。它表示被指向的东西。

## 让我们分析以下程序：

```
// pointer.c

#include <stdio.h>

(1) int main(void) {
(2) int x, y;
(3) int *ptr;

(4) x = 5;
(5) ptr = &x;
(6) y = *ptr;
(7) printf("x = %d y = %d\n", x, y);
(8) return 0;
(9) }
```

第 (3) 行声明 `ptr` 为一个指针变量，将包含某个 `int` 变量的地址。第 (5) 行使用取地址运算符将 `int` 变量 `x` 的地址赋给指针变量 `ptr`。第 (6) 行使用间接运算符获取 `ptr` 所指向的东西（一个 `int` 值）并将其赋给 `y`。我们说指针变量 `ptr` 被解引用，并给出被指向的东西，即 5，以便在赋值语句中使用。语句 (5) 和 (6) 的效果与我们进行了赋值 `y = x;` 相同，即将值 5 赋给 `y`。

该程序的输出为：

```
x = 5 y = 5
```

要在 C 程序中打印内存地址，可以使用 `%p` 格式说明符，并将 `printf()` 传递要打印的地址值。

例如：

```
// address.c

#include <stdio.h>

int main(void) {
    int x = 5;
    printf("x = %d\t &x = %p\n", x, &x);
}
```

既打印变量 x 的值，也打印其在内存中的地址。输出将类似于：

```
x = 5       &x = FFFFFFF4
```

## 函数中的指针参数

除传递数组外，C 函数始终通过将每个参数（实际参数）的值传递给函数来调用。在函数中对这些参数（形式参数）所做的任何更改都不会反映回调用环境。因此，调用环境中这些参数的存储值不能由函数更改。这称为按值传递。例如：

```
// value.c

#include <stdio.h>

int main(void);
void foo(int num);

int main(void) {
    int num = 5;

    printf("num = %d\n", num);
    foo(num);
    printf("num = %d\n", num);
    return 0;
}

void foo(int num) {
    printf("num = %d\n", num);
    num = num + 1;
    printf("num = %d\n", num);
}
```

该程序的输出为：

```
num = 5
num = 5
num = 6
num = 5
```

这表明按值传递不允许修改实际参数。

要模拟按引用传递，我们可以使用指针将任何数据项的地址传递给函数。在处理发送给函数的指针时，调用函数时指针的值（即实际参数的地址）会被复制到形式参数中。通过在函数内解引用指针，我们可以访问并修改它所指向的数据（实际参数）。

例如：

```
// swap.c

#include <stdio.h>

void swap(int *u, int *v);

int main(void) {
    int x, y;

    x = 5;
    y = 7;

    printf("x = %d\ty = %d\n", x, y);
    swap(&x, &y);
    printf("x = %d\ty = %d\n", x, y);

    return 0;
}

void swap(int *u, int *v) {
    int temp;

    printf("u = %d\tv = %d\n", *u, *v);
    temp = *u;
    *u = *v;
    *v = temp;
    printf("u = %d\tv = %d\n", *u, *v);
}
```

该程序的输出为：

| x = 5 | y = 7 |
|-------|-------|
| u = 5 | v = 7 |
| u = 7 | v = 5 |
| x = 7 | y = 5 |

请注意，调用：

```
swap(&x, &y);
```

传输实际参数 x 和 y 的地址，而不是它们的值。这意味着形式参数 u 和 v 将具有地址作为它们的值。因此，它们应使用函数原型声明为指针：

```
void swap(int *u, int *v);
```

指针和数组以几乎完全相同的方式用于访问内存。区别在于，指针是一个以地址作为值的变量，而数组名是一个固定的地址或指针。

声明数组时，编译器必须分配一个基址和足够的存储空间以容纳数组的所有元素。基址是数组在内存中存储的初始位置，即数组第一个元素（索引 0）的地址。因此，数组名也是指向数组第一个元素的指针。如果我们声明一个整数数组：

```
int num[100];
```

那么数组名 num 等价于数组第一个元素的地址 &num[0]：

```
num = &num[0]
```

两者都表示数组第一个元素的内存地址，并且两者都是指针常量，因为它们在程序运行期间保持固定。但是，它们可以作为值赋给指针变量，我们可以随意更改该指针变量的值。例如：

```
int num[100]; // reserve sizeof(int)*100 bytes of memory
int *ptr; // pointer variable
```

如果将 ptr 赋为数组 num 初始元素的地址，则可以使用指针变量访问数组存储。因此我们可以执行：

```
ptr = num;
or
ptr = &num[0];
```

数组的初始元素现在可以作为 *ptr 访问，即 ptr 所指向的东西。

## 指针运算

指针运算是 C 最强大的特性之一，并提供了数组下标索引的替代方案。语句：

```
ptr = &num[1];
and
ptr = num + 1;
```

是等价的，并将把数组第二个元素的地址赋给 ptr。有趣的是，如果指针变量 ptr 是指向特定类型的指针，那么表达式 ptr + 1 会产生存储或访问该类型下一个变量的正确内存地址。以下每个语句都是有效的，并将带我们到达该类型的下一个变量，即数组的下一个元素：

```
ptr = ptr + 1;
ptr += 1;
++ptr;
ptr++;
```

这是一个使用指针运算对 100 个整数的数组求和的程序。

```
// psum1.c
#include <stdio.h>
int main(void) {
    int i, num[100], sum, *ptr;
    for (i = 0; i < 100; i++) {
        num[i] = i;
    }
    for (sum = 0, ptr = num; ptr <= &num[99]; ptr++) {
        sum += *ptr;
    }
    printf("sum = %d\n", sum);
    return 0;
}
```

在此示例中，指针变量 ptr 首先初始化为数组 num 的基址。ptr 的连续值等价于 &num[0]、&num[1]、...、&num[99]。在每次迭代中，我们解引用指针 ptr 以访问添加到求和变量的数组元素内容。

一般来说，给定以下声明：

```
int i, num[100];
int *ptr;
```

我们可以说 ptr + i 是地址 ptr 的第 i<sup>th</sup> 个偏移量，而 num + i 是数组 num 基址的第 i<sup>th</sup> 个偏移量。以下是对数组求和的另一种方法：

```
// psum2.c

#include <stdio.h>

int main(void) {
    int i, num[100], sum;

    for (i = 0; i < 100; i++) {
        num[i] = i;
    }

    for (sum = 0, i = 0; i < 100; ++i) {
        sum += *(num + i);
    }

    printf("sum = %d\n", sum);
    return 0;
}
```

请注意，因为 num 是数组名，它是一个常量指针，以下表达式是非法的，因为我们不能更改 num 的值：

```
num = ptr;
++num;
num++;
num += 2;
```

