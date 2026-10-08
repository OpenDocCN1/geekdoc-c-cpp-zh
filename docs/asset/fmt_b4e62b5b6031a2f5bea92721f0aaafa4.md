
`for (iElement = listNames.begin(); iElement!=listNames.end(); ++iElement)`
`cout << *iElement << " ";`
`cout << endl;`

# 课程 19 答案

## 测验

- 1. 默认排序标准由 `std::less<>` 指定，它实际上使用运算符 `operator<` 来比较两个整数，如果第一个小于第二个，则返回 true。
- 2. 在一起，一个接一个。
- 3. `size()`，与所有 STL 容器一样。

## 练习题

- 1. 二元谓词可以是
```cpp
struct FindContactGivenNumber
{
  bool operator () (const CContactItem& lsh, const CContactItem& rsh)
  {
    return (lsh.strPhoneNumber < rsh.strPhoneNumber);
  }
};
```
- 2. 结构和 `multiset` 的定义将是
```cpp
#include <set>
#include <iostream>
#include <string>
using namespace std;
struct PAIR_WORD_MEANING
{
string strWord;
string strMeaning;
PAIR_WORD_MEANING sequence(const string& sWord, const string& sMeaning)
    : strWord (sWord), strMeaning (sMeaning) {
bool operator< (const PAIR_WORD_MEANING& pairAnotherWord) const
{
    return (strWord < pairAnotherWord.strWord);
}
};
int main()
{
multiset<PAIR_WORD_MEANING> msetDictionary;
PAIR_WORD_MEANING word1("C++", "A programming language");
PAIR_WORD_MEANING word2("Programmer", "A geek");
msetDictionary.insert(word1);
msetDictionary.insert(word2);
```
- 3. 一种解决方案是
```cpp
#include <set>
#include <iostream>
using namespace std;
template <typename T>
void DisplayContent(const T& sequence)
{
    T::iterator iElement;
for (iElement = sequence.begin(); iElement!=sequence.end(); ++iElement)
    cout << *iElement << " ";
}
int main () {
multiset<int> msetIntegers;
msetIntegers.insert(5);
msetIntegers.insert(5);
msetIntegers.insert(5);
set<int> setIntegers;
setIntegers.insert (5);
setIntegers.insert (5);
setIntegers.insert (5);
cout << 'Displaying the contents of the multiset: ';
DisplayContent(msetIntegers);
cout << endl;
cout << 'Displaying the contents of the set: ';
DisplayContent(setIntegers);
cout << endl;
return 0;
}
```

# 课程 20 答案

## 测验

- 1. 默认排序标准由 `std::less<>` 指定。
- 2. 挨在一起。
- 3. `size()`.
- 4. 你不会在 `map` 中找到重复元素！

## 练习题

- 1. 一种允许重复条目的关联容器。例如，`multimap`：
```cpp
std::multimap<string, string>
```
- 2. 允许重复条目的关联容器。
```cpp
struct FPredicate
{
    bool operator<(const wordProperty& lsh, const wordProperty& rsh) const
    {
        return (lsh.strWord < rsh.strWord);
    }
};
```
- 3. 参考课程 19 的提示。

# 课程 21 答案

## 测验

- 1. 二元谓词。
- 2. 它可以被构造。
- 3. 因为所有元素都存在。

## 练习题

- 1. 就像一个 lambda
```cpp
vector<int> setIntegers;
for (int nCount = 0; nCount < 10; ++nCount)
    setIntegers.push_back(nCount);
}
```
- 3. 一种解决方案是：
```cpp
int main () {
    vector<int> setIntegers;
    for (int nCount = 0; nCount < 10; ++nCount)
        setIntegers.push_back(nCount);
    cout << "Displaying the contents of the set: ";
    for (int n : setIntegers)
        cout << n << " ";
    cout << endl;
    return 0;
}
```

## 练习

