
```cpp
copy(charList.begin(), lastElem, screen);                 //Line 10
cout << endl;                                             //Line 11

    //remove_if
newLastElem = remove_if(charList.begin(),
                        charList.end(), isupper());       //Line 12
cout << "Line 13: Character list after "
     << "removing the uppercase " << endl
     << "    letters: ";                                  //Line 13
copy(charList.begin(), newLastElem, screen);              //Line 14
cout << endl;                                             //Line 15

int list[10] = {12, 34, 56, 21, 34,
                78, 34, 55, 12, 25};                      //Line 16

vector<int> intList(list, list + 10);                     //Line 17
vector<int>::iterator endElement;                         //Line 18

ostream_iterator<int> screenOut(cout, " ");               //Line 19

cout << "Line 20: intList: ";                             //Line 20
copy(intList.begin(), intList.end(), screenOut);          //Line 21
cout << endl;                                             //Line 22

vector<int> temp1(10);                                    //Line 23

    //remove_copy
endElement = remove_copy(intList.begin(),
                         intList.end(),
                         temp1.begin(), 34);              //Line 24

cout << "Line 25: temp1 list after copying "
     << "all the elements of intList "
     << "and all " << " except 34: ";                     //Line 25
copy(temp1.begin(), endElement, screenOut);               //Line 26
cout << endl;                                             //Line 27

vector<int> temp2(10, 0);                                 //Line 28

    //remove_copy_if
remove_copy_if(intList.begin(), intList.end(),
               temp2.begin(), lessThanOrEqualTo50);       //Line 29

cout << "Line 30: temp2 after copying all the "
     << "elements of intList except all "
     << " numbers less than 50: ";                        //Line 30
copy(temp2.begin(), temp2.end(), screenOut);              //Line 31
cout << endl;                                             //Line 32

return 0;
}

bool lessThanOrEqualTo50(int num)
{
    return (num <= 50);
}
```

## 示例运行

```
Line 6: Character list: A a A B A C D E F A
Line 9: Character list after removing A: a B C D E F
Line 13: Character list after removing the uppercase
        letters: a c e
Line 20: intList: 12 34 56 21 34 78 34 55 12 25
Line 25: temp1 list after copying all the elements of intList
        except 34: 12 56 21 78 55 12 25
Line 30: temp2 after copying all the elements of intList except
        numbers less than 50: 56 78 55 0 0 0 0 0 0 0
```

第2行的语句创建一个 char 类型的 vector（即 charList），并使用第1行创建的数组 charList 初始化 charList。第3行的语句声明两个 vector 迭代器：lastElem 和 newLastElem。第4行的语句声明一个 ostream 迭代器 screen。第6行的语句输出 charList 的值。第8行的语句使用函数 remove 从 charList 中删除所有出现的 'A'。该函数返回一个指针，指向新区间最后一个元素之后的位置，并将其存储在 lastElem 中。第10行的语句输出新区间中的元素。（注意，第10行的语句输出的是区间 charList.begin()...lastElem-1 中的元素。）第12行的语句使用函数 remove_if 从字符列表中删除大写字母，并将函数 remove_if 返回的指针存储在 newLastElem 中。第14行的语句输出新区间中的元素。

第17行的语句创建一个 int 类型的 vector（即 intList），并使用第16行创建的数组 list 初始化 intList。第21行的语句输出 intList 的元素。第24行的语句将 intList 中除 34 之外的所有元素复制到 temp1 中。列表 intList 未被修改。第26行的语句输出 temp1 的元素。第28行的语句创建一个包含 10 个分量的 int 类型 vector（即 temp2），并将 temp2 的所有元素初始化为 0。第29行的语句使用函数 remove_copy_if 复制 intList 中大于 50 的那些元素。第31行的语句输出 temp2 的元素。

## replace、replace_if、replace_copy 和 replace_copy_if 函数

函数 replace 用于将给定范围内某个给定元素的所有出现替换为新值。函数 replace_if 用于将给定范围内满足特定条件的元素值替换为新值。这些函数的原型如下：

