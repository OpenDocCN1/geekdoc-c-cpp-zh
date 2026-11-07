

```c
int main(void) {
    // initialize unordered array a
    int a[SIZE] = { 2, 6, 4, 8, 10, 12, 89, 68, 45, 37 };

    printf("%s", "Enter 1 to sort in ascending order,\n"
                 "Enter 2 to sort in descending order: ");
    int order = 0;
    scanf("%d", &order);

    puts("\nData items in original order");

    // output original array
    for (size_t counter = 0; counter < SIZE; ++counter) {
        printf("%5d", a[counter]);
    }

    // sort array in ascending order; pass function ascending as an
    // argument to specify ascending sorting order
    if (order == 1) {
        bubbleSort(a, SIZE, ascending);
        puts("\nData items in ascending order");
    }
    else { // pass function descending
        bubbleSort(a, SIZE, descending);
        puts("\nData items in descending order");
    }

    // output sorted array
    for (size_t counter = 0; counter < SIZE; ++counter) {
        printf("%5d", a[counter]);
    }

    puts("\n");
}

// multipurpose bubble sort; parameter compare is
// the comparison function that determines sorting order
void bubbleSort(int work[], size_t size, int (*compare)(int a, int b)) {
    void swap(int *element1Ptr, int *element2Ptr); // prototype

    // loop to control passes
    for (int pass = 1; pass < size; ++pass) {
        // loop to control number of comparisons per pass
        for (size_t count = 0; count < size - 1; ++count) {
            // if adjacent elements are out of order, swap them
            if ((*compare)(work[count], work[count + 1])) {
                swap(&work[count], &work[count + 1]);
            }
        }
    }
}
```

**图 7.17** 使用函数指针的多用途排序程序。（第 2 部分，共 3 部分。）

```c
// swap values at memory locations to which element1Ptr and
// element2Ptr point
void swap(int *element1Ptr, int *element2Ptr) {
    int hold = *element1Ptr;
    *element1Ptr = *element2Ptr;
    *element2Ptr = hold;
}

// determine whether elements are out of order for an ascending order sort
int ascending(int a, int b) {
    return b < a; // should swap if b is less than a
}

// determine whether elements are out of order for a descending order sort
int descending(int a, int b) {
    return b > a; // should swap if b is greater than a
}
```

```text
Enter 1 to sort in ascending order,
Enter 2 to sort in descending order: 1

Data items in original order
   2    6    4    8   10   12   89   68   45   37
Data items in ascending order
   2    4    6    8   10   12   37   45   68   89
```

```text
Enter 1 to sort in ascending order,
Enter 2 to sort in descending order: 2

Data items in original order
   2    6    4    8   10   12   89   68   45   37
Data items in descending order
  89   68   45   37   12   10    8    6    4    2
```

**图 7.17** | 使用函数指针的多用途排序程序。（第 3 部分，共 3 部分。）

### 函数指针参数

以下参数出现在 bubbleSort 的函数头中（第 48 行）：

```c
int (*compare)(int a, int b)
```

这告诉 bubbleSort 要接收一个参数（compare），它是指向函数的指针，具体来说是指向一个接收两个 int 并返回 int 结果的函数。*compare 两边的括号是必需的，用于将 * 与 compare 分组，并表明 compare 是一个指针。如果没有括号，声明将是

```c
int *compare(int a, int b)
```

它声明的是一个接收两个整数作为参数并返回指向整数的指针的函数。

要通过函数指针调用传递给 bubbleSort 的函数，我们对其进行解引用，如第 56 行的 if 语句所示：

```c
if ((*compare)(work[count], work[count + 1]))
```

对该函数的调用也可以不解引用指针，如下所示：

```c
if (compare(work[count], work[count + 1]))
```

它直接将指针用作函数名。第一种通过指针调用函数的方法明确表明 compare 是一个指向函数的指针，并对其解引用来调用函数。第二种方法使 compare 看起来像实际的函数名。这可能会让阅读代码的人感到困惑，因为他们想查看 compare 的函数定义，却发现它从未被定义。

### 7.12.2 使用函数指针创建菜单驱动系统

函数指针的一个常见用途是在菜单驱动系统中。程序提示用户通过键入菜单项的编号，从菜单（可能为 0 到 2）中选择一个选项。程序用不同的函数处理每个选项。它将指向每个函数的指针存储在一个函数指针数组中。用户的选择被用作数组下标，数组中的指针被用来调用函数。

图 7.18 提供了一个定义和使用函数指针数组的机制的一般示例。我们定义了三个函数——function1、function2 和 function3。每个函数接收一个整数参数并且不返回任何值。我们将指向这些函数的指针存储在数组 f 中（第 13 行）。从最左边的一组括号开始，该定义读作：“f 是一个包含 3 个函数指针的数组，每个指针指向接受一个 int 作为参数并返回 void 的函数。”该数组用这三个函数的名称初始化。当用户输入 0 到 2 之间的值时，我们将该值用作函数指针数组的下标。在函数调用中（第 23 行），f[choice] 选择数组中位置 choice 处的指针。我们解引用该指针来调用函数，并将 choice 作为函数参数传递。每个函数打印其参数的值和函数名，以表明该函数被正确调用。在本章的练习中，你将开发几个菜单驱动系统。

