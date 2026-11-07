
```c
// function main begins program execution
int main(void) {
    char string1[SIZE] = ""; // reserves 20 characters
    char string2[] = "string literal"; // reserves 15 characters

    // prompt for string from user then read it into array string1
    printf("%s", "Enter a string (no longer than 19 characters): ");
    scanf("%19s", string1); // input no more than 19 characters

    // output strings
    printf("string1 is: %s\nstring2 is: %s\n", string1, string2);
    puts("string1 with spaces between characters is:");

    // output characters until null character is reached
    for (size_t i = 0; i < SIZE && string1[i] != '\0'; ++i) {
        printf("%c ", string1[i]);
    }

    puts("");
}
```

Enter a string (no longer than 19 characters): Hello there
string1 is: Hello
string2 is: string literal
string1 with spaces between characters is:
H e l l o

图 6.8 | 将字符数组当作字符串处理。（第 2 部分，共 2 部分）

### 自测题

1（选择题）以下 a)、b) 或 c) 的陈述中，哪一项是错误的？
- a) 表示字符串的字符数组可以使用 printf 和 %s 转换说明符输出，如下所示：
    printf("%s\n", month);
- b) 函数 printf 与 scanf 一样，不会检查字符数组有多大。
- c) 当函数 printf 显示表示字符串的字符数组的字符时，它会在试图打印数组末尾之后的第一个字符时停止。
- d) 以上陈述全部正确。

答案：c) 是错误的。实际上，printf 会一直显示字符，直到遇到终止空字符，即使该字符的位置已远远超出数组末尾。

2（判断题）下面的数组最多可以存储 20 个字符的字符串和一个终止空字符：

    char name1[20];

答案：错误。实际上，该语句创建的字符数组最多可以存储 19 个字符的字符串和一个终止空字符。

## 6.6 静态局部数组和自动局部数组

第 5 章讨论了存储类说明符 static。静态局部变量在程序运行期间存在，但仅在函数体内可见。我们可以将 static 应用于局部数组定义，以防止数组在每次调用函数时被创建和初始化、在每次函数退出时被销毁。这可以减少程序的执行时间，特别是对于包含大型数组且函数被频繁调用的程序。静态数组在程序启动时被初始化一次。如果没有显式初始化静态数组，则该数组的元素默认被初始化为零。

图 6.9 演示了带有局部静态数组（第 23 行）的函数 staticArrayInit（第 21～38 行）以及带有局部自动数组（第 43 行）的函数 automaticArrayInit（第 41～58 行）。函数 staticArrayInit 被调用两次（第 11 行和第 15 行）。函数中的局部静态数组在程序启动时被初始化为零（第 23 行）。该函数打印数组，为每个元素加 5，然后再次打印数组。第二次调用该函数时，静态数组包含第一次调用期间存储的值。

```c
// fig06_09.c
// Static arrays are initialized to zero if not explicitly initialized.
#include <stdio.h>

void staticArrayInit(void); // function prototype
void automaticArrayInit(void); // function prototype

// function main begins program execution
int main(void) {
    puts("First call to each function:");
    staticArrayInit();
    automaticArrayInit();

    puts("\n\nSecond call to each function:");
    staticArrayInit();
    automaticArrayInit();
    puts("");
}

// function to demonstrate a static local array
void staticArrayInit(void) {
    // initializes elements to 0 before the function is called
    static int array1[3];

    puts("\nValues on entering staticArrayInit:");

    // output contents of array1
    for (size_t i = 0; i <= 2; ++i) {
        printf("array1[%zu] = %d ", i, array1[i]);
    }

    puts("\nValues on exiting staticArrayInit:");
    // modify and output contents of array1
    for (size_t i = 0; i <= 2; ++i) {
        printf("array1[%zu] = %d ", i, array1[i] += 5);
    }
}

// function to demonstrate an automatic local array
void automaticArrayInit(void) {
    // initializes elements each time function is called
    int array2[3] = {1, 2, 3};

    puts("\n\nValues on entering automaticArrayInit:");

    // output contents of array2
    for (size_t i = 0; i <= 2; ++i) {
        printf("array2[%zu] = %d ", i, array2[i]);
    }

    puts("\nValues on exiting automaticArrayInit:");
    // modify and output contents of array2
    for (size_t i = 0; i <= 2; ++i) {
        printf("array2[%zu] = %d ", i, array2[i] += 5);
    }
}
```

