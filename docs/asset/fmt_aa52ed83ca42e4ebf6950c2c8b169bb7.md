
# 动手练习 2：数组的和

编写一个计算整数数组所有元素之的程序。

将下方程序输入 `Code::Block`，像第 1 天那样进行编译和运行。

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 40, 50};
    int size = sizeof(numbers) / sizeof(numbers[0]);
    int sum = 0;

    // 计算元素之和
    for (int i = 0; i < size; i++) {
        sum += numbers[i];
    }

    printf("Sum of array elements: %d\n", sum);

    return 0;
}
```

![](img/50a3ffd9d521bd89400f66c4b293162_132_0.png)

图 12 练习执行的控制台输出示例

# 练习 3：反转数组

编写一个原地反转整数数组元素的程序。

将下方程序输入 `Code::Block`，像第 1 天那样进行编译和运行。

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 40, 50};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    // 原地反转数组
    for (int i = 0; i < size / 2; i++) {
        int temp = numbers[i];
        numbers[i] = numbers[size - 1 - i];
        numbers[size - 1 - i] = temp;
    }

    // 打印数组
    for (int i = 0; i < size; i++) {
        printf("Element at index %d: %d\n", i, numbers[i]);
    }

    return 0;
}
```

```
Element at index 0: 50
Element at index 1: 40
Element at index 2: 30
Element at index 3: 20
Element at index 4: 10
```

图 13 练习执行的控制台输出示例

# 动手练习 4：使用指针交换整数

编写一个使用指针交换两个整数值的 C 程序。

```c
#include <stdio.h>

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int num1 = 5, num2 = 10;
    printf("Before swap: num1 = %d, num2 = %d\n", num1, num2);
    swap(&num1, &num2);
    printf("After swap: num1 = %d, num2 = %d\n", num1, num2);
    return 0;
}
```

![](img/50a3ffd9d521bd89400f66c4b293162_137_0.png)

图 14 练习执行的控制台输出示例

# 练习 5：使用指针查找字符串长度

编写一个使用指针计算字符串长度的 C 程序。

```c
#include <stdio.h>

int stringLength(const char *str) {
    const char *p = str;
    while (*p) {
        p++;
    }
    return p - str;
}

int main() {
    const char *text = "Hello, World!";
    int length = stringLength(text);
    printf("Length of the string: %d\n", length);
    return 0;
}
```

```
Length of the string: 13
```

图 15 练习执行的控制台输出示例

# 练习 6：使用指针计算数组之和

编写一个使用指针计算数组元素之和的 C 程序。

```c
#include <stdio.h>

int arraySum(int *arr, int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += *(arr + i);
    }
    return sum;
}

int main() {
    int numbers[] = {1, 2, 3, 4, 5};
    int size = sizeof(numbers) / sizeof(numbers[0]);
    int sum = arraySum(numbers, size);
    printf("Sum of elements in the array: %d\n", sum);
    return 0;
}
```

```
Sum of elements in the array: 15
```

图 16 练习执行的控制台输出示例

# 练习 7：数组的指针算术

编写一个 C 程序，通过使用指针倒序打印整数数组元素来演示数组的指针算术。

```c
#include <stdio.h>

void printReverse(int *arr, int size) {
    int *p = arr + size - 1;
    while (p >= arr) {
        printf("%d ", *p);
        p--;
    }
    printf("\n");
}

int main() {
    int numbers[] = {10, 20, 30, 40, 50};
    int size = sizeof(numbers) / sizeof(numbers[0]);
    printReverse(numbers, size);
    return 0;
}
```

```
}

int main() {

int numbers[] = {1, 2, 3, 4, 5};

int size = sizeof(numbers) / sizeof(numbers[0]);

printf("Array in reverse order: ");

printReverse(numbers, size);

return 0;
}
```

![](img/50a3ffd9d521bd894000f66c4b293162_145_0.png)

图 17 练习执行控制台输出示例

# 第 8 天：文件处理

## 阅读作业：文件 I/O 基础

文件 I/O（输入/输出）是编程的一个基础方面，允许你从文件中读取数据并将数据写入文件。在这份基础指南中，我将提供 C 语言中用于读取和写入文件的示例。你也可以将这些概念应用于其他编程语言。

### 1. 从文件中读取

以下是在 C 中从文件中读取的方法：

```c
#include <stdio.h>

int main() {
    // 声明一个文件指针
    FILE *file;

    // 打开文件进行读取
    file = fopen("sample.txt", "r");

    // 检查文件是否成功打开
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 1; // 使用错误码退出
    }

    // 读取并打印文件的每一行
    char line[100]; // 假设行不超过 100 个字符
    while (fgets(line, sizeof(line), file) != NULL) {
        printf("%s", line);
    }

    // 关闭文件
    fclose(file);

    return 0;
}
```

在这个示例中，我们：

- 声明了一个文件指针 (`FILE *file`)。
- 使用 `fopen` 打开文件。
- 检查文件是否成功打开。
- 使用 `fgets` 从文件中读取行并打印它们。
- 最后使用 `fclose` 关闭文件。

### 2. 写入文件

以下是在 C 中向文件中写入的方法：

```c
#include <stdio.h>

int main() {
    // 声明一个文件指针
    FILE *file;

    // 打开文件进行写入
    file = fopen("output.txt", "w");

    // 检查文件是否成功打开
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 1; // 使用错误码退出
    }

    // 将数据写入文件
    fprintf(file, "Hello, File I/O!\n");
    fprintf(file, "This is a basic example.\n");

    // 关闭文件
    fclose(file);

    return 0;
}
```

在这个示例中，我们：

