

## 示例：复制数组

我们经常需要制作数组的副本。请注意，我们不能简单地说：

```
.dup = num
```

所需要做的就是遍历原始数组，并将相应的值复制到第二个数组中。

```
// Makes a copy of an array.
#include <stdio.h>
#define MAX 5
int main(void) {
    int i, num[MAX], dup[MAX];
    for (i = 0; i < MAX; ++i) {
        num[i] = i;
    }
    printf("Original array:\n");
    for (i = 0; i < MAX; ++i) {
        printf("%d ", num[i]);
    }
    printf("\n\n");
    for (i = 0; i < MAX; ++i) {
        dup[i] = num[i];
    }
    printf("Duplicate array:\n");
    for (i = 0; i < MAX; ++i) {
        printf("%d ", dup[i]);
    }
    printf("\n");
    return 0;
}
```

程序输出如下：

```
Original array:
0 1 2 3 4
Duplicate array:
0 1 2 3 4
```

## 计算字母频率

假设我们想要计算文本文件中每个字母（大写和小写）出现的次数。查看 ASCII（或 Unicode）表，我们看到大写字母的数值范围是 65 - 90，小写字母的数值范围是 97 - 122。

统计每个字母出现频率的简单技巧是使用一个名为 `letter` 的数组，用于存储从文件中读取的每个字符的计数。我们可以使用每个字符的 ASCII 值作为数组的索引，该字符的计数将存储在那里。

例如，每次在文件中看到字母 `'A'` 时，我们都可以在 `letter` 数组的索引 65 处递增计数器，因为 65 是 `'A'` 的数值：

```
letter[65] = letter[65] + 1;
or
++letter[65];
or
++letter['A'];
```

在这里，字符 `'A'` 将被转换为数值（65），该数值将用作 `letter` 数组的索引。

我们可以将此推广到文件中的每个字母，如下所示：

```
++letter[c];
```

其中 c 是从文件中读取的字符。

我们计算文本文件中字母频率的代码如下：

```
// Calculates the frequency of occurrence of each letter in a file.
#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>

int main(void) {
    FILE *fp;
    int c, i;
    static int letter[256];

    if ((fp = fopen("getty.txt", "r")) == NULL) {
        fprintf("File %s could not be opened.\n", fileName);
        exit(1);
    }

    while ((c = getc(fp)) != EOF) {
        if (isupper(c) || islower(c)) {
            letter[c] += 1;
        }
    }

    for (i = 'A'; i < 'Z'; ++i) {
        if (letter[i] != 0) {
            printf("%d %c %d\n", i, i, letter[i]);
        }
    }

    puts("\n");

    for (i = 'a'; i < 'z'; ++i) {
        if (letter[i] != 0) {
            printf("%d %c %d\n", i, i, letter[i]);
        }
    }

    fclose(fp);
    return 0;
}
```

请注意，尽管我们只关心大写或小写字符，但我们声明了一个包含 256 个位置的数组，以涵盖我们在文件中可能遇到的所有可能字符，包括可打印和不可打印字符。

因此，数组的每个元素将用作索引数值对应字母的计数器。但是，我们在哪里初始化数组的每个元素，即在哪里将每个计数器初始化为零？

答案是，letter 数组被声明为 static，而声明为 static 的 int 数组会自动将数组的每个元素初始化为零！

程序输出如下：

```
69 P 1
70 F 1
73 I 3
78 N 1
84 T 2
87 W 2

97 a 100
98 b 13
99 c 31
100 d 54
101 e 165
102 f 24
103 g 26
104 h 79
105 i 66
107 k 3
108 l 41
109 m 13
110 n 75
111 o 91
112 p 16
113 q 1
114 r 81
115 s 45
116 t 122
117 u 20
118 v 23
119 w 25
121 y 10
```

## 埃拉托斯特尼筛法 埃氏筛（简单预置算法表）

埃拉托斯特尼筛法（Sieve of Eratosthenes）用于生成素数，由希腊学者埃拉托斯特尼开发，他生活在公元前约 275 年至公元前约 195 年。公元前约 240 年，埃拉托斯特尼成为埃及亚历山大图书馆的馆长，那是当时世界上最先进的学习中心。他因在诗歌、戏剧、文学、地理学、哲学和天文学方面的才华而广为人知。埃拉托斯特尼绘制了已知世界的准确地图，计算了地球的周长和其自转轴的倾斜度，并确定了地球到太阳和月球的大小及距离。