```cpp
template <class ForwardItr, class Type >
void replace(ForwardItr first, ForwardItr last,
             const Type& oldValue, const Type& newValue);

template <class ForwardItr, class UnaryPredicate, class Type>
void replace_if(ForwardItr first, ForwardItr last,
                UnaryPredicate op, const Type& newValue);
```

函数 replace 将区间 first...last-1 中所有值等于 oldValue 的元素替换为 newValue 指定的值。函数 replace_if 将区间 first...last-1 中所有满足 op(element) 为 true 的元素替换为 newValue 指定的值。

函数 replace_copy 是 replace 和 copy 的组合。类似地，函数 replace_copy_if 是 replace_if 和 copy 的组合。我们先来看函数 replace_copy 和 replace_copy_if 的原型。

```cpp
template <class ForwardItr, class OutputItr, class Type>
OutputItr replace_copy(ForwardItr first, ForwardItr last,
                       OutputItr destFirst,
                       const Type& oldValue,
                       const Type& newValue);

template <class ForwardItr, class OutputItr,
          class UnaryPredicate, class Type>
OutputItr replace_copy_if(ForwardItr first, ForwardItr last,
                          OutputItr destFirst,
                          UnaryPredicate op,
                          const Type& newValue);
```

函数 replace_copy 将区间 first...last-1 中的所有元素复制到从 destFirst 开始的容器中。如果该区间中某个元素的值等于 oldValue，则将其替换为 newValue。函数 replace_copy_if 将区间 first...last-1 中的所有元素复制到从 destFirst 开始的容器中。如果该区间中任意元素满足 op(element) 为 true，则在目标位置将其值替换为 newValue。这两个函数都返回一个 outputItr（指针），它指向目标位置中最后复制的元素之后的位置。

示例 21-19 中的程序展示了如何使用函数 replace、replace_if、replace_copy 和 replace_copy_if。

### 示例 21-19

```cpp
//STL Functions replace, replace_if, replace_copy, and
//    replace_copy_if

#include <iostream>
#include <cctype>
#include <algorithm>
#include <iterator>
#include <vector>

using namespace std;

bool lessThanOrEqualTo50(int num);

int main()
{
    char cList[10] = {'A', 'a', 'A', 'B', 'A',
                      'C', 'D', 'E', 'F', 'A'};        //Line 1

    vector<char> charList(cList, cList + 10);           //Line 2

    ostream_iterator<char> screen(cout, " ");          //Line 3

    cout << "Line 4: Character list: ";                 //Line 4
    copy(charList.begin(), charList.end(), screen);     //Line 5
    cout << endl;                                        //Line 6

        //replace
    replace(charList.begin(), charList.end(),
            'A', 'Z');                                  //Line 7

    cout << "Line 8: Character list after replacing "
         << "A with Z: " << endl;                       //Line 8
    copy(charList.begin(), charList.end(), screen);     //Line 9
    cout << endl;                                        //Line 10

        //replace_if
    replace_if(charList.begin(), charList.end(),
               isupper, '*');                            //Line 11
    cout << "Line 12: Character list after "
         << "replacing the uppercase " << endl
         << "letters with *: ";                         //Line 12
    copy(charList.begin(), charList.end(), screen);     //Line 13
    cout << endl;                                        //Line 14

    int list[10] = {12, 34, 56, 21, 34,
                    78, 34, 55, 12, 25};               //Line 15

    vector<int> intList(list, list + 10);               //Line 16

    ostream_iterator<int> screenOut(cout, " ");         //Line 17

    cout << "Line 18: intList: ";                       //Line 18
    copy(intList.begin(), intList.end(), screenOut);    //Line 19
    cout << endl;                                        //Line 20

    vector<int> temp1(10);                               //Line 21

        //replace_copy
    replace_copy(intList.begin(), intList.end(),
                 temp1.begin(), 34, 0);                 //Line 22
```
