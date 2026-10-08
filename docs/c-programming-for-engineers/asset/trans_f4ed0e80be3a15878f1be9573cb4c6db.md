

## 12.4. 指针与字符串

const char *day[] = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};

| day[0] | "Sunday" |
| day[1] | "Monday" |
| day[2] | "Tuesday" |
| day[3] | "Wednesday" |
| day[4] | "Thursday" |
| day[5] | "Friday" |
| day[6] | "Saturday" |

图 12.3: 字符串指针数组

```c
#include <stdio.h>
int main() {
    int n;
    const char *day[] = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};

    do {
        printf("Enter a day from 1 to 7: ");
        scanf("%d", &n);

        if (n < 1 || n > 7) {
            printf("Invalid input. Please try again.\n");
        }
    } while (n < 1 || n > 7);

    puts(day[n-1]);

    return 0;
}
```

声明 `const char *day[] = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};` 创建了一个名为 day 的数组，其中每个元素都是一个指向字符串的指针。例如，day[0] 指向 "Sunday"，day[1] 指向 "Monday"，以此此类推。这允许使用数组索引方便地访问星期的名称。

## 12.5 指针与函数

### 1.1 函数指针

指针可以指向函数，允许将函数作为参数传递给其他函数、存储在数据结构中，或在运行时进行动态赋值。这使得诸如回调和实现多态等强大的技术成为可能。例如：

```c
void sayHello() {
    printf("Hello, World!\n");
}

int main() {
    // 不接受参数且返回 void 的函数指针
    void (*ptr)() = sayHello; // 注意语法

    // 将 sayHello 的地址赋值给 ptr
    ptr(); // 通过指针调用函数

    return 0;
}
```
这将输出：Hello, World!

### 1.2 与函数交换数据

指针允许函数接收并处理除标量以外的数据类型。

#### 值传递

C 语言中函数接收数据的基本方法是值传递。在值传递中，会创建参数值的副本并传递给函数。在函数内部的修改不会影响原始变量。这种方法用于整数等简单类型。例如，考虑在不修改原始值的情况下错误交换值：

```c
void swap(int x, int y) { // 错误的交换函数
    int temp = x;
    x = y;
    y = temp;
}

int main() {
    int a = 5, b = 10;
    swap(a, b); // 这里的交换无效
    printf("a: %d, b: %d\n", a, b); // 输出：5, 10 (未改变)
}
```

#### 引用传递

指针允许通过引用传递数据，使能够修改修改数据。在引用传递中，原始变量的内存地址被传递给函数。函数内部的修改会影响原始变量。这种方法用于大型数据结构（如数组），以避免复制。例如，考虑使用指针正确交换值：

```c
void swap(int *x, int *y) { // 正确的交换函数，使用了指针
    int temp = *x;
    *x = *y;
    *y = temp;
}

int main() {
    int a = 5, b = 10;
    swap(&a, &b); // 将地址传递给交换函数
    printf("a: %d, b: %d\n", a, b); // 输出：10, 5 (已交换)
}
```

在值传递和引用传递之间选择时，请考虑数据类型和预期的函数行为。值传递适用于简单数据类型，并且更，因为它避免了对原始数据的意外修改。相比之下，引用传递更适用于大型数据结构，以提高效率并修改原始数据。它避免了大量数据的复制。此外，通过引用传递，可以使用指针来间接地“返回”多个值，因为 C 函数只能返回单个值。

请参见表 12.1 了解值传递与引用传递差异的总结。

#### 表 12.1：值传递与引用传递的比较

| 特性 | 值传递 | 引用传递 |
|---|---|---|
| 传递了什么？ | 值的副本 | 原始变量的内存地址 |
| 函数内部的变化： | 原始变量 | 原始变量 |
| 优点： | 简单数据类型，安全 | 复杂数据类型，高效 |

## 12.6 动态内存分配

动态内存分配允许程序在运行时分配内存，而不是在编译时进行静态内存分配。用于动态内存管理的函数有 `malloc()` 和 `free()`。

- `malloc()`：从堆（heap）区域请求一块内存。分配的字节数作为参数。
- `free()`：将之前分配的块释放回存储区。返回分配块的指针。

例如：

```c
// 为 5 个整数分配内存
int *ptr = malloc(5 * sizeof(int));

// 使用内存
ptr[0] = 1;

// 释放内存
free(ptr);
```

这里，`malloc()` 函数为 5 个整数分配空间。我们可以通过 `ptr` 访问内存。这使得内存需求可以在运行时灵活变化，而不是在编译时固定。

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#define ARRAY_SIZE 10

int main() {
    int *array;

    // 为数组动态分配内存
    array = (int*)malloc(ARRAY_SIZE * sizeof(int));

    if (array == NULL) {
        printf("内存分配失败!\n");
        return 1;
    }

    // 设置随机数生成的种子
    srand(time(NULL));

    // 用随机数填充数组
    for (int i = 0; i < ARRAY_SIZE; i++) {
        array[i] = rand() % 101; // 生成 0..100 的随机数
    }

    // 打印数组元素
    printf("Array elements: ");
    for (int i = 0; i < ARRAY_SIZE; i++) {
        printf("%d ", array[i]);
    }
    printf("\n");

    // 释放动态分配的内存
    free(array);

    return 0;
}
```

## 12.7 空指针

空指针（Null pointers）是不指向任何内存位置的指针。可以通过给指针赋值 `NULL` 值来创建。

```c
type * pointer_name = NULL;
```

以下是空指针的一些常见用途：

- 未初始化的指针：空指针通常用于在分配有效地址之前初始化指针这有助于防止野指针。
- 函数参数：当没有意义的值可以传递时，可以将 NULL 作为参数传递给期望指针的函数。
- 动态内存分配：当使用函数 `malloc()` 时，如果内存分配失败，将返回 NULL。
- 数据结构：空指针表示树和链表等数据结构的结束。
- 提高可读性：使用空指针可以提高代码的可读性，明确表示指针未意图指向有效的内存位置。

