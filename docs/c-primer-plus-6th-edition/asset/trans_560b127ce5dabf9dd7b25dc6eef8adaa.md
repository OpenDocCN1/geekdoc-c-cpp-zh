

# STL 与 string 类

`string` 类虽然不是 STL 的一部分，但其设计时考虑了 STL。例如，它拥有 `begin()`、`end()`、`rbegin()` 和 `rend()` 成员函数。因此，它可以使用 STL 接口。列表 16.17 使用 STL 展示了你可以从单词的字母中形成的所有排列组合。排列是容器中元素的重新排列。`next_permutation()` 算法将范围内的内容转换为下一个排列；对于字符串来说，这些排列是按字母升序排列排列的。如果算法执行成功，它返回 `true`；如果该范围已经是最终序列，它则返回 `false`。要获取范围的所有排列，你应该从最早可能的顺序开始元素，而程序使用了 STL 的 `sort()`。

列表 16.17 strstl.cpp

```cpp
// strstl.cpp -- 将 STL 应用于字符串
#include <iostream>
#include <string>
#include <algorithm>

int main() {
    using namespace std;
    string letters;
    cout << "Enter the letter grouping (quit to quit): ";
    while (cin >> letters && letters != "quit") {
        cout << "Permutations of " << letters << endl;
        sort(letters.begin(), letters.end());
        do {
            cout << letters << endl;
        } while (next_permutation(letters.begin(), letters.end()));
        cout << "Enter next sequence (quit to quit): ";
    }
    cout << "Done.\n";
    return 0;
}
```

这里是列表 16.17 中程序的示例运行：

Enter the letter grouping (quit to quit): awl
Permutations of awl
aw
awl
law
lwa
wal
wla
Enter next sequence (quit to quit): all
Permutations of all
all
lal
lla
Enter next sequence (quit to quit): quit
Done.

注意，`next_permutation()` 算法会自动仅提供唯一的排列，这就是为什么输出中单词 `aul` 和单词 `all` 显示了更多的排列，因为后者包含重复的字母。

# 函数对象（又称仿函数 Functors）

## 函数与容器方法

有时你可以在 STL 方法和 STL 函数之间进行选择。通常情况下，方法是更好的选择。首先，它应该针对特定容器经过更好的优化。其次，作为成员函数，它可以使用模板类的内存管理事实，并在需要时调整容器的大小。

假设例如，你有一个数字列表，并想从列表中删除某个值（例如 4）的所有实例。如果 `la` 是一个 `list<int>` 对象，你可以使用 `la.remove(4);`
`// 从列表中删除所有 4`

在调用此方法后，所有值为 4 的元素都已从列表中删除，并且列表会自动调整大小。还有一个名为 `remove()` 的 STL 算法（参见附录 G）。它不是由对象调用的，而是接收范围参数。如果 `lb` 是一个 `list<int>` 对象，调用该函数看起来如下所示：
`remove(lb.begin(), lb.end(), 4);`

然而，由于 `remove()` 不是成员函数，它不能调整列表的大小。相反，它确保所有未被删除的项都在列表的开头，并返回一个指向末尾之后元素的迭代器。你可以使用这个迭代器来修复列表的大小。例如，你可以使用 `erase()` 方法来移除描述列表中不再需要的部分的范围。列表 16.18 展示了这是如何工作的。

列表 16.18 listrmv.cpp

```cpp
// listrmv.cpp -- 将 STL 应用于字符串
#include <iostream>
#include <list>
#include <algorithm>
```

# 第 16 章 string 类与标准模板库

```cpp
void Show(int);
const int LIM = 10;
int main()
{
  using namespace std;
  int ar[LIM] = {4, 5, 4, 2, 3, 4, 8, 1, 4};
  list<int> la(ar, ar + LIM);
  list<int> lb(la);
  cout << "Original list contents:\n\t";
  for_each(la.begin(), la.end(), Show);
  cout << endl;
  la.remove(4);
  cout << "After using the remove() method:\n\t";
  cout << "la:\n";
  for_each(la.begin(), la.end(), Show);
  cout << endl;
  list<int>::iterator last;
  last = remove(lb.begin(), lb.end(), 4);
  cout << "After using the remove() function:\n\t";
  cout << "lb:\n\t";
  for_each(lb.begin(), lb.end(), Show);
  cout << endl;
  lb.erase(last, lb.end());
  cout << "After using the erase() method:\n\t";
  cout << "lb:\n\t";
  for_each(lb.begin(), lb.end(), Show);
  cout << endl;
  return 0;
}
```

```cpp
void Show(int v)
{
  std::cout << v << " ''";
}
```

这里是列表 16.18 中程序的输出。

Original list contents:
4 5 4 2 3 4 8 1 4
After using the remove() method:
la:
4 5 2 3 8 1
After using the remove() function:
lb:	4 5 2 3 8 1
After using the erase() method:
lb:	4 5 2 3 8 1

