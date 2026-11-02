
```c
// shuffle cards in deck
void shuffle(unsigned int wDeck[][FACES])
{
    // for each of the cards, choose slot of deck randomly
    for (size_t card = 1; card <= CARDS; ++card) {
        size_t row;    // row number
        size_t column; // column number

        // choose new random location until unoccupied slot found
        do {
            row = rand() % SUITS;
            column = rand() % FACES;
        } while (wDeck[row][column] != 0);

        // place card number in chosen slot of deck
        wDeck[row][column] = card;
    }
}

// deal cards in deck
void deal(unsigned int wDeck[][FACES], const char *wFace[],
    const char *wSuit[])
{
    // deal each of the cards
    for (size_t card = 1; card <= CARDS; ++card) {
        // loop through rows of wDeck
        for (size_t row = 0; row < SUITS; ++row) {
            // loop through columns of wDeck for current row
            for (size_t column = 0; column < FACES; ++column) {
                // if slot contains current card, display card
                if (wDeck[row][column] == card) {
                    printf("%5s of %-8s%s", wFace[column], wSuit[row],
                        card % 2 == 0 ? "\n" : "\t"); // 2-column format
                }
            }
        }
    }
}
```

**图 7.24** | 洗牌与发牌。（第 2 部分，共 2 部分。）

| | |
|---|---|
| 红桃九 | 梅花五 |
| 黑桃Q | 黑桃3 |
| 红桃Q | 梅花A |
| 红桃K | 黑桃6 |
| 方块J | 黑桃5 |
| 红桃7 | 梅花K |
| 梅花3 | 红桃8 |
| 方块3 | 方块4 |
| 方块Q | 方块5 |

**图 7.25** | 发牌程序的示例运行。（第 1 部分，共 2 部分。）

| | |
|---|---|
| 方块6 | 红桃5 |
| 黑桃A | 红桃6 |
| 方块9 | 梅花Q |
| 黑桃8 | 梅花9 |
| 梅花2 | 梅花6 |
| 梅花A | 梅花J |
| 梅花4 | 梅花8 |
| 黑桃4 | 黑桃7 |
| 方块7 | 梅花7 |
| 黑桃K | 方块10 |
| 红桃J | 红桃A |
| 黑桃J | 梅花10 |
| 方块8 | 方块2 |
| 方块A | 黑桃9 |
| 红桃4 | 红桃2 |
| 方块K | 黑桃10 |
| 红桃3 | 红桃10 |

**图 7.25** | 发牌程序的示例运行。（第 2 部分，共 2 部分。）

## 7.12 函数指针

函数指针包含函数在内存中的*地址*。在第 6 章中，我们看到数组名实际上是数组中第一个元素在内存中的地址。类似地，函数名实际上是执行该函数任务的代码在内存中的起始地址。函数指针可以*传递*给函数、从函数中*返回*、*存储*在数组中，并*赋值*给其他函数指针。

### 7.12.1 按升序或降序排序

为了说明函数指针的用法，图 7.26 给出了图 7.15 中冒泡排序程序的修改版本。新版本由 `main` 以及函数 `bubble`、`swap`、`ascending` 和 `descending` 组成。函数 `bubble` 除了接收一个整型数组和数组大小之外，还接收一个函数指针——函数 `ascending` 或函数 `descending`——作为*参数*。程序提示用户选择按*升序*还是按*降序*对数组排序。如果用户输入 1，则将指向函数 `ascending` 的指针传递给函数 `bubble`，从而使数组按*递增*顺序排序。如果用户输入 2，则将指向函数 `descending` 的指针传递给函数 `bubble`，从而使数组按*递减*顺序排序。程序的输出如图 7.27 所示。

```c
1  // Fig. 7.26: fig07_26.c
2  // Multipurpose sorting program using function pointers.
3  #include <stdio.h>
4  #define SIZE 10
5
```

**图 7.26** | 使用函数指针的多用途排序程序。（第 1 部分，共 3 部分。）

