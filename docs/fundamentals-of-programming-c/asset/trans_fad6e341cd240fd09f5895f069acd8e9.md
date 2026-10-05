

## 12.5. 随机置乱向量

```cpp
/*
 * 返回一个 begin...end - 1 范围内的伪随机数，
 * 包含。如果 begin >= end 则返回 0。
 */
int random(int begin, int end) {
    if (begin >= end)
        return 0;
    else {
        int range = end - begin;
        return begin + rand() % range;
    }
}
/*
 * 随机置乱整数向量。
 * a 是要置乱的向量，n 是它的长度。
 */
void permute(vector<int>& a) {
    int n = a.size();
    for (int i = 0; i < n - 1; i++) {
        // 从当前位置到集合末尾
        // 选择一个伪随机位置
        swap(a[i], a[random(i, n)]);
    }
}
// 测试 permute 函数，该函数随机置乱
// 向量的内容
int main() {
    // 初始化随机生成器种子
    srand(static_cast<int>(time(0)));
    // 创建向量 {1,2,3,4,5,6,7,8}
    vector<int> vec { 1, 2, 3, 4, 5, 6, 7, 8 };

    // 打印之前的向量
    print(vec);
    cout << endl;

    permute(vec);

    // 打印之后的后的向量
    print(vec);
    cout << endl;
}
```

运行列表 12.8 (randompermute.cpp) 一次产生：

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|
| 2 | 7 | 1 | 6 | 4 | 8 | 3 | 5 |

注意列表 12.8 (randomperm.cpp) 中的 `permute` 函数使用了简单的非嵌套循环且没有递归。`permute` 函数将变量 `i` 从 0 变为向量中倒数第二个元素的索引。在循环内部，函数通过 `rand` 获取一个大于或等于 `i` 的伪随机索引。它交换位置 `i` 和随机位置上的元素。此时，索引为 `i` 处的所有元素都较小且不会改变；函数继续执行。循环增加索引 `i`，该过程持续到所有的 `i` 值都被考虑过。

为了确保正确性，`permute` 函数能够生成向量的任何有效排列。重要重要的是，我们的 `permute` 函数能够以等概率产生所有可能的所有排列；换句话说，我们不希望 `permute` 函数生成某些排列的频率比其他排列更高。列表 12.8 (randomperm.cpp) 中的 `permute` 函数是可以的，但请考虑算法的一个轻微变体。

```cpp
// 随机置乱向量？
void faulty_permute(vector<int>& a) {
  int n = a.size();
  for (int i = 0; i < n; i++) {
    // 在向量中选择一个伪随机位置
    swap(a[i], a[rand(0, n)]);
  }
}
```

你看到 `faulty_permute` 和 `permute` 之间的区别了吗？`faulty_permute` 函数从所有有效索引中选择随机索引，而 `permute` 可以在任何循环迭代期间交换向量内任何位置的元素。虽然这种方法看起来和 `permute` 一样好，但它实际上创建了排列的不均匀分布。列表 12.9 (comparepermutations.cpp) 对向量 (1, 2, 3) 的每个排列执行了 1,000,000 次并统计了每个排列次数。这个三元素向量恰好有六种排列。