图 6.9 | 如果没有显式初始化，静态数组将被初始化为零。（第 1 部分，共 2 部分）

First call to each function:

Values on entering staticArrayInit:
array1[0] = 0  array1[1] = 0  array1[2] = 0
Values on exiting staticArrayInit:
array1[0] = 5  array1[1] = 5  array1[2] = 5

Values on entering automaticArrayInit:
array2[0] = 1  array2[1] = 2  array2[2] = 3
Values on exiting automaticArrayInit:
array2[0] = 6  array2[1] = 7  array2[2] = 8

Second call to each function:

Values on entering staticArrayInit:
array1[0] = 5  array1[1] = 5  array1[2] = 5 ---- 上次调用后保留的值
Values on exiting staticArrayInit:
array1[0] = 10  array1[1] = 10  array1[2] = 10

Values on entering automaticArrayInit:
array2[0] = 1  array2[1] = 2  array2[2] = 3 ---- 上次调用后重新初始化的值
Values on exiting automaticArrayInit:
array2[0] = 6  array2[1] = 7  array2[2] = 8

函数 automaticArrayInit 也被调用两次（第 12 行和第 16 行）。自动局部数组的元素被初始化为 1、2 和 3（第 43 行）。该函数打印数组，为每个元素加 5，然后再次打印数组。第二次调用该函数时，数组元素会再次被初始化为 1、2 和 3，因为该数组具有自动存储期。

### 自测题

1（选择题）以下 a)、b) 或 c) 的陈述中，哪一项是错误的？
- a) 静态局部变量在程序运行期间存在，但仅在函数体内可见。
- b) 静态局部数组只创建和初始化一次，而不是在每次函数调用时都创建和初始化。这可以减少程序的执行时间，特别是对于包含大型数组且函数被频繁调用的程序。
- c) 如果没有显式初始化静态数组，则该数组的元素默认被初始化为零。
- d) 以上陈述全部正确。

答案：d。

## 6.7 向函数传递数组

要向函数传递数组参数，需指定不带任何方括号的数组名。例如，如果数组 hourlyTemperatures 已定义为

```c
int hourlyTemperatures[HOURS_IN_A_DAY];
```

函数调用

```c
modifyArray(hourlyTemperatures, HOURS_IN_A_DAY)
```

将数组 hourlyTemperatures 及其大小传递给函数 modifyArray。

回顾一下，C 中所有参数都是按值传递的。然而，C 会自动按引用将数组传递给函数——被调用的函数可以修改调用者的原始数组元素值。我们在第 7 章会看到这并不矛盾。数组名求值得到数组第一个元素在内存中的地址。因为传递的是数组的起始地址，被调用函数确切地知道数组存储在哪里。因此，被调用函数对数组元素所做的任何修改都会改变调用者中原始数组元素的值。

### 说明数组名是一个地址

图 6.10 通过使用 %p 转换说明符打印地址，打印 array、&array[0] 和 &array，从而证明“数组名的值”实际上就是数组第一个元素的地址。%p 转换说明符通常以十六进制数输出地址，但这取决于编译器。十六进制（基数为 16）数由数字 0 到 9 以及字母 A 到 F 组成——这些字母分别对应十进制数 10 到 15。在线附录 E 深入讨论了二进制（基数为 2）、八进制（基数为 8）、十进制（基数为 10；标准整数）和十六进制整数之间的关系。输出显示