1. 这里有一个解决方案：
```cpp
struct CaseInsensitiveCompare {
    bool operator()(const string& str1, const string& str2) const {
        string str1Copy(str1), str2Copy(str2);
        transform(str1Copy.begin(), str1Copy.end(), str1Copy.begin(), tolower);
        transform(str2Copy.begin(), str2Copy.end(), str2Copy.begin(), tolower);
        return str1Copy < str2Copy;
    }
};
```
2. 这里是演示。注意 `std::copy()` 如何在不知道集合性质的情况下工作。它仅通过迭代器类工作：
```cpp
#include <vector>
#include <algorithm>
#include <list>
#include <string>
#include <iostream>
using namespace std;
int main () {
    list<string> listNames;
    listNames.push_back("Jack");
    listNames.push_back("John");
    listNames.push_back("Anna");
    listNames.push_back("Skate");
###vector<string> vecNames(4);
    copy(listNames.begin(), listNames.end(), vecNames.begin());
    vector<string>::iterator iNames;
    for (iNames = vecNames.begin(); iNames != vecNames.end(); ++iNames) {
        cout << *iNames << '\n';
    }
    return 0;
}
```
3. `std::sort()` 和 `std::stable_sort()` 的区别在于，后者在排序时确保了对象的相对位置。由于应用程序需要按照事件发生的顺序存储数据，因此你应该选择 `stable_sort()` 来保持天体事件之间的相对顺序不变。

# 第 24 课答案

## 测验

- 1. 是，通过提供一个谓词来实现。
- 2. `Coins` 类需要实现 `operator`。
- 3. 不，你只能对栈顶进行操作。因此你无法访问栈底的硬币。

## 练习

- 1. 二元谓词可以是 `operator`：
```cpp
class Person
{
public:
 int Age;
bool IsFemale;
bool operator< (const Person&anotherPerson) const {
bool bRet = false;
if (Age > anotherPerson.Age)
bRet = true;
else if (IsFemale && anotherPerson.IsFemale)
bRet = true;
  return bRet;
}
};
```
- 2. 只需插入栈中。当你弹出数据时，你实际上反转了内容，因为栈是一种后进先出（LIFO）容器。

# 第 25 课答案

## 测验

- 1. 不。`bitset` 持有的位数在编译时是固定的。
- 2. 因为它不是。它不能像其他容器那样动态扩展扩展；它不支持容器所需的方式的迭代器。
- 3. 不。`std::bitset` 最适合这个目的。

## 练习

- 1. 这里演示了具有实例化、初始化、显示和加法的 `std::bitset`：
```cpp
#include <bitset>
#include <iostream>
int main() {
    // 将 bitset 初始化为 1001
    std::bitset<4> fourBits(9);
    std::cout << "fourBits: " << fourBits << std::endl;
    // 初始化另一个 bitset 为 0010
    std::bitset<4> fourMoreBits(2);
    std::cout << "fourMoreBits: " << fourMoreBits << std::endl;
    std::bitset<4> addResult(fourBits.to_ulong() + fourMoreBits.to_ulong());
    std::cout << "The result of the addition: " << addResult << std::endl;
    return 0;
}
```
- 2. 在前面的示例中对所有的 `bitset` 对象调用 `flip()` 函数：
```cpp
Result.flip();
std::cout << "The result of the flip is: " << addResult << std::endl;
```

# 第 26 课答案

## 测验

- 1. 我会查看 `www.boost.org`。我希望你也这样做！
- 2. 不，通常编写良好（且选择正确）的智能指针不会这样做。
- 3. 当是侵入式时，它们拥有的对象需要持有它；否则，它们可以在自由存储中持有这些信息。
- 4. 列表需要双向遍历，所以它需要是双向链的。

## 练习

- 1. `object->DoSomething ();` 是错误的，因为指针在前面的步骤丢失了对对象的所有权。这将导致崩溃（或某些不愉快的情况）。
- 2. 代码看起来如下：
```cpp
#include <memory>
#include <iostream>
using namespace std;
class Fish
{
public:
    Fish() { cout << "Fish: Constructed!" << endl; }
    ~Fish() { cout << "Fish: Destructed!" << endl; }
};
void Swim(const unique_ptr<Fish>& const) {
    cout << "Fish swims in water" << endl;
}
class Carp : public Fish
}; // 注意：此处修复了原文缺失的括号
void MakeFishSwim(const unique_ptr<Fish>& inFish) {
    inFish->Swim();
}
int main () {
    unique_ptr<Fish> myCarp(new Carp); // 注意这个
    MakeFishSwim(myCarp);
    return 0;
}
```