列表 12.9: comparepermutations.cpp
```cpp
#include <iostream>
#include <vector>
#include <ctime>
#include <cstdlib>

using namespace std;

/*
* 打印 int 向量的内容
* a 是要打印的向量；a 不会被修改
* n 是向量中元素的数量
*/
void print(const vector<int>& a) {
  int n = a.size();
  cout << " ";
  if (n > 0) {
    cout << a[0]; // 打印第一个元素
    for (int i = 1; i < n; i++) {
      cout << ', ' << a[i]; // 打印其余元素
    }
  }
  cout << endl;
}

/*
* 返回一个 begin..end - 1 范围内的伪随机数，
* 如果 begin >= end 则返回 0。
*/
int random(int begin, int end) {
    if (begin >= end)
        return 0;
    else {
        int range = end - begin;
        return begin + rand() % range;
    }
}

/*
* 随机置乱整数向量。
* a 是要置乱的向量，n 是它的长度。
*/
void permute(vector<int>& a) {
    int n = a.size();
    for (int i = 0; i < n - 1; i++) {
        // 从当前位置到集合末尾
        // 选择一个伪随机位置
        swap(a[i], a[random(i, n)]);
    }
}

/* 随机置乱向量？ */
void faulty_permute(vector<int>& a) {
    int n = a.size();
    for (int i = 0; i < n; i++) {
        // 在集合中选择一个伪随机位置
        swap(a[i], a[random(0, n)]);
    }
}

/* 将向量分类为六种排列之一 */
int classify(const vector<int>& a) {
    switch (100*a[0] + 10*a[1] + a[2]) {
        case 123: return 0;
        case 132: return 1;
        case 213: return 2;
        case 231: return 3;
        case 312: return 4;
        case 321: return 5;
    }
    return -1;
}

/* 报告统计数据 */
void report(const vector<int>& a) {
    cout << "1,2,3: " << a[0] << endl;
    cout << "1,3,2: " << a[1] << endl;
    cout << "2,1,3: " << a[2] << endl;
    cout << "2,3,1: " << a[3] << endl;
    cout << "3,1,2: " << a[4] << endl;
    cout << "3,2,1: " << a[5] << endl;
}

/*
 // 用零填充向量。
 // a 是向量，n 是它的长度。
 */
void clear(vector<int>& a) {
  int n = a.size();
  for (int i = 0; i < n; i++)
    a[i] = 0;
}

int main() {
    // 初始化随机生成器种子
    srand(static_cast<int>(time(0)));

    // tally 跟踪每种排列模式
    // tally[0] 计数 (1,2,3)
    // tally[1] 计数 (1,3,2)
    // tally[2] 计数 (2,1,3)
    // tally[3] 计数 (2,3,1)
    // tally[4] 计数 (3,1,2)
    // tally[5] 计数 (3,2,1)
    vector<int> tally(0, 0, 0, 0, 0, 0);

    // original 持有向量 (1,2,3)
    const vector<int> original (1, 2, 3);

    // working 持有 original 的副本并进行置乱
    vector<int> working;

    // 运行排列百万次
    const int RUNS = 1000000;

    cout << "---- 随机排列 #1 ----" << endl;
    clear(tally);
    for (int i = 0; i < RUNS; i++) { // 运行 1,000,000 次
        // 创建 original 的副本
        working = original;
        // 使用第一个算法置乱向量
        permute(working);
        // 计数此排列
        tally[classify(working)]++;
    }
    report(tally);   // 报告结果

    cout << "---- 随机排列 #2 ----" << endl;
    clear(tally);
    for (int i = 0; i < RUNS; i++) { // 运行 1,000,000 次
        // 创建 original 的副本
        working = original;
        // 使用第二个算法置乱向量
        faulty_permute(working);
        // 计数此排列
        tally[classify(working)]++;
    }
    report(tally); // 报告结果
}
```

在列表 12.9 (comparepermutations.cpp) 的输出中，输出 #1 对应于 `permute` 函数，输出 #2 是 `faulty_permute` 函数。列表 12.9 (comparepermutations) 的输出揭示了错误的排列函数倾向于某些排列而非其他：

```
随机排列 #1
1,2,3: 166608
1,3,2: 166820
2,1,3: 166350
2,3,1: 166702
3,1,2: 166489
3,2,1: 167031
随机排列 #2
1,2,3: 168517
1,3,2: 184756
2,1,3: 185246
2,3,1: 185225
3,1,2: 148476
3,2,1: 147980
```

在百万次运行中，`permute` 函数提供的六种排列 ({1, 2, 3}, {2, 1, 3}, {2, 3, 1}) 的均匀分布频率高于排列 ({1, 2, 3}, {3, 1, 2}, {3, 2, 1})。为了了解为什么 `faulty_permute` 行为异常，我们需要检查它在一次调用期间可以产生的所有排列。图 12.5 显示了一个分级结构，映射了 `faulty_permute` 如何为每个 `for` 循环转换其向量参数的内容。树的顶部显示为

![](img/e326304bd50fbc4f7d5a64c1487eb635_346_0.png)

图 12.5：一个映射 `faulty_permute` 在其循环每次迭代中转换向量 1, 2, 3 方式的树

原始向量，{1, 2, 3}。

