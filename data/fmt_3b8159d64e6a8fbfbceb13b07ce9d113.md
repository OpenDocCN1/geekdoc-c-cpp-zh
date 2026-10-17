
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

# 12.7 空指针

空指针 `Null pointers` 是不指向任何内存位置的指针。可以通过给指针赋值 `NULL` 值来创建。

```c
type * pointer_name = NULL;
```

以下是空指针的一些常见用途：

- 未初始化的指针：空指针通常用于在分配有效地址之前初始化指针这有助于防止野指针。
- 函数参数：当没有意义的值可以传递时，可以将 `NULL` 作为参数传递给期望指针的函数。
- 动态内存分配：当使用函数 `malloc()` 时，如果内存分配失败，将返回 `NULL`。
- 数据结构：空指针表示树和链表等数据结构的结束。
- 提高可读性：使用空指针可以提高代码的可读性，明确表示指针未意图指向有效的内存位置。

# 第12章 指针

在访问任何指针变量之前检查其是否为 `NULL` 指针是一个良好的习惯，可以避免运行时错误和崩溃。

## 检查指针是否为 NULL

编写程序以避免在使用 `NULL` 指针访问指针值时发生段错误

```c
// C NULL pointer demonstration
#include <stdio.h>

int main() {
    // 声明空指针
    int *ptr = NULL;

    // 仅当指针有值时才进行解引用
    if (ptr == NULL) {
        printf("Pointer does not point to anything");
    } else {
        printf("Value pointed to by pointer: %d", *ptr);
    }
    return 0;
}
```

C语言标准规定了 `NULL` 指针，为程序员提供了一种机制来判断给定的指针是否合法。

## 解引用 NULL 指针

如果我们使用以下 C 代码会发生什么：

```c
// Trying to dereencing a null pointer
#include<stdio.h>
int main() {
    int *ptr = NULL;

    printf("%d",*ptr);
    return 0;
}
```

在某些机器上，上述代码可以编译成功，但在运行时会崩溃。程序在所有机器上的表现并不一致。请在风险风险的情况下尝试该代码！

# 高级指针概念

## 空指针

空指针 `void *` 是 C 语言中的一种特殊指针，它可以指向任何数据类型的对象。它们提供了一种通用的操作方法，可以在不指定特定数据类型的情况下处理内存地址。

空指针类似于通配符指针，可以存储任何数据类型的地址。它使用以下语法定义：

```c
void *pointer_name;
```

通过空指针，我们可以存储和操作内存地址，无需关心所指向数据的实际类型。

示例：

```c
void *ptr;
int x = 10;

ptr = &x; // 将 x 的地址赋值给空指针
```

```c
// 要解引用空指针，
// 需要将其转换为适当的类型
printf("Value of x: %d", *(int*)ptr); // 输出: Value of x: 10
```

空指针不能直接解引用，因为它们缺乏特定的类型。相反，它们在解引用之前需要进行类型转换。示例：

```c
int x = 4;
float y = 5.5;
void *ptr;

// 将 x 的地址赋值给 ptr
ptr = &x;
```

```c
// 将空指针转换为 int 后对其进行解引用
printf("Integer variable is %d", *(int*)ptr);
```

```c
// 现在，将 y 的地址赋值给 ptr
ptr = &y;
// 将空指针转换为 float 后对其进行解引用
printf("Float variable is %f", ((float*)ptr);
```

输出：

Integer variable = 4

Float variable = 5.500000

空指针在 C 编程中具有多种优势：

- 它们通常与 `malloc()` 和 `calloc()` 等内存分配函数一起使用，因为这些函数返回空指针，允许它们为任何数据类型分配内存。
- 空指针能够实现泛型函数，例如用于 `qsort()` 的比较函数，它可以处理不同的数据类型。
- 当与类型为 `void (*) (void)` 的函数指针结合时，可以指向接受任何参数并返回任何值的函数。
- 空指针对于实现动态数据结构（如列表、树和队列）至关重要，在这些结构中数据类型可能会变化。
- 它们还经常用于类型转换，增加了数据操作的灵活性。

### 指针转换

指针转换涉及将指针从一种数据类型转换为另一种类型。它在处理空指针或处理不兼容的指针类型时经常使用。

示例：

```c
float pi = 3.14;
void *voidPtr = &pi; // 指向 pi 的指针

// 将空指针转换为 float 指
float *floatPtr = (float*)voidPtr;

printf("Value of pi: %.2f\n", *floatPtr); // 输出: Value of pi: 3.14
```