```c
6 // prototypes
7 void bubble(int work[], size_t size, int (*compare)(int a, int b) );
8 int ascending(int a, int b);
9 int descending(int a, int b);
10
11 int main(void)
12 {
13    // initialize unordered array a
14    int a[SIZE] = { 2, 6, 4, 8, 10, 12, 89, 68, 45, 37 };
15
16    printf("%s", "Enter 1 to sort in ascending order,\n"
17       "Enter 2 to sort in descending order: ");
18    int order; // 1 for ascending order or 2 for descending order
19    scanf("%d", &order);
20
21    puts("\nData items in original order");
22
23    // output original array
24    for (size_t counter = 0; counter < SIZE; ++counter) {
25       printf("%5d", a[counter]);
26    }
27
28    // sort array in ascending order; pass function ascending as an
29    // argument to specify ascending sorting order
30    if (order == 1) {
31       bubble(a, SIZE, ascending);
32       puts("\nData items in ascending order");
33    }
34    else { // pass function descending
35       bubble(a, SIZE, descending);
36       puts("\nData items in descending order");
37    }
38
39    // output sorted array
40    for (size_t counter = 0; counter < SIZE; ++counter) {
41       printf("%5d", a[counter]);
42    }
43
44    puts("\n");
45 }
46
47 // multipurpose bubble sort; parameter compare is a pointer to
48 // the comparison function that determines sorting order
49 void bubble(int work[], size_t size, int (*compare)(int a, int b))
50 {
51    void swap(int *element1Ptr, int *element2Ptr); // prototype
52
53    // loop to control passes
54    for (unsigned int pass = 1; pass < size; ++pass) {
55
56       // loop to control number of comparisons per pass
57       for (size_t count = 0; count < size - 1; ++count) {
58
            // if adjacent elements are out of order, swap them
            if ((*compare)(work[count], work[count + 1])) {
                swap(&work[count], &work[count + 1]);
            }
        }
    }
}

// swap values at memory locations to which element1Ptr and
// element2Ptr point
void swap(int *element1Ptr, int *element2Ptr)
{
    int hold = *element1Ptr;
    *element1Ptr = *element2Ptr;
    *element2Ptr = hold;
}

// determine whether elements are out of order for an ascending
// order sort
int ascending(int a, int b)
{
    return b < a; // should swap if b is less than a
}

// determine whether elements are out of order for a descending
// order sort
int descending(int a, int b)
{
    return b > a; // should swap if b is greater than a
}
```

**图 7.26** | 使用函数指针的多用途排序程序。（第 3 部分，共 3 部分。）

```text
Enter 1 to sort in ascending order,
Enter 2 to sort in descending order: 1

Data items in original order
    2   6   4   8   10   12   89   68   45   37
Data items in ascending order
    2   4   6   8   10   12   37   45   68   89
```

```text
Enter 1 to sort in ascending order,
Enter 2 to sort in descending order: 2

Data items in original order
    2   6   4   8   10   12   89   68   45   37
Data items in descending order
    89   68   45   37   12   10   8   6   4   2
```

**图 7.27** | 图 7.26 中冒泡排序程序的输出。

下列参数出现在 `bubble` 的函数头中（第 49 行）：

`int (*compare)(int a, int b)`

这告诉 `bubble` 应期待一个参数（`compare`），它是指向函数的指针，该函数接收两个整型参数并返回一个整型结果。`*compare` 两边需要加圆括号，以便将 `*` 与 `compare` 组合在一起，表明 `compare` 是一个指针。如果我们没有包含圆括号，声明就会变成

`int *compare(int a, int b)`

它声明的是一个接收两个整数作为参数并返回指向整数的指针的函数。

`bubble` 的函数原型如第 7 行所示。原型中的第三个参数可以写成

`int (*)(int, int);`

即省略函数指针名和参数名。

传递给 `bubble` 的函数在 `if` 语句（第 60 行）中按如下方式调用：

`if ((*compare)(work[count], work[count + 1]))`

正如对变量指针解引用以访问变量的值一样，对函数指针解引用以使用该函数。

也可以不对指针解引用而直接调用该函数，如下所示：

`if (compare(work[count], work[count + 1]))`

这会将指针直接用作函数名。我们更倾向于第一种通过指针调用函数的方法，因为它明确说明 `compare` 是一个函数指针，并对其解引用以调用该函数。第二种通过指针调用函数的方法会使其看起来好像 `compare` 是一个实际函数。这可能会使阅读代码的程序员感到困惑，因为其想查看函数 `compare` 的定义，却发现该文件中从未定义过它。

### 7.12.2 使用函数指针创建菜单驱动系统

函数指针的一个常见用途是在基于文本的菜单驱动系统中。系统提示用户通过输入菜单项编号来从菜单（可能为 1 到 5）中选择一个选项。每个选项由不同的函数处理。指向每个函数的指针存储在一个函数指针数组中。用户的选择被用作数组中的索引，数组中的指针用于调用函数。

图 7.28 提供了一个定义和使用函数指针数组的机制的通用示例。我们定义了三个函数——function1、function2 和 function3——它们各自接收一个整型实参并且不返回任何值。我们将指向这三个函数的指针存储在数组 f 中，该数组在第 14 行定义。这个定义从最左边的一组圆括号开始读：“f 是一个包含 3 个函数指针的数组，每个函数指针都接收一个 int 作为实参并返回 void。”该数组用这三个函数的名称初始化。当用户输入 0 到 2 之间的值时，该值被用作函数指针数组的索引。在函数调用（第 25 行）中，f[choice] 选择数组中位置 choice 处的指针。对该指针解引用以调用该函数。

