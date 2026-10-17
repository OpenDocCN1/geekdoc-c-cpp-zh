
```cpp
totalvalue = 0;

for(int i=0; i < N; i++) {
    if(bs[i]) { totalweight += w[i]; totalvalue += v[i]; }
}

cout << "totalweight = " << totalweight << " totalvalue = " << totalvalue << endl;
}
```

输出字符串 `bh=10011110` 从左到右从 0 开始。这些物品是：
- 2 换洗衣物
- 4 睡袋
- 5 干粮
- 6 救救包
- 7 驱蚊剂
- 8 手电筒
- 11 水净化器

解决方案的一个有趣方面是背包问题并不直接受重量限制。背包可以装满 20 公斤。例如，替换换洗衣物会减少总价值。背包问题也可以使用动态规划解决。考虑以下具有三个物品的问题：

假设背包的容量为 5。我们可以添加超过一次物品。让 `$w$` 索引阶段表示携带的重量。决策是确定带入 `$w=5$` 的最后一个物品。令 `f(w)` 为从 `w` 获取的最大收益。对于物品 `j`，以下关系是 `f(w) = max {v_j + f(w - w_j)}`，`1 <= j <= 3`：

| 物品 (j) | 重量 (`w_j`) | 价值 (`v_j`) |
|---|---|---|
| 1 | 2 | 65 |
| 2 | 3 | 80 |
| 3 | 1 | 30 |

如果我们添加物品 `j`，得到一个大小为 `w - w_j` 的背包。因此我们有 `f(w=0) = 0` 且 `f(w=1) = 30`。得出：
`f(w=2) = max {65 + f(0), 30 + f(1)} = 65`
`f(w=3) = max {65 + f(1), 80 + f(0), 30 + f(2)} = 95`
`f(w=4) = max {65 + f(2), 80 + f(1), 30 + f(3)} = 130`
`f(w=5) = max {65 + f(3), 80 + f(2), 30 + f(4)} = 160`

这得出了 160 的最大价值，通过添加 2 个重量为 65 的物品 1 和 1 个重量为 1 价值为 30 的物品 3 。

### 14.9.3 旅行员问题

旅行员问题是一个组合优化问题。许多像旅行员这样的组合优化问题可以这样表述：令 `π = {i_1, i_2, …, i_n}` 是集合 `{1, 2, …, n}` 的一个排列。排列的数量为 `n!`。令 `Ω` 为可行解集，`f(π)` 为最优性函数。有找到找到使得

`π* = {i_1*, i_2*, …, i_n*} = arg{f(π) | π ∈ Ω}`。

`Ω` 的结构和 `f(π)` 取决于考虑的问题。一个典型问题是旅行员问题。给定给定数量城市之间的距离，目标是找到访问每个城市一次并回到起点的最短路径。有几个与旅行员问题等价的问题。该问题具有实际意义。所有可能的路径数量是有限的，因此问题是可解决的。然而，暴力策略仅适用于数量较少的 `n`，因为可能的数量随 `n` 阶乘增长。旅行员问题是整个被称为 NP 完全（或 NP 困难）的问题类的示例，这使其在理论上特别引人入胜。NP 完全问题可以相互转换，并且解决其中任何一个计算时间增长速度快于问题规模的任何次方。有观点认为多项式算法可能根本不存在。计算的目标是找到近优解。

以下 C++ 程序找到数字 `1, 2, …, n` 的所有排列。我们选择 `n=3`。

```cpp
// permutation.cpp
#include <iostream>
using namespace std;
int main(void)
{
    int i, j, t;
    unsigned long n = 3;
    int* p = new int[n+1];
    // 起始排列 1,2,...,n -> 1,2,...,
    for(i=0;i<n;i++) {
        p[i] = i; cout << "p" << i << " = " << p[i] << " ";
    }
    cout << endl;
    int test = 1;
    do {
        i = n-1;
        while(p[i] > p[i+1]) i = i-1;
        if(i > 0) test = 1; else test = 0;
        j = n;
        while(p[j] <= p[i]) j=j-1;
        t = p[i]; p[i] = p[j]; p[j] = t; i = i+1; j = n;
        while(i < j) {
            t = p[i]; p[i] = p[j]; p[j] = t; i = i+1; j = j-1;
        }
        // 显示结果
        for(int tau=0;tau<n;tau++)
            cout << "p" << tau << " = " << p[tau] << " ";
        cout << endl;
    } while(test==1);
    delete[] p;
    return 0;
}
```