```c
1  // Fig07_18.c
2  // Demonstrating an array of pointers to functions.
3  #include <stdio.h>
4
5  // prototypes
6  void function1(int a);
7  void function2(int b);
8  void function3(int c);
9
10 int main(void) {
11     // initialize array of 3 pointers to functions that each take an
12     // int argument and return void
13     void (*f[3])(int) = {function1, function2, function3};
```

**图 7.18** | 演示函数指针数组。（第 1 部分，共 2 部分。）

```c
    printf("%s", "Enter a number between 0 and 2, 3 to end: ");
    int choice = 0;
    scanf("%d", &choice);

    // process user
    while (choice >= 0 && choice < 3) {
        // invoke function at location choice in array f and pass
        // choice as an argument
        (*f[choice])(choice);

        printf("%s", "Enter a number between 0 and 2, 3 to end: ");
        scanf("%d", &choice);
    }

    puts("Program execution completed.");
}

void function1(int a) {
    printf("You entered %d so function1 was called\n", a);
}

void function2(int b) {
    printf("You entered %d so function2 was called\n", b);
}

void function3(int c) {
    printf("You entered %d so function3 was called\n", c);
}
```

```text
Enter a number between 0 and 2, 3 to end: 0
You entered 0 so function1 was called

Enter a number between 0 and 2, 3 to end: 1
You entered 1 so function2 was called

Enter a number between 0 and 2, 3 to end: 2
You entered 2 so function3 was called

Enter a number between 0 and 2, 3 to end: 3
Program execution completed.
```

**图 7.18** | 演示函数指针数组。（第 2 部分，共 2 部分。）

## ✓ 自测

- **1.（正确/错误）** 考虑以下参数，它出现在我们的冒泡排序函数的函数头中：

  ```c
  int (*compare)(int a, int b)
  ```

  这个 compare 参数是一个指向函数的指针，该函数接收两个整数参数并返回一个整数结果。*compare 两边的括号是可选的，但为了清晰起见，我们保留它们。

  答案：*错误。* 括号是必需的，用于将 `*compare` 分组以表明 compare 是一个指针。如果没有括号，声明将是

  ```c
  int *compare(int a, int b)
  ```

  这仅仅是一个接收两个整数作为参数并*返回指向整数的指针*的函数的头。

- **2.（填空）** 就像解引用指向变量的指针可以访问变量的值一样，解引用指向函数的指针可以 ______。

  答案：调用该函数。

## 7.13 安全的 C 编程

### printf_s、scanf_s 及其他安全函数

前面的“安全的 C 编程”章节介绍了 `printf_s` 和 `scanf_s`，并提到了 C 标准附录 K 所述标准库函数的其他更安全版本。像 `printf_s` 和 `scanf_s` 这样的函数之所以更安全，一个关键特征是它们具有*运行时约束*，要求其指针参数非 `NULL`。这些函数在尝试使用指针*之前*会检查这些运行时约束。任何 `NULL` 指针参数都是*约束违规*，会导致函数失败并返回状态通知。如果 `scanf_s` 的任何指针参数（包括格式控制字符串）为 `NULL`，则调用 `scanf_s` 会返回 `EOF`。如果格式控制字符串为 `NULL`，或者任何对应于 `%s` 的参数为 `NULL`，则调用 `printf_s` 会停止输出数据并返回一个负数。有关附录 K 函数的完整细节，请参阅 C 标准文档或编译器的库文档。

### 有关指针的其他 CERT 指南

误用指针是当今系统中许多常见安全漏洞的根源。CERT 提供了各种指南来帮助你防止此类问题。如果你正在构建工业级 C 系统，你应当熟悉位于 [https://wiki.sei.cmu.edu/](https://wiki.sei.cmu.edu/) 的*CERT C 安全编码标准*。以下指南适用于本章介绍过的指针编程技术：

- **EXP34-C：** 解引用 `NULL` 指针通常会导致程序崩溃，但 CERT 遇到过解引用 `NULL` 指针可让攻击者执行代码的情况。
- **DCL13-C：** 第 7.5 节讨论了 `const` 与指针的用法。如果函数参数指向的值不会被函数更改，应使用 `const` 表示该数据是常量。例如，要表示指向不会修改的字符串的指针，请使用 `const char *` 作为指针参数的类型。
- **WIN04-C：** 本指南讨论在 Microsoft Windows 上加密函数指针的技术，以帮助防止攻击者覆盖它们并执行攻击代码。