### 悬空指针

当指向已释放或不再有效的内存时，就会产生悬空指针。例如，当之前分配给指针的内存被释放，但指针仍然持有该地址时。悬空指针会导致不可预测的行为，例如访问程序未拥有的内存或导致崩溃。

示例：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *ptr, a = 55;

    ptr = malloc(sizeof(int)); // 分配内存
    *ptr = 33; // 在动态分配的内存中存储数字
    printf("Data at ptr: %d\n", *ptr);
    ptr = &a; // 指向 'a'
    printf("Data at ptr: %d\n", *ptr);
    free(ptr); // 释放内存
    return 0;
}
```

代码首先声明了一个整数指针 `ptr` 和一个整数变量 `a`。然后，使用 `malloc()` 为整数动态分配内存，并将分配的内存地址赋值给 `ptr`。

在分配内存后，代码将数字 33 存储在动态分配的内存中并打印。然后，它将 `ptr` 指向变量 'a' 的地址并打印其值。最后，它调用了 `free(ptr)`，这是有问题的，因为 'a' 是栈变量，而不是堆分配的内存。这产生了一个悬空指针。

为了避免此类问题，请确保仅对通过 `malloc`、`calloc` 或 `realloc` 分配的内存调用 `free`。

## 进阶指针概念

```c
type **pointer_name = &normal_pointer_variable;
```

示例用法：

```c
int var = 10;
int *ptr = &var; // 指向 var 的指针
int **pptr = &ptr; // 指向 ptr 的指针
```

```c
// 输出：通过 pptr 获取 var 的值: 10
printf("Value of var via pptr: %d\n", **pptr);
```

![](img/33fb6b7acbb6df48a3c9564e97117da6_206_0.png)

图 12.6：双指针

这是一个演示在 C 中使用双指针的程序：

```c
// 演示指向指针的 C 程序
#include <stdio.h>

int main() {
    int var = 10;
    int *ptr = &var; // 指向 var 的指针
    int **pptr = &ptr; // 指向 ptr 的双级指针

    ptr = &var; // 将 var 的地址存入 ptr
    pptr = &ptr; // 将 ptr 的地址存入 pptr

    // 使用单指针和双指针显示 var 的值
    printf("Value of var: %d\n", var);
    printf("Value of var using single pointer = %d\n", *ptr);
    printf("Value of var using double pointer = %d\n", **pptr);

    // 显示指针地址
    printf("Address of pptr = %p\n", pptr);
    printf("Value of pptr = %p\n", *pptr);
    printf("Address of ptr = %p\n", &ptr);
    printf("Value of pptr = %p\n", ptr);
    printf("Address of val = %p\n", &var);

    return 0;
}
```

典型输出：

```
Value of var = 10
Value of var using single pointer = 10
Value of var using double pointer = 10
Address of pptr = 0x7ffee78f470
Value of pptr = 0x7ffee78f468
Address of pptr = 0x7ffee78f468
Value of pptr = 0x7ffee78f464
Address of val = 0x7ffee78f464
```

具体的地址将取决于程序分配的内存而变化。

双指针在 C 中有多种用途，包括：

- 修改作为参数传递给函数的指针变量中存储的地址。
- 为多维数组动态分配内存。
- 管理分级数据结构，例如树节点或链表。

在 C 中，指针不限于两个层级。我们可以根据需要使用任意层级，但由于复杂性的增加，使用多个层级时应格外谨慎。

## 12.9 树莓派中的硬件访问

树莓派是一种广泛使用的单板计算机，它提供了多种硬件能力，包括通用输入/输出 `GPIO` 引脚。在为树莓派进行 C 编程时，指针对于高效访问和操作这些硬件组件至关重要。

为了演示，让我们考虑控制连接到 `GPIO` 引脚 18 的 `LED`。我们将使用指针直接访问 `GPIO` 寄存器并设置或读取引脚值。

```c
#include <bcm2835.h>

// LED 的 GPIO 引脚号
#define LED_PIN 18