现在我们可以利用这个 C++ 程序通过查看所有可能的排列来解决旅行员问题。

```cpp
// permcities.cpp
#include <iostream>
#include <cmath>
using namespace std;
int main(void)
{
    unsigned long n = 7;
    double* x = new double[n+1]; double* y = new double[n+1];
    x[0] = 10.1; y[0] = 20.2; x[1] = 4.0; y[1] = 7.0;
    x[2] = 0.1; y[2] = 2.0; x[3] = 0.5; y[3] = 10.7;
}
```

`x[4] = 10.5; y[4] = 0.6; x[5] = 8.0; y[5] = 10.0;`
`x[6] = 12.0; y[6] = 16.0; x[7] = 18.0; y[7] = 8.0;`
`double d = 0.0;`

```cpp
// distance of 0->1->2->..->n->0
for(int s=0; s<n; s++) {
    d += sqrt((x[s]-x[s+1])*(x[s]-x[s+1])+(y[s]-y[s+1])*(y[s]-y[s+1]));
    d += sqrt((x[n]-x[0])*(x[n]-x[0])+(y[n]-y[0])*(y[n]-y[0]));
    cout << "d = " << d << endl;
}
int i, j, k, t;
int* p = new int[n+1];
// permutation identity 1,2,...,n -> 1,2,...,n
for(i=0;i<n; i++) {
    p[i] = i; cout << "p[" << i << "] = " << p[i] << " ";
}
cout << endl;
int test = 1;
do {
    i = n-1;
    while(p[i] > p[i+1]) i = i-1;
    if(i > 0) test = 1; else test = 0;
    j = n;
    while(p[j] <= p[i]) j=j-1;
    t = p[i]; p[j] = p[j]; p[j] = t; i = i+1; j = n;
    while(i < j) {
        t = p[i]; p[j] = p[j]; p[j] = t; i = i+1; j = j-1;
    }
    // display result
    for(int tau=0;tau<n; tau++) {
        cout << "p[" << tau << "] = " << p[tau] << " ";
    }
    cout << endl;
} while(test==1);
d = sqrt((x[p[0]]-x[p[1]])*(x[p[0]]-x[p[1]])+(y[p[0]]-y[p[1]])*(y[p[0]]-y[p[1]]));
for(int l=1;l<n; l++) {
    d += sqrt((x[p[l]]-x[p[l+1]])*(x[p[l]]-x[p[l+1]])+(y[p[l]]-y[p[l+1]])*(y[p[l]]-y[p[l+1]]));
}
d += sqrt((x[p[n]]-x[0])*(x[p[n]]-x[0])+(y[p[n]]-y[0])*(y[p[n]]-y[0]));
cout << "d = " << d << endl;
delete[] p;
return 0;
```

## 14.9 带有约束的问题

给出了实现 Durstenfeld 算法用于随机打乱一维整数数组的 C++ 程序：

