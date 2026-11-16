

## 3. 编写对函数的调用：

我们需要做的第三件事就是在需要时调用该函数。

```c
// Calculates the area of a rectangle.
int main(void) {
    int length, width, area;

    length = 8;
    width = 6;

    area = calcRectArea(length, width);
    printf("The area = %d\n", area);
    return 0;
}
```

在这里，我们声明变量 length、width 和 area，并为 length 和 width 赋值。对函数 calcRectArea() 进行调用，传递两个参数 length 和 width。函数返回的值被赋给 area，然后将其输出。

函数调用可以像程序代码中的任何其他有效 C 语句一样在程序代码本身中使用。函数可以在 main() 或任何其他函数中调用，并且可以根据需要调用任意次，也可以不调用。请注意，始终只有一个函数声明和一个实现（定义），但可以对给定函数进行多次调用。

下面是我们的完整代码，其中包含多个调用我们计算矩形面积的函数的示例：

```c
int calcRectArea(int length, int width);

// Calculates the areas of various rectangles.
int main(void) {
    int length, width, area, l, w;

    // Function Call 1
    length = 8;
    width = 6;
    area = calcRectArea(length, width);
    printf("The area = %d\n", area);

    // Function Call 2
    l = 5;
    w = 3;
    area = calcRectArea(l, w);
    printf("The area = %d\n", area);

    // Function Call 3
    printf("The area = %d\n",calcRectArea(4, 8));

    // Function Call 4
    calcRectArea(2, 6);

    return 0;
}

// Calculates area of a rectangle given its length and width.
// Returns The area of a rectangle.
int calcRectArea(int length, int width) {
    int area;
    area = length * width;
    return area;
}
```

### 函数调用 1：

将值赋给变量 `length` 和 `width`，这些变量作为参数传递给函数 `calcRectArea()`。函数返回一个计算值，该值被赋给 `area`，然后将其输出。

### 函数调用 2：

将值赋给变量 l 和 w，这些变量作为参数传递给函数 calcRectArea()。函数返回一个计算值，该值被赋给 area，然后将其输出。

请注意，在这种情况下，传递给函数的参数（称为实参）的名称与函数接收的参数（称为形参）的名称不需要相同！名称不需要匹配！C 只是将第一个实参传递给第一个形参，将第二个实参传递给第二个形参，以此类推。

但是，实参的数量必须等于形参的数量（即，传递给函数的参数数量必须与函数声明接收的参数数量相同）。此外，第一个实参的数据类型必须与第一个形参的数据类型匹配，第二个实参的数据类型必须与第二个形参的数据类型匹配，以此类推。

### 函数调用 3：

函数返回值未被赋给变量以供输出，因为函数调用本身就包含在 printf() 语句中！在这里，返回的 int 值被替换到 printf() 字符串的 %d 格式说明符中，函数的返回值会立即被输出。

### 函数调用 4：

这个函数调用虽然在技术上是正确的，但并未使用函数返回的值，因为我们在调用函数时既没有赋值也没有以任何方式使用返回值。返回值被简单地忽略！我们将看到其他函数调用示例，其中返回值未被使用。

### 函数的优点

- 程序变得更易读。
- 函数可以与程序的其余部分分开进行测试和调试。
- 通过将逻辑步骤隔离在函数中，程序的各个部分更加独立，错误的可能性降低。
- 同一个函数可以从程序的不同位置调用。因此，常用的逻辑块只需编写一次。

## 程序执行流程

程序执行流程是指 C 代码被执行的顺序。执行始终从 main() 中的第一条语句开始，语句按从第一条到最后一条的顺序依次执行。

例如，考虑下面交换两个变量值的程序：

```c
int main(void) {
   int x, y, temp;   // Statement 1
   x = 5;            // Statement 2
   y = 6;            // Statement 3
   temp = x;         // Statement 4
   x = y;            // Statement 5
   y = temp;         // Statement 6
   return 0;         // Statement 7
}
```

上面程序中的语句按以下顺序执行：

- 语句 1
- 语句 2
- 语句 3
- 语句 4
- 语句 5
- 语句 6
- 语句 7

向程序中添加函数定义不会改变程序的执行流程。但是，函数内部的语句在函数被调用之前不会执行。

当进行函数调用时，程序控制权会跳转到函数中的第一条语句。函数中的所有语句都会被执行，直到遇到 return 语句或函数的右花括号为止。程序控制权会返回到函数调用发生的位置。

### 考虑以下程序：

```c
// Geometric drawing program

#include <stdio.h>

// Function prototypes
void drawRectangle(void);
void drawTriangle(void);
void drawCircle(void);

// Calls the geometric drawing functions
int main(void) {
    drawCircle();
    drawRectangle();
    drawTriangle();
    drawCircle();

    return 0;
}

// Displays a rectangle.
void drawRectangle(void) {
    printf("**********\n");
    printf("*        *\n");
    printf("*        *\n");
    printf("*        *\n");
    printf("**********\n");
}

// Displays a triangle.
void drawTriangle(void) {
    printf("   *   \n");
    printf("  * *  \n");
    printf(" *   * \n");
    printf("*     *\n");
    printf("*******\n");
}

// Displays a circle.
void drawCircle(void) {
    printf("  ***  \n");
    printf(" *   * \n");
    printf("*     *\n");
    printf(" *   * \n");
    printf("  ***  \n");
}
```

请注意，函数定义在程序中出现的顺序并不重要。让我们执行 `main()` 函数的第一行：

```
drawCircle();
```

执行此语句会将程序控制权转移到 `drawCircle()` 函数。`drawCircle()` 函数中的以下每条语句都会被执行：

```
printf(" **** \n");
printf(" * * \n");
printf("** ** \n");
printf(" * * \n");
printf(" **** \n");
```

当到达 `drawCircle()` 函数的右花括号时，程序控制权会返回到 `main()` 中对 `drawCircle()` 调用之后的语句：

```
drawRectangle();
```

执行此语句会将程序控制权转移到 `drawRectangle()` 函数。`drawRectangle()` 函数中的以下每条语句都会被执行：

```
printf("************\n");
printf("** **\n");
printf("** **\n");
printf("** **\n");
printf("************\n");
```

当到达 `drawRectangle()` 函数的右花括号时，程序控制权会返回到 `main()` 中对 `drawRectangle()` 调用之后的语句：

```
drawTriangle();
```

执行此语句会将程序控制权转移到 drawTriangle() 函数。drawTriangle() 函数中的以下每条语句都会被执行：

```
printf(" * \n");
printf(" * * \n");
printf(" * * * \n");
printf(" * * * * \n");
printf("*********\n");
```

当到达 drawTriangle() 函数的右花括号时，程序控制权会返回到 main() 中对 drawTriangle() 调用之后的语句：

```
drawCircle();
```

执行此语句会将程序控制权转移到 drawCircle() 函数。drawCircle() 函数中的以下每条语句将再次被执行：

```
printf(" *** \n");
printf(" * * \n");
printf(" * * \n");
printf(" * * \n");
printf(" *** \n");
```

当到达 drawCircle() 函数的右花括号时，程序控制权会返回到 main() 中对 drawCircle() 调用之后的语句：

```
return 0;
```

这完成了程序的执行，并将控制权移交回操作系统。

