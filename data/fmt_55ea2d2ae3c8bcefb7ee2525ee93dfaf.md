
```cpp
elementType operator () (const elementType& elem1,
                         const elementType& elem2)
{
  return (elem1 * elem2);
};
};
```

# 二元函数

# 课程 21：理解函数对象

感兴趣的实现再次位于 `operator()` 中，它接受两个参数并返回它们的积。此类二元函数用于如 `std::transform` 等算法，你可以用它来乘以两个容器的内容。列表 21.5 展示了此类二元函数在 `std::transform` 中的用法。

## 列表 21.5 使用二元函数乘以两个范围

```cpp
0: #include <vector>
1: #include <iostream>
2: #include <algorithm>

3:
4: template <typename elementType>
5: class Multiply
6: {
7: public:
8: elementType operator (const elementType& elem1,
9: const elementType& elem2)
10: {
11: return (elem1 * elem2);
12: }
13: }

14:
15: int main (
16: {
17: using namespace std;

18:
19: // 创建两个包含 10 个元素的整数示例 vector
20: vector <int> vecMultiplicand, vecMultiplier;

21:
22: // 插入示例值 = 0 to 9
23: for (int nCount1 = 0; nCount1 < 10; ++nCount1)
24: vecMultiplicand.push_back(nCount1);

25:
26: // 插入示例值 100 to 109
27: for (int nCount2 = 100; nCount2 < 110; ++nCount2)
28: vecMultiplicand.push_back(nCount2);

29:
30: // 存储乘法结果的第三容器
31: vector <int> vecResult;

32:
33: // 为乘法结果留空间
34: vecResult.resize(10);
35: transform ( vecMultiplicand.begin(), // 乘数范围
36:    vecMultiplicand.end(), // 范围结束
37:    vecMultiplier.begin(), // 乘数值
38:    vecResult.begin(), // 存储结果的范围
39:    Multiply<int>(), // 乘法的函数
40:    cout << "The contents of the first vector are: " << endl;
41:    for (size_t nIndex = 0; nIndex < vecMultiplicand.size(); ++nIndex)
42:        cout << vecMultiplicand[nIndex] << ' ';
43:    cout << endl;
44:    cout << "The contents of the second vector are: " << endl;
45:    for (size_t nIndex = 0; nIndex < vecMultiplier.size(); ++nIndex)
46:        cout << vecMultiplier[nIndex] << ' ';
47:    cout << endl;
48:    cout << "The contents of the multiplication is: " << endl;
49:    for (size_t nIndex = 0; nIndex < vecResult.size(); ++nIndex)
50:        cout << vecResult[nIndex] << ' ';
51:    return 0;
52: }
```

### 输出

第一个 vector 的内容是：
0 1 2 3 4 5 6 7 8 9 
第二个 vector 的内容是：
乘法的结果是：

### 分析
（此处由于用户提供的文本在 Output 之后截断，我仅翻译了提供的部分）