- 声明了一个文件指针 (`FILE *file`)。
- 使用 `fopen` 打开文件，并指定文件名 ("output.txt") 和写入模式 ("w")，这会创建一个新文件或截断现有文件。
- 检查文件是否成功打开。
- 使用 `fprintf` 将数据写入文件。
- 最后使用 `fclose` 关闭文件。

记住妥善处理错误，检查文件是否打开成功，并在完成后关闭文件以释放系统资源。此外，你还可以探索其他模式（例如用于追加的 "a"）和错误处理机制，以实现更健壮的文件 I/O 操作。

# 动手练习 1：从文件中读取文本

编写一个 C 程序，读取名为 "input.txt" 的文本文件的内容并将其打印到控制台。

创建一个仅包含 "Hello" 的文本文件 "input.txt"。该 "input.txt" 文件需要与 `main.c` 位于同一目录下。

在 `Code::Block` 中输入下方所示程序，并像第 1 天那样进行编译和运行。

```c
#include <stdio.h>

int main() {
    FILE *file;
    char ch;

    // 打开文件进行读取
    file = fopen("input.txt", "r");

    // 检查文件是否成功打开
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 1; // 使用错误码退出
    }

    // 读取并打印文件的每个字符
    while ((ch = fgetc(file)) != EOF) {
        printf("%c", ch);
    }

    // 关闭文件
    fclose(file);

    return 0;
}
```

C:\myproject\day1\exe

Hello

Process returned 0 (execution time: 0.040s)

Press any key to continue.

图 18 练习 1 的控制台输出示例

# 练习 2：向文件中写入文本

编写一个 C 程序获取用户输入并将其写入名为 "output.txt" 的文本文件。

在 `Code::Block` 中输入下方所示程序，并像第 1 天那样进行编译和运行。

```c
#include <stdio.h>

int main() {
    FILE *file;
    char text[100];

    // 打开文件进行写入
    file = fopen("output.txt", "w");

    // 检查文件是否成功打开
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 1; // 使用错误码退出
    }

    // 读取用户输入并将其写入文件
    if (fgets(text, sizeof(text), stdin) != NULL) {
        fprintf(file, "%s", text);
    }

    // 关闭文件
    fclose(file);

    return 0;
}
```

C:\myproject\day1\exe

Enter text:

Hello

Process returned 0 (execution time: 0.040s)

图 19 练习 2 的控制台输出示例

# 练习 3：将文本写入文件

编写一个 C 程序，读取名为 "input.txt" 的文本文件内容并将其写入到名为 "output.txt" 的文本文件中。

创建一个仅包含 "Hello" 的文本文件 "input.txt"。该 "input.txt" 文件需要与 `main.c` 位于同一目录下。

在 `Code::Block` 中输入下方所示程序，并像第 1 天那样进行编译和运行。

```c
#include <stdio.h>

int main() {
    FILE *file;
    char ch;

    // 打开文件进行读取
    file = fopen("input.txt", "r");

    // 检查文件是否成功打开
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 1; // 使用错误码退出
    }

    // 打开文件进行写入
    file = fopen("output.txt", "w");

    // 检查文件是否成功打开
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 1; // 使用错误码退出
    }

    // 读取文件的每个字符并写入文件
    while ((ch = fgetc(file)) != EOF) {
        fprintf(file, "%c", ch);
    }

    // 关闭文件
    fclose(file);
    fclose(file);

    return 0;
}
```

C:\myproject\day1\exe

Hello

Process returned 0 (execution time: 0.040s)

```cpp
int x;

int y;
} Point;
```

现在你可以直接声明 `Point` 变量而无需使用 `struct`：

`Point p5;`

在 C 和 C++ 中定义结构体是一项基础概念，它允许你创建自定义数据类型来表示程序中的复杂数据结构。它们被广泛用于高效地组织和管理数据。

## 阅读作业：联合体 (Unions)

C 中的 `UNION`（联合体）是一种复合数据类型，允许你定义一个结构，其中不同数据类型的多个变量共享相同的内存位置。与结构体不同（结构体所有成员的内存是单独分配的），联合体在任何时刻只有一个成员可以持有值。当你需要在同一内存空间中表示不同类型的数据时，联合体特别有用，可以节省内存并为程序提供灵活性。以下是在 C 语言中定义和使用联合体的方法：

### 定义联合体：

定义联合体的语法与结构体相似：

```c
union unionName {

    datype member1;

    datype member2;

    // ...
    dataType memberN;
}
```

- `UNION`: 使用该关键字来声明联合体。
- `unionName`: 这是联合体类型的名称。
- `dataType`: 这些是联合体成员的数据类型。每个成员可以有不同的数据类型。
- `member1`, `member2`, ..., `memberN`: 这些是联合体成员的名称。

示例：

让我们定义一个联合体 `Value`，它可以持有存储整数、浮点数或字符：

```c
union Value {
    int intValue;
    float floatValue;
    char charValue;
};
```

在这个示例中，我们定义了一个名为 `Value` 的联合体，包含三个成员：`intValue`、`floatValue` 和 `charValue`。

### 访问联合体成员：

访问联合体成员时像使用结构体一样使用点 (.) 运算符。但请记住，任何时候只应访问并给一个成员赋值：

```c
union Value data;
```

```c
data.intValue = 42; // 分配一个整数值
```

```c
data.floatValue = 3.14; // 分配一个浮点值
```

```c
// 在另一个成员赋值后访问该成员是未定义行为
```

### 联合体的大小：

联合体的大小由其最大成员的大小决定。在上面的示例中，`Value` 联合体的大小将是整数的大小，因为它是最大的成员。

### 初始化联合体：

你可以在声明时初始化联合体：

```c
union Value data = {42}; // 将 intValue 成员初始化为 42
```

### 用场景：