下面所示的筛法算法通过建立一个包含 1 到 1000 所有数字的数组，然后筛选出所有非素数，从而生成并计算 1 到 1000 之间的素数。已知 1、2 和 3 是素数，它筛选出 2 和 3 的所有倍数。接下来按顺序遇到且未被筛选的数字被视为素数，然后筛选出它的倍数。算法将继续进行，直到只剩下素数。

```
#include <stdio.h>
#define SIZE 1000
int main(void) {
    int i, mult, count;
    int flag[SIZE+1];
    count = 1;
    // Initialize flag array
    for (i = 1; i <= SIZE; ++i) {
        flag[i] = 1;
    }
    // Iterate through array
    for (i = 2; i <= SIZE; ++i) {
        if (flag[i] == 1) { // Found a prime
            ++count; // Count new prime
            mult = i;
            // loop deletes all multiples of new prime
            while (mult <= SIZE) {
                flag[mult] = 0;
                mult = mult + i;
            }
        }
    }
    printf("There are %d primes.\n", count);
    return 0;
}
```

- 1. 筛选要筛取值范围，故取从1到1000
- 2. 用2去筛，留下2，剔除2倍数
- 3. 用3去筛，留下3，剔除3倍数
- 4. 用5筛，留下5，剔除5倍数

## 程序输出：

```
There are 169 primes.
```

## 尝试以下操作：

看看你能否修改程序以显示 1 到 1000 之间的所有素数。

看看你能否修改程序以输出 40,000 到 50,000 之间的所有素数，每行显示 10 个。同时显示素数的数量。

## 数组元素作为函数参数

数组元素可以像任何其他变量一样作为函数参数传递。下面的示例按值传递两个数组元素。请注意，swap 函数尝试交换两个数组元素的值，但由于数组元素是按值传递的，交换后的值不会反映回 main() 中。

```
#include <stdio.h>

#define SIZE 5

void swap(int x, int y);

int main(void) {
    int i, num[SIZE];

    for (i = 0; i < SIZE; ++i) {
        num[i] = i;
    }

    printf("Before swap: num[2] = %d num[3] = %d\n", num[2], num[3]);
    swap(num[2], num[3]);
    printf("After swap: num[2] = %d num[3] = %d\n", num[2], num[3]);

    return 0;
}

void swap(int x, int y) {
    int temp;

    temp = x;
    x = y;
    y = temp;
}
```

产生的输出如下：

```
Before swap: num[2] = 2 num[3] = 3
After swap: num[2] = 2 num[3] = 3
```

通过在每个数组元素函数参数前放置取地址运算符（&），我们可以按引用传递两个数组元素。当然，我们还需要修改 swap() 函数以接受地址而不是 int 值。请注意，交换后的值现在已反映回 main() 中。

```
#include <stdio.h>

#define SIZE 5

void swap(int *x, int *y);

int main(void) {
    int num[SIZE];
    int i;

    for (i = 0; i < SIZE; ++i) {
        num[i] = i;
    }

    printf("Before swap: num[2] = %d num[3] = %d\n", num[2], num[3]);
    swap(&num[2], &num[3]);
    printf("After swap: num[2] = %d num[3] = %d\n", num[2], num[3]);

    return 0;
}

void swap(int *x, int *y) {
    int temp;

    temp = *x;
    *x = *y;
    *y = temp;
}
```

现在产生的输出如下：

```
Before swap: num[2] = 2 num[3] = 3
After swap: num[2] = 3 num[3] = 2
```

## 数组作为函数参数

将数组作为参数传递时，数组的全部内容不会被复制到形式参数数组中。相反，指向数组第一个元素的指针（地址）会被传递给形式参数。因此，函数对形式参数数组所做的任何更改实际上都是对传递给函数的原始数组进行更改，而不是对数组的副本进行更改。换句话说，在 C 中，数组始终是按引用传递的。

要将整个数组传递给函数，只需在函数调用中列出数组名，不带任何下标即可。尽管接收函数不需要知道数组的大小，但通常将数组的大小传递给函数是个好主意。

### 示例：按引用传递数组。

我们的示例将声明并初始化一个包含十个元素的数组。该数组将被传递给一个函数，其中数组的元素将被更改。数组将在调用更改数组元素的函数之前和之后输出。

```
#include <stdio.h>

void updateArray(int num[], int size);

int main(void) {
    int x[10];

    for (i = 0; i < 10; i++) {
        x[i] = i * 10;
    }

    printf("Before: ");
    for (i = 0; i < 10; i++) {
        printf("%5d", x[i]);
    }

    printf("\n\n");

    updateArray(x, 10);

    printf("After: ");
    for (i = 0; i < 10; i++) {
        printf("%5d", x[i]);
    }

    printf("\n\n");
    return 0;
}
```

