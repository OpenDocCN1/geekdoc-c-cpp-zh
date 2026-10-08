

## 10.7.3 统计二进制表示中的置位

`bitcount()` 函数接收一个整数作为输入，并返回其二进制表示中 1 的个数。算法如下：

- 1. 将变量 `count` 初始化为 0。
- 2. 在循环中，使用位与操作与 1 检查 `n` 的最低位（LSB）是 0 还是 1。
- 3. 如果 LSB 为 1，则计数 `count`。
- 4. 将 `n` 右移 1 位，将下一位移到最低位置。
- 5. 重复步骤 2-4，直到 `n` 变为 0，表示所有位都已计数。
- 6. 返回最终计数结果。

```c
int bitcount(int n) {
    count = 0;
    while(n != 0) {
        if (n&1 != 0) // test last bit
            count++;
        n = n >> 1;
    }
    return count;
}
```

注意，对于 32 位整数，循环可能需要 32 次迭代，但如果所有的 1 位都被移出，循环可以提前结束。
与其在 LSB 为 1 时递增 `count`，你也可以使用 `count = count + (n&1)`；但编译器可能会生成相同的机器代码。

## 10.7.4 一种改进方法：Brian Kernighhan 算法

`popcount` 函数接收一个整数 `n` 作为输入，并返回其二进制表示中 1 的个数。该函数使用了一种称为 Brian Kernighhan 算法的技巧来统计数字中置位（1位）的数量。“popcount” 是 population count（人口计数）的缩写，指的是数字二进制表示中值为 1 的位总数。该算法如下：

- 1. 将变量 `count` 初始化为 0。
- 2. 在循环中，对 `n` 和 `n-1` 执行位与操作，以清除最低位（将其设置为 0），并将结果存回 `n` 中。
- 3. 每次迭代中，最低位被清除，且 `count` 加 1。
- 4. 循环持续到 `n` 变为 0，表示所有位都已清除。
- 5. 返回最终计数结果。

```c
int popcount(int n) {
    count = 0;
    while(n != 0) {
        n = n&&(n-1); // clear last bit
        count++;
    }
    return count;
}
```

这种算法更高效，因为它只遍历数字二进制表示中的置位位，而不是遍历所有位。例如，如果 `n` 的二进制表示为 `1000000000001`，则只需要两次迭代即可完成计数，而使用之前的算法需要 16 次迭代。这说明算法的选择如何极大影响程序的性能。

## 10.7.5 检查数字是否为 2 的幂

`PowerOfTwo()` 函数接收一个整数 `n` 作为输入，如果数字是 2 的幂则返回 1，否则返回 0。它使用以下条件判断一个数字是否为 2 的幂：

- 数字不应为零 (n != 0)。
- 数字应该只有一个位被设置为 1。这个条件通过对 `n` 和 `n-1` 执行位与操作来检查。如果结果为 0，则意味着 `n` 只有一个位设置为 1。
- 数字的最高位位应该是 0。这个条件通过将数字右移 31 位 (n >> 31) 并与 0 比较来检查。

主程序提示用户输入一个整数，使用 `scanf("%d")` 读取输入，然后调用 `isPowerOfTwo()` 函数判断该数字是否为 2 的幂。根据 `isPowerOfTwo` 的返回值打印相应的消息。

```c
int isPowerOfTwo(int n) {
    return n != 0 && (n & (n-1)) == 0 && (n >> 31) == 0;
}
void main(void) {
    int x;

    printf("enter an integer:\n");
    scanf("%d", &x);
    if(isPowerOfTwo(x)) {
        printf("%d is a power of two\n", x);
    } else {
        printf("%d is not a power of two\n", x);
    }
}
```

## 表 10.2：面向初学者的重要库

| 库 | 描述和关键函数 |
|---|---|
| <stdio.h> | 标准输入输出库，提供控制台、文件和设备 I/O 操作函数，如 `printf()`、`gets()` 和 `feof()`。 |
| <stdlib.h> | 标准库，包含内存分配、转换、排序和实用操作的通用函数，如 `malloc()`、`atoi()`、`rand()` 和 `qsort()`。 |
| <ctype.h> | 字符分类库，用于分类字符（字母、数字、大写字母等），函数如 `isalpha()`、`isdigit()` 和 `isspace()`。 |
| <time.h> | 时间库，用于处理日期、时间和间隔，提供如 `time()`、`localtime()` 和 `difftime()` 函数。 |
| <string.h> | 字符串处理函数，如 `strlen()`、`strcpy()` 和 `strcmp()`。 |
| <malloc.h> | 动态内存分配库，提供在运行时分配和释放内存的函数。 |
| <math.h> | 数学库，提供数学函数，如 `pow()`、`log()` 和 `sinh()`。 |
| <stdbool.h> | 布尔库，定义了 `bool`、`true` 和 `false`。 |