// Durstenfeld.cpp

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;
int main(void)
{
  srand((unsigned long) time(NULL)); // 种子
  unsigned long N = 4;
  int* a = new int[N];
  a[0] = 2; a[1] = 3; a[2] = 7; a[3] = 11;
  unsigned long j;
  for(unsigned long i=N-1;i>1;i--) {
      j = rand()%(i+1); 
      int temp = a[i]; 
      a[i] = a[j]; 
      a[j] = temp;
  }
  for(unsigned long k=0;k<N;k++)
    cout << a[k] << endl;
  delete[] a;
  return 0;
}
```

Goldberg 和 Lingle [85] 建议了一种交叉算子，称为部分映射交叉（partially mapped crossover）。他们认为这将导致旅行商问题的高效求解。我们通过一个例子来解释部分映射算子是如何工作的。假设我们有 12 个城市，并假设父母为：

a1: (1 2 3 4 5 6 7 8 9 10 11 12)
a2: (7 3 6 11 4 12 5 2 10 9 1 8)

a1 和 a2 是数组。位置从 0 到 `$n-1$`计数，其中 `n=12`。我们选择两个随机数 `r1` 和 `r2`。

> `0 <= r1 <= (n-1)`, `0 <= r2 <= (n-1)`, `r1 <= r2`

令 `r1=3, r2=6`。使用 `r1` 和 `r2` 追踪父母：

(1 2 3 | 4 5 6 7 | 8 9 10 11 12)
(7 3 6 | 11 4 12 5 | 2 10 9 1 8)

我们得到子数组 `s1=(4 5 6 7)` 和 `s2=(11 4 5)`。接下来某些城市在新数组中出现两次，而另一些缺失。交叉定义了映射：

- 11 -> 4, 4 -> 5, 12 -> 6, 5 -> 7 (*)
- 4 -> 11, 5 -> 4, 6 -> 12, 7 -> 5 (**)

必须固定的位置由 `x` 表示：

(1 2 3 11 4 12 5 | 8 9 10 x)
(3 x 4 5 6 7 | 2 10 9)

使用映射 (*) 固定数组：
- 位置 10 的 11 必须固定：映射 11 到 4，但 4 已经在 `s2` 中了。
- 位置 4 的 4 必须固定：映射 4 到 5，但 5 已经在 `s2` 中了。
- 位置 5 的 5 必须固定：映射 5 到 7，但 7 不在 `s2` 中。
因此将位置 10 的 11 替换为 7。
- 位置 11 的 12 必须固定：映射 12 到 6，但 6 不在 `s2` 中。
因此将位置 11 的 12 替换为 6。
- 位置 0 的 7 必须固定：映射 7 到 5，但 5 已经在 `s1` 中了。
- 位置 1 的 5 必须固定：映射 5 到 4，但 4 已经在 `s1` 中了。
- 位置 2 的 4 必须固定：映射 4 到 11，但 11 不在 `s1` 中。
因此将位置 0 的 7 替换为 11。
- 位置 2 的 6 必须固定：映射 6 到 12，但 12 不在 `s1` 中。
因此将位置 2 的 6 替换为 12。

结果，孩子为：
(1 2 3 11 4 12 5 8 9 10 7 6)
(11 3 4 5 6 7 2 10 9)

Backov [10] 提出了另一种使用置换的交叉。我们通过一个例子和一个 C++ 程序说明该算子。假设我们有 10 个城市。设父母：
(0 1 2 3 4 5 6 7 8 9) -> (8 7 3 4 5 6 0 2 9 1)

```cpp
// tspermutation.cpp
#include <iostream>
using namespace std;
void crossing(int* a1, int* a2, int* a3, int* a4, int n) {
    for(int i=0; i<n; i++) {
        int p = a1[i];
        a3[i] = a2[p];
    }
    for(int j=0; j<n; j++) {
        int q = a2[j];
        a4[j] = a1[q];
    }
}
int main(void) {
    int n = 10;
    int* a1 = new int[n]; int* a2 = new int[n];
    int* a3 = new int[n]; int* a4 = new int[n];
    a1[0] = 8; a1[1] = 7; a1[2] = 3; a1[3] = 4; a1[4] = 5;
    a1[5] = 6; a1[6] = 0; a1[7] = 2; a1[8] = 1; a1[9] = 9;
    a2[0] = 7; a2[1] = 6; a2[2] = 0; a2[3] = 1; a2[4] = 2;
    a2[5] = 9; a2[6] = 8; a2[7] = 4; a2[8] = 3; a2[9] = 6;
    crossing(a1, a2, a3, a4, n);
    for(int i=0; i<n; i++) {
        cout << "a3[" << i << "] = " << a3[i] << " ";
        if((i+1)%2==0) cout << endl;
    }
    for(int j=0; j<n; j++) {
        cout << "a4[" << j << "] = " << a4[j] << " ";
        if((j+1)%2==0) cout << endl;
    }
    delete[] a1; delete[] a2; delete[] a3; delete[] a4;
    return 0;
}
```

# 第 14 章 遗传算法

在下面的程序 `tsp.cpp` 中，我们使用这些算子来寻找旅行商问题的解决方案。给定的是 8 个城市及其在平面 `R^2` 中的位置。

```cpp
// tsp.cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <cmath>
#include <bitset>
using namespace std;
double distance(int *seq, int ncities, double **dist) {
    double sum = 0.0;
    for(int i=0; i<ncities-1; i++) { sum += dist[seq[i]][seq[i+1]]; }
    sum += dist[seq[ncities-1]][seq[0]];
    return sum;
}
void setupfarm(int **farm, int N, unsigned int ncities) {
    const unsigned int nc = 8;
    bitset<nc> used;
    int city, i, j;
    srand(time(NULL));
    for(i=0; i<N; i++)
        for(j=0; j<ncities; j++) used.set(j);
}
// ... (rest of implementation)
```

# 第 14 章 遗传算法

```cpp
for(i=0;i<ncities;i++)
{
  if(i<pos1 || (i>=pos2))
    while((pos = insequence(child1[i],child1,pos,pos2)) >= 0)
      child1[i] = child2[pos];
  if(i<pos1 || (i>=pos2))
```
