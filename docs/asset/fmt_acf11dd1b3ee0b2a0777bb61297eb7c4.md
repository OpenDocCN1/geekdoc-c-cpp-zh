
```cpp
int main() {
    int i, j, arr1[ROWS][COLS], arr2[ROWS], arr3[COLS];

    for(i = 0; i < ROWS; i++) {
        for(j = 0; j < COLS; j++) {
            cin >> arr1[i][j];
        }
    }

    find_sums(arr1, arr2, arr3);

    for(i = 0; i < ROWS; i++) {
        cout << "Row " << i << ": ";
        for(j = 0; j < COLS; j++) {
            cout << arr1[i][j] << " ";
        }
        cout << "Sum = " << arr2[i] << endl;
    }

    for(j = 0; j < COLS; j++) {
        cout << "Col " << j << ": ";
        for(i = 0; i < ROWS; i++) {
            cout << arr1[i][j] << " ";
        }
        cout << "Sum = " << arr3[j] << endl;
    }

    return 0;
}
```

```cpp
void find_sums(const int arr1[][COLS], int arr2[], int arr3[])
{
    int i, j;
    for(i = 0; i < ROWS; i++) {
        arr2[i] = 0;
        for(j = 0; j < COLS; j++) {
            arr2[i] += arr1[i][j];
        }
    }
    for(j = 0; j < COLS; j++) {
        arr3[j] = 0;
        for(i = 0; i < ROWS; i++) {
            arr3[j] += arr1[i][j];
        }
    }
}
```

### C.11.23
编写一个函数，接收一个 `3x4` 的二维数组作为参数，返回一个数组，其中每个元素等于二维数组对应行的元素之和，以及另一个数组，其中每个元素等于二维数组对应列的元素之和。编写一个程序读取 `12` 个整数到一个 `3x4` 的二维数组中，并使用该函数显示每行的元素以及每列元素的总和。

（注：上述代码块为根据逻辑补全的示例，因原文中代码不完整，此处按翻译逻辑并保持结构。）

我再次强调，编译器将二维数组翻译为指向数组的指针，而不是你可能预期的指针。因此，编写 `void test(int **arr);` 是非法的。我们将在第 `14` 章讨论 `new` 运算符，你将在示例 `C14.5` 中看到我们如何使用指向变量的指针来动态创建二维数组并将其传递给函数。总结编译器如何翻译其参数：

- 一维：例如，`arr[10]` 被翻译为 `*arr`。
- 二维：例如，`arr[10][20]` 被翻译为指针 `(*arr)[20]`。
- 指针数组：例如，`*arr[10]` 被翻译为指针 `**arr`。

或者，我们可以将数组视为一维的，但我不希望这样做，因为访问元素变得更难以理解且容易出错。当然，我们需要知道它的维度。例如：

```
void f(int *arr, int rows, int cols)
{
    for(int i = 0; i < rows; i++)
```

```cpp
for(int j = 0; j < cols; j++)
cout << arr[i*cols+j] << ' ' ; /* 语法复杂且
容易出错。正如我们所知，它等同于
当我们编写 arr[i][j] 时编译器产生的表达式。 */
```

和一维数组一样，为了将二维数组作为参数传递，我们只写它的名称，不带括号。如果我们想传递一行（例如 `i`），我们传递指向该行的指针（`arr[i]`），就像传递一维数组时所做的一样。例如，以下程序显示第一行的元素：

```cpp
#include <iostream> // 示例 11.26
```

```cpp
const int ROWS = 2;
const int COLS = 3;
```

```cpp
void show_row(const int a[]);
```

```cpp
int main() {
    int arr[ROWS][COLS] = {{1, 2, 3}, {4, 5, 6}};

    show_row(arr[0]);
    return 0;
}
```

```cpp
void show_row(const int a[])
{
    for(int i = 0; i < COLS; i++)
        std::cout << a[i] << ' ';
}
```

## 练习

C.11.23 编写一个函数，接收一个 `3x4` 的二维数组作为参数，并返回一个数组，其中每个元素等于二维数组对应行的元素之和，以及另一个数组，其中每个元素等于二维数组对应列的元素之和。编写一个程序读取 `12` 个整数到一个 `3x4` 的二维数组中，并使用该函数显示每行的元素以及每列元素的总和。

