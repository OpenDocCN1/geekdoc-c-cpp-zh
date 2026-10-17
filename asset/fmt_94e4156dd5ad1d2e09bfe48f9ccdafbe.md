
```cpp
class RMQ {                               // 区间最小查询

private:

    int _A[MAX_N], SpT[MAX_N][LOG_TWO_N];

public:

    RMQ(int n, int A[]) {                   // 构造函数以及预处理

        for (int i = 0; i < n; i++) {

            _A[i] = A[i];                // 从索引 i 开始长度为 2^0

        }

        // 两个嵌套循环的总复杂度为 O(n log n)

        for (int j = 1; (1 << j) <= n; j++) // 对于每个满足 2^j <= n 的 j
            for (int i = 0; i < n - (1 << j); i++) { // 对于每个有效的 i，O(log n)
                if (SpT[i][j-1] < SpT[i + (1 << (j-1))][j-1]) { // RMQ
                    SpT[i][j] = SpT[i][j-1];     // 从索引 i 开始长度为 2^j
                } else
                    SpT[i][j] = SpT[i + (1 << (j-1))][j-1]; // 从索引 i+2^(j-1) 开始长度为 2^j
            }

    }

    int query(int i, int j) {                   // 此查询为 O(1)
        int k = (int)floor(log2((double)j-i+1));   // 2^k <= j-i+1
        if (SpT[i][k] <= SpT[j - (1 << k)][k]) return SpT[i][k];
        else
            return SpT[j - (1 << k)][k];
    }

};
```

源码：`SparseTable.java`

对于测试用例 `$n=7$` 且 `$A = \{18, 17, 13, 19, 15, 11, 20\}$`（如 2.4.3 所示），稀疏表 `SpT` 的内容如下：

| index | 0 | 1 | 2 |
| :--- | :--- | :--- | :--- |
| 0 | 18 | 13 | 11 |
| 1 | 17 | 13 | 11 |
| 2 | 13 | 13 | 11 |
| 3 | 19 | 15 | 11 |
| 4 | 15 | | |
| 5 | 11 | | |
| 6 | 20 | | |

在第一列中，`j = 0` 表示从索引 `i` 开始长度为 `2^0 = 1` 的数组的 RMQ，我们 `SpT[i][j] = i`。
在第二列中，`j = 1` 表示从索引 `i` 开始长度为 `2^1 = 2` 的数组的 RMQ。注意最后一行是空的。
在第三列中，`j = 2` 表示从索引 `i` 开始长度为 `2^2 = 4` 的数组的 RMQ。注意最后三行是空的。

# 汉诺塔 (Tower of Hanoi)

## 问题描述

问题的经典描述如下：有三个柱子 `A`, `B` 和 `C`，以及 `n` 个盘子，所有盘子的大小不同。从所有盘子按升序堆叠在一个柱子上（`A`）开始，你的任务是将所有 `n` 个盘移动到另一个柱子上（`C`）。任何盘子不能放在比它小的盘子上面，且每次只能从一个柱子移动一个盘子到另一个。

## 解决方案

经典的汉诺塔问题存在简单的递归回溯解。将 `n` 个盘从 `A` 移动到 `C` 并使用额外的 `B` 作为中间柱可以分解为以下子问题：

- 1. 以 `C` 为中间柱，将 `n-1` 个盘从 `A` 移动到 `B`。在这个递归步骤后，我们在 `A` 上留下了盘子 `n`。
- 2. 将盘子 `n` 从 `A` 移动到 `C`。
- 3. 以 `A` 为中间柱，将 `n-1` 个盘从 `B` 移动到 `C`。

这 `n-1` 个盘将放在盘子 `n` 之上，而 `n` 现在位于 `C` 的底部。

注意步骤 1 和 3 是递归步骤。基础情况是 `n=1`，此时我们只需将单个盘子从当前的源柱子移动到目的地，跳过中间柱子。示例 C++ 实现代码 `Implementation` 所示：

```cpp
#include <iostream>
#include <cstdio>
using namespace std;

void solve(int count, char source, char destination, char intermediate) {
    if (count == 1)
        printf("Move top disc from pole %c to pole %c\n", source, destination);
    else {
        solve(count-1, source, intermediate, destination);
        solve(1, source, destination, intermediate);
        solve(count-1, intermediate, destination, source);
    }
}

int main() {
    solve(3, 'A', 'C', 'B'); // 为第一个参数尝试更大的值
    return 0;
}
```