int main() {
    // 初始化 GPIO
    if(!bcm2835_init())
        return 1;

    // 设置 LED 引脚为输出
    bcm2835_gpio_fsel(LED_PIN, BCM2835_GPIO_FSEL_OUTP);

    // 声明指向 GPIO 寄存器基地址的指针
    volatile unsigned *gpio = (volatile unsigned *) BCM2835_GPIO_BASE;

    while(1) {
        // 使用指针向 GPIO 引脚写入 1，开启 LED
        *gpio |= (1<<LED_PIN);

        // 延迟
        delay(1000);

        // 向 GPIO 引脚写入 0 关闭 LED
        *gpio &= ~(1<<LED_PIN);

        // 延迟
        delay(1000);
    }
    return 0;
}
```

在此示例中：

- 我们使用 `bcm2835` 库初始化 `GPIO`。`bcm2835` 库是一个 C 库，用于直接、底层访问树莓派博通 2835 SOC（片上系统）上的 `GPIO`（通用输入/输出）。
- 将 `GPIO` 引脚 18 设置为输出引脚。
- 声明指向 `GPIO` 寄存器基地址的指针。`volatile` 关键字告诉编译器寄存器中的值可能会在程序外部随时更改。
- 在循环内部，我们使用指针直接写入 `GPIO` 寄存器位掩码，并在延迟之间切换 `LED` 的开关状态。

这种直接访问提供了对 `LED` 等硬件组件的控制。指针允许我们直接与物理 `GPIO` 端口交互，便于与树莓派上的外部设备进行实时接口。

## 总结

在本章中，我们涵盖了指针的指针、动态内存分配以及 C 中用于管理内存的一些常用函数。通过理解这些概念，你将能够编写出更高效、更强大的 C 代码，同时避免常见的陷阱和安全风险。

通过练习、耐心和奉献，你将掌握指针和内存管理。

问题

- 12.1 什么是指针的指针？
- 12.2 指针与普通变量有何区别？
- 12.3 如何获取指针指向的值？
- 12.4 取地址运算符 `(&)` 与解引用运算符 `(*)` 有什么区别？
- 12.5 如何将数组作为参数传递给函数？
- 12.6 解释指针算术。如何增加或递减指针？
- 12.7 使用指针时有哪些常见的错误？
- 12.8 使用指针时有哪些常见的错误？
- 12.9 使用指针时有哪些常见的错误？
- 12.10 使用指针时有哪些常见的错误？
- 12.11 使用指针时有哪些常见的错误？
- 12.12 使用指针时有哪些常见的错误？
- 12.13 使用指针时有哪些常见的错误？
- 12.14 使用指针时有哪些常见的错误？
- 12.15 什么是结构体？

# 13. 结构化数据

在编程中，结构体 `struct` 是将不同变量分组到一个名称下以创建自定义类型的基本方法。

## 结构体：语法声明

定义结构体的语法涉及 `struct` 关键字、结构体名称以及在大括号内的成员变量列表。例如：

```c
struct Person {
  char name[10];
  int age;
  float height;
};
```

这段代码定义了一个名为 `person` 的结构体，包含三个成员变量：`name`、`age` 和 `height`。

## 访问结构体成员

访问结构体成员涉及点运算符 `.` 后紧跟成员名称。例如：

```c
#include <stdio.h>

struct Person {
    char name[10];
    int age;
    float height;
};

int main() {
    // 声明并初始化结构体变量
    struct Person person1 = {"Sarah", 20, 1.65f};
    struct Person person2 = {"Adam", 25, 1.80f};

    // 打印第一个结构体数据
    printf("Name: %s\n", person1.name);
    printf("Age: %d\n", person1.age);
    printf("Height: %f\n", person1.height);

### 打印第二个结构体数据
    printf("Name: %s\n", person2.name);
    printf("Age: %d\n", person2.age);
    printf("Height: %f\n", person2.height);

    return 0;
}
```

![](img/33fb6b7acbb6df48a3c9564e97117da6_211_0.png)

## 结构体指针

指针也可以指向结构体和联合体，允许对复杂数据结构进行动态分配和操作。声明结构体指针非常简单：

```c
struct Person *ptr;
```

要通过指针访问结构体成员，我们可以使用箭头运算符 `->` 或者通过解引用：

```c
ptr->age = 26;
(*ptr).age = 26;
```

在处理包含指针的结构体（例如链表）时，这个箭头运算符特别有用。

示例代码如下：

```c
#include <stdio.h>

struct Person {
    char name[18];
    int age;
    float height;
};

int main() {
```

// 声明并初始化结构体变量

struct Person person1 = {"Sarah", 20, 1.65f};

struct Person person2 = {"Adam", 25, 1.8f};

// 声明指向结构体的指针

struct Person *ptr;

// 将结构体变量的地址赋值给指针

ptr = &person1;