（注：上述代码块为根据逻辑补全的示例，因原文中代码不完整，此处按翻译逻辑并保持结构。）

我再次强调，编译器将二维数组翻译为指向数组的指针，而不是你可能预期的指针。因此，编写 `void test(int **arr);` 是非法的。我们将在第 `14` 章讨论 `new` 运算符，你将在示例 `C14.5` 中看到我们如何使用指向变量的指针来动态创建二维数组并将其传递给函数。总结编译器如何翻译其参数：

- 一维：例如，`arr[10]` 被翻译为 `*arr`。
- 二维：例如，`arr[10][20]` 被翻译为指针 `(*arr)[20]`。
- 指针数组：例如，`*arr[10]` 被翻译为指针 `**arr`。

或者，我们可以将数组视为一维的，但我不希望这样做，因为访问元素变得更难以理解且容易出错。当然，我们需要知道它的维度。例如：

```
void f(int *arr, int rows, int cols)
{
    for(int i = 0; i < rows; i++)
```

```cpp
for(int j = 0; j < cols; j++)
cout << arr[i*cols+j] << ' ' ; /* 语法复杂且
容易出错。正如我们所知，它等同于
当我们编写 arr[i][j] 时编译器产生的表达式。 */
```

## 将二维数组作为参数

声明一个接收二维数组作为参数的函数最常见的方法是编写数组的名称，后跟它的维度。例如，`test()` 接收一个具有 `5` 行 `10` 列的二维整数数组参数。

```
void test(int arr[5][10]);
```

由于正如第 `7` 章讨论的那样，编译器不需要知道行数就可以计算元素的内存位置，因此第一个维度可以省略。如果你指定了它，编译器会忽略它。例如：

```
void test(int arr[][10]);
```

然而，必须指定列数。在通常情况下，当将多维数组传递给函数时，第一个维度必须指定，并与数组的声明匹配。在这种情况下，编译器将拥有必要的信息来对地址算术进行正确的缩放，并访问元素。在这个示例中，任何第二个维度为 `10` 的数组都可以传递给该函数，但维度不为 `10` 的数组则不行。

C++ 将二维数组视为一个一维数组的数组，编译器实际上会将二维参数翻译为指向数组的指针。因此，我们可以等价地写为：`void test(int (*arr)[10]);`；括号 `[]` 的优先级高于 `*`，必要，否则它将被解释为指向 `10` 个整数指针的数组，而不是指向包含 `10` 个整数数组的指针。虽然那种声明更准确，但我更倾向于使用第一种，以确保该参数是一个二维数组。

防御一下，问题将接踵而至。`arr` 指向哪里？它指向数组的第一行。如果执行 `arr++`，它指向哪里？在下一次中，它增加了一个行的大小。`(*arr)[1]` 是什么？它是 `arr` 所指向的行的第二个元素。`(*arr++)` 是否会让 `arr` 增加到下一行并访问其第一个元素？我们如何知道已经到达数组的总行数？通常，我们使用计数器，或者在第 `8` 章的二维数组（*) 中传递一个参数。

我再次强调，编译器将二维数组翻译为指向数组的指针，而不是你可能预期的指针。因此，编写 `void test(int **arr);` 是非法的。我们将在第 `14` 章讨论 `new` 运算符，你将在示例 `C14.5` 中看到我们如何使用指向变量的指针来动态创建二维数组并将其传递给函数。总结编译器如何翻译其参数：

- 一维：例如，`arr[10]` 被翻译为 `*arr`。
- 二维：例如，`arr[10][20]` 被翻译为指针 `(*arr)[20]`。
- 指针数组：例如，`*arr[10]` 被翻译为指针 `**arr`。

或者，我们可以将数组视为一维的，但我不希望这样做，因为访问元素变得更难以理解且容易出错。当然，我们需要知道它的维度。例如：

```
void f(int *arr, int rows, int cols)
{
    for(int i = 0; i < rows; i++)
```

```cpp
for(int j = 0; j < cols; j++)
cout << arr[i*cols+j] << ' ' ; /* 语法复杂且
容易出错。正如我们所知，它等同于
当我们编写 arr[i][j] 时编译器产生的表达式。 */
```

