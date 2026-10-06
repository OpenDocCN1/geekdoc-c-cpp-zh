

# 10.4 STL 中的算法 — 433

这里是这些算法的示例：

示例 10.11：实际排序算法的示例。

```cpp
//10_11.cpp
#include <iostream>
#include <algorithm>
#include <functional>
#include <vector>
using namespace std;

int main()
{
    int iarray[]={26,17,15,22,23,33,32,40};
    vector<int> ivector(iarray,iarray+sizeof(iarray)/sizeof(int));

    // 并输出最大元素和最小元素
    cout<<max_element(ivector.begin(),ivector.end())<<endl;
    cout<<min_element(ivector.begin(),ivector.end())<<endl;

    // 排序 ivector.begin()+4 和
    // ivector.begin() 之间的元素，将结果放入区间
    // [ivector.begin(),ivector.begin()+4]。不保证
    // 剩余元素的顺序会被保持。
    partial_sort(ivector.begin(),ivector.begin()+3,ivector.end());
    copy(ivector.begin(),ivector.end(),ostream_iterator<int>(cout, " "));
    cout<<endl;

    // 本地排序并将结果拷贝到另一个地方
    vector<int> ivector1(5);
    partial_sort(ivector.begin(),ivector.end(),ivector1.begin(),
    ivector1.end());
    copy(ivector1.begin(),ivector1.end(),ostream_iterator<int>(cout, " "));
    cout<<endl;

    // 排序，使用升序作为默认排序
    sort(ivector.begin(),ivector.end());
    copy(ivector.begin(),ivector.end(),ostream_iterator<int>(cout, " "));
    cout<<endl;

    // 元素的插入不会影响最小元素
    // 和最大元素的位置

    cout<<lower_bound(ivector.begin(),ivector.end(),24)<<endl;
    cout<<upper_bound(ivector.begin(),ivector.end(),24)<<endl;

    // 使用二分查找在有序区间内查找一个元素
    cout<<binary_search(ivector.begin(),ivector.end(),33)<<endl;
    cout<<binary_search(ivector.begin(),ivector.end(),34)<<endl;

    // 获取下一个排列
    next_permutation(ivector.begin(),ivector.end());
    copy(ivector.begin(),ivector.end(),ostream_iterator<int>(cout, ""));
    cout<<endl;

    // 获取上一个排列
    prev_permutation(ivector.begin(),ivector.end());
    copy(ivector.begin(),ivector.end(),ostream_iterator<int>(cout, ""));
    cout<<endl;

    // 合并两个序列 ivector 和 ive1，将结果放入
    // vector2
    vector<int> ivector2(13);
    merge(ivector.begin(),ivector.end(),ivector1.begin(),ivector1.end(),
    ivector2.begin());
    copy(ivector2.begin(),ivector2.end(),ostream_iterator<int>(cout, ""));
    cout<<endl;

    // 将所有小于 *(ivector.begin()+5) 的元素放在
    // 左侧，将其他元素放在它的右侧。操作过程中
    // 不保证相对顺序会被保持。
    nth_element(ivector2.begin(),ivector2.begin()+5,ivector2.end());
    copy(ivector2.begin(),ivector2.end(),ostream_iterator<int>(cout, ""));
    cout<<endl;

    // 排序并保持相对顺序
    stable_sort(ivector2.begin(),ivector2.end());
    copy(ivector2.begin(),ivector2.end(),ostream_iterator<int>(cout, ""));
    cout<<endl;

    // 在有序区间内查找子区间，确保子区间内
    // 的所有元素都等于一个指定的值
    pair<vector<int>::iterator, vector<int>::iterator> pairIter;
    pairIter=equal_range(ivector2.begin(),ivector2.end(),22);
    cout<<(pairIter.first)<<endl;
    cout<<(pairIter.second)<<endl;

    // 合并两个有序序列并替换原始序列
    int iarray3[] = { 1, 3, 5, 7, 2, 4, 6, 8 };
    vector<int> ivector3(iarray3,iarray3+sizeof(iarray3)/sizeof(iarray3));
    inplace_merge(ivector3.begin(),ivector3.begin()+4,
```

## 10.4.5 数值算法

有四个通用的数值算法；表 10.7 列出了 STL 中的数值算法。

这里是这些算法的示例：

示例 10.12：数值算法的示例。

```cpp
//10_12.cpp
#include <iostream>
#include <numeric>
#include <functional>
#include <vector>
using namespace std;

int main() {
    int iarray[]={1,2,3,4,5};
    vector<int> ivector(iarray,iarray+sizeof(iarray)/sizeof(iarray));

    // 累加
    cout<<accumulate(ivector.begin(),ivector.end(),0)<<endl;

    // 内积
    cout<<inner_product(ivector.begin(),ivector.end(),ivector.begin(),0)<<endl;

// 差分
    adjacent_difference(ivector.begin(),ivector.end(), ostream_iterator<int>(cout, " "));

// 相邻求和
    cout << partial_sum(ivector.begin(),ivector.end()) << endl;
}
```

表 10.7：数值算法

| 名称 | 描述 |
| :--- | :--- |
| accumulate | 计算范围内元素的和 |
| inner_product | 计算两个对应元素乘积的和 |
| adjacent_difference | 计算相邻元素之间的差 |
| partial_sum | 返回相邻元素和的序列 |

