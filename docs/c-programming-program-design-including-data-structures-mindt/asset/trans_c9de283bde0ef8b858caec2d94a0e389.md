
```cpp
//reverse_copy
reverse_copy(intList.begin(), intList.end(),
             back_inserter(resultList));                //line 19

cout << "Line 20: resultList: ";                     //line 20
copy(resultList.begin(), resultList.end(),
     screen);                                          //line 21
cout << endl;                                         //line 22

listItr = intList.begin();                            //line 23
listItr++;                                            //line 24
listItr++;                                            //line 25

cout << "Line 26: intList before rotating: ";        //line 26
copy(intList.begin(), listItr.end(), screen);         //line 27
cout << endl;                                         //line 28

//rotate
rotate(intList.begin(), listItr, intList.end());     //line 29

cout << "Line 30: intList after rotating: ";         //line 30
copy(intList.begin(), intList.end(), screen);         //line 31
cout << endl;                                         //line 32

//rotate_copy
resultList.clear();                                   //line 33

rotate_copy(intList.begin(), listItr,
            intList.end(),
            back_inserter(resultList));                //line 34

cout << "Line 35: intList after rotating and "
     << "copying:\n"
     << "\n";                                        //line 35
copy(intList.begin(), intList.end(), screen);         //line 36
cout << endl;                                         //line 37

cout << "Line 38: resultList after rotating "
     << "and copying:\n"
     << "\n";                                        //line 38
copy(resultList.begin(), resultList.end(),
     screen);                                          //line 39
cout << endl;                                         //line 40

resultList.clear();                                   //line 41

rotate_copy(intList.begin(),
            find(intList.begin(), intList.end(), 6),
            intList.end(),
            back_inserter(resultList));                //line 42
cout << "Line 43: resultList after rotating and "
     << "copying:\n"
     << "            ";                         // line 43
copy(resultList.begin(), resultList.end(),
     screen);                                   // line 44
cout << endl;                                   // line 45

return 0;                                       // line 46
}                                               // line 47
```

## 示例运行：

```text
Line 12: intList: 1 3 5 7 9 0 2 4 6 8
Line 16: intList after reversal: 8 6 4 2 0 9 7 5 3 1
Line 20: intList: 1 3 5 7 9 0 2 4 6 8
Line 26: intList before rotating: 8 6 4 2 0 9 7 5 3 1
Line 30: intList after rotating: 4 2 0 9 7 5 3 1 8 6
Line 35: intList after rotating and copying:
         4 2 0 9 7 5 3 1 8 6
Line 38: resultList after rotating and copying:
         0 9 7 5 3 1 8 6 4 2
Line 43: resultList after rotating and copying:
         6 4 2 0 9 7 5 3 1 8
```

## 函数 `count`、`count_if`、`max`、`max_element`、`min`、`min_element` 和 `random_shuffle`

算法 count 统计给定值在给定范围内出现的次数。实现该算法的函数原型如下：

```cpp
template <class InputItr, class T>
iterator_traits<InputItr>::difference_type
        count(InputItr first, InputItr last, const T& value);
```

函数 count 返回参数 `value` 指定的值在范围 `first...last-1` 中出现的次数。

算法 `count_if` 统计给定值在给定范围内满足特定条件的出现次数。实现该算法的函数原型如下：

```cpp
template <class InputItr, class UnaryPredicate>
iterator_traits<InputItr>::difference_type
        count_if(InputItr first, InputItr last, UnaryPredicate Op);
```

函数 count_if 返回范围 `first...last-1` 中使 `op(elem)` 为真的元素个数。

算法 **max** 用于确定两个值中的最大值。它有两种形式，如下列原型所示：

```
template <class Type>
const Type& max(const Type& aVal, const Type& bVal);
```

```
template <class Type, class compare>
const Type& max(const Type& aVal, const Type& bVal, compare comp);
```

第一种形式使用与 **Type** 关联的大于运算符。第二种形式使用由 **comp** 指定的比较操作。

算法 **max_element** 用于确定给定范围内的最大元素。该算法有两种形式，如下列原型所示：

```
template <class forwardItr>
forwardItr max_element(forwardItr first, forwardItr last);
```

```
template <class forwardItr, class compare>
forwardItr max_element(forwardItr first, forwardItr last,
                       compare comp);
```

第一种形式使用与范围 **first...last-1** 中元素的数据类型关联的大于运算符。第二种形式使用由 **comp** 指定的比较操作。两种形式都返回指向范围 **first...last-1** 中最大值的元素的迭代器。

算法 **min** 用于确定两个值中的最小值。它有两种形式，如下列原型所示：

```
template <class Type>
const Type& min(const Type& aVal, const Type& bVal);
```

```
template <class Type, class compare>
const Type& min(const Type& aVal, const Type& bVal, compare comp);
```

第一种形式使用与 **Type** 关联的小于运算符。第二种形式使用由 **comp** 指定的比较操作。

算法 **min_element** 用于确定给定范围内的最小元素。该算法有两种形式，如下列原型所示：

```
template <class forwardItr>
forwardItr min_element(forwardItr first, forwardItr last);
```

```
template <class forwardItr, class compare>
forwardItr min_element(forwardItr first, forwardItr last,
                       compare comp);
```

第一种形式使用与范围 **first...last-1** 中元素的数据类型关联的小于运算符。第二种形式使用由 **comp** 指定的比较操作。两种形式都返回指向范围 **first...last-1** 中最小值的元素的迭代器。

算法 `random_shuffle` 用于随机排列给定范围内的元素。该算法有两种形式，如下列原型所示：

```
template <class randomAccessItr>
void random_shuffle(randomAccessItr first,
                    randomAccessItr last);

template <class randomAccessItr, class randomAccessGenerator>
void random_shuffle(randomAccessItr first, randomAccessItr last,
                    randomAccessGenerator rand);
```

第一种形式使用均匀分布随机数生成器重新排列范围 `first...last-1` 中的元素。第二种形式使用随机数生成函数对象或函数指针重新排列范围 `first...last-1` 中的元素。

示例 21-25 说明了如何使用这些函数。

## 示例 21-25

```cpp
// STL functions count, count_if, min_element,
//                    max_element, random_shuffle

#include <iostream>                              //Line 1
#include <cctype>                                //Line 2
#include <algorithm>                             //Line 3
#include <iterator>                              //Line 4
#include <vector>                                //Line 5

using namespace std;                             //Line 6

void doubleNum(int num);                         //Line 7

int main()                                        //Line 8
{
        vector<char> charList = {'Z', 'a', 'z', 'B', //Line 9
                                 'Z', 'c', 'D', 'e',
                                 'F', 'Z' };        //Line 10

        ostream_iterator<char> screen(cout, " "); //Line 11

        cout << "Line 12: charList: ";          //Line 12
        copy(charList.begin(), charList.end(), screen); //Line 13
        cout << endl;                             //Line 14

        //count
        int noOfZs = count(charList.begin(),
                           charList.end(), 'Z'); //Line 15
```