和一维数组一样，为了将二维数组作为参数传递，我们只写它的名称，不带括号。如果我们想传递一行（例如 `i`），我们传递指向该行的指针（`arr[i]`），就像传递一维数组时所做的一样。例如，以下程序显示第一行的元素：

```cpp
#include <iostream> // 示例 11.26
```

```cpp
const int ROWS = 2;
const int COLS = 3;
```

```cpp
void show_row(const int a[]);
```

```cpp
int main() {
    int arr[ROWS][COLS] = {{1, 2, 3}, {4, 5, 6}};

    show_row(arr[0]);
    return 0;
}
```

```cpp
void show_row(const int a[])
{
    for(int i = 0; i < COLS; i++)
        std::cout << a[i] << ' ';
}
```

## 练习

C.11.23 编写一个函数，接收一个 `3x4` 的二维数组作为参数，并返回一个数组，其中每个元素等于二维数组对应行的元素之和，以及另一个数组，其中每个元素等于二维数组对应列的元素之和。编写一个程序读取 `12` 个整数到一个 `3x4` 的二维数组中，并使用该函数显示每行的元素以及每列元素的总和。

```cpp
#include <iostream>
using std::cout;
using std::cin;
```

```cpp
const int ROWS = 3;
const int COLS = 4;
```

```cpp
void find_sums(const int arr1[][COLS], int arr2[], int arr3[]);
```

```cpp
int main() {
    int i, j, arr1[ROWS][COLS], arr2[ROWS], arr3[COLS];
    // (此处代码逻辑翻译，原文不完整)
}
```

## 322 C++ 简介

```cpp
const int ROWS = 4;
const int COLS = 4;
```

```cpp
void show_board(const int c[][COLS], const int s[][COLS]);
void sel_card(const int c[][COLS], const int s[][COLS], int row, int col);
```

```cpp
int main() {
    int i, j, m, r, c, c2, cnt, cards[ROWS], status[ROWS][COLS] = {0};
    cnt = 0;
    for(i = r = 0; i < ROWS; i++) {
        for(j = 0; j < COLS; j+=2) {
            cards[i][j] = cards[i][j+1] = r+1;
        }
    }
    srand(time(NULL));
    for(i = 0; i < ROWS; i++) {
        for(j = 0; j < COLS; j++) {
            c = cards[i][j];
            m = rand() % ROWS;
            r = rand() % COLS;
            cards[i][j] = cards[m][r];
            cards[m][r] = c;
        }
    }
    show_board(cards, status);
    m = 0;
    while (cnt != ROWS+COLS) {
        sel_card(cards, status, &r, &c);
        cout << "Card_1 = " << cards[r][c] << "\n";
        sel_card(cards, status, &r2, &c2);
        cout << "Card_2 = " << cards[r2][c2] << "\n";
        if(cards[r][c] == cards[r2][c2]) {
            cout << "Cards matched !!!\n";
            cnt += 2;
        } else {
            cout << "Sorry. No match !!!\n";
            status[r][c] = status[r2][c2] = 0;
            m++;
        }
        show_board(cards, status);
        for(i = 0; i < 18; i++)
            cout << "\n";
    }
    cout << "Congrats: You did it in " << m << " tries\n";
    return 0;
}
```

```cpp
void show_board(const int c[][COLS], const int s[][COLS])
{
    int i, j;
    for(i = 0; i < ROWS; i++) {
        for(j = 0; j < COLS; j++) {
            if(s[i][j] == 1)
                cout << c[i][j] << ' ';
            else
                cout << "*";
        }
        cout << '\n';
    }
}
```

```cpp
void sel_card(const int c[][COLS], const int s[][COLS], int *row, int *col)
{
    while (1) {
        cout << "Enter row and column: ";
        cin >>row >> *col;
        (*row)--; 
        (*col)--;
        if(*row >= ROWS || *row < 0 || *col >= COLS || *col < 0) {
            cout << "Out of bound dimensions\n";
            continue;
        }
        if(s[*row][*col] == 1) {
            cout << "Error: This card is already flipped\n";
            continue;
        }
        s[*row][*col] = 1;
        return;
    }
}
```

## 324 C++ 简介

### 将数据传递给 main()

当从从命令行运行程序时，通常需要向它传递信息。例如，假设可执行文件 `hello.exe` 存储在 `C` 盘中。命令行：

```
C:\hello 100 200
```
