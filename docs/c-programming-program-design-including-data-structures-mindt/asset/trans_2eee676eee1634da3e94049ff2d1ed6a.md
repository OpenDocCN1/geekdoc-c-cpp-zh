
## 示例运行：

```text
Line 13: Character list: A a A B A c D e F A
Line 17: Character list after removing A: a B c D e F
Line 21: Character list after removing the uppercase
          letters: a c e
Line 27: intList: 12 34 56 21 34 78 34 55 12 25
Line 32: temp1 list after copying all the elements of intList
          except 34: 12 56 21 78 55 12 25
Line 37: temp2 after copying all the elements of intList except
          numbers less than 50: 56 78 55 0 0 0 0 0 0 0
```

第10行的语句创建`char`并初始化vector对象`charList`。第11行的语句声明两个vector迭代器：`lastElem`和`newLastElem`。第12行的语句声明一个ostream迭代器`screen`。第14行的语句输出`charList`的值。第16行的语句使用函数`remove`从`charList`中删除所有出现的`'A'`。该函数返回一个指向新范围最后一个元素之后位置的指针，该指针存储在`lastElem`中。第18行的语句输出新范围内的元素。（注意，第18行的语句输出范围`charList.begin()...lastElem-1`内的元素。）第20行的语句使用函数`remove_if`从列表`charList`中删除大写字母，并将函数`remove_if`返回的指针存储在`newLastElem`中。第22行的语句输出新范围内的元素。

第24行的语句创建并初始化vector对象`intList`。第28行的语句输出`intList`的元素。第31行的语句将`intList`中除34以外的所有元素复制到`temp1`中。列表`intList`未被修改。第33行的语句输出`temp1`的元素。第35行的语句创建一个包含10个`int`类型分量的vector `temp2`，并将`temp2`的所有元素初始化为0。第36行的语句使用函数`remove_copy_if`复制`intList`中大于50的那些元素。第38行的语句输出`temp2`的元素。

## 函数 replace、replace_if、replace_copy 和 replace_copy_if

函数`replace`用于将给定范围内给定元素的所有出现替换为新值。函数`replace_if`用于将给定范围内满足特定条件的元素值替换为新值。这些函数的原型如下：

```cpp
template <class ForwardItr, class Type>
void replace(ForwardItr first, ForwardItr last,
             const Type& oldValue, const Type& newValue);

template <class forwardItr, class unaryPredicate, class Type>
void replace_if(forwardItr first, forwardItr last,
                unaryPredicate op, const Type& newValue);
```

函数`replace`将范围`first...last-1`中所有值等于`oldValue`的元素替换为`newValue`指定的值。函数`replace_if`将范围`first...last-1`中所有满足`op(element)`为`true`的元素替换为`newValue`指定的值。

函数`replace_copy`是`replace`和`copy`的组合。类似地，函数`replace_copy_if`是`replace_if`和`copy`的组合。让我们先看一下函数`replace_copy`和`replace_copy_if`的原型。

```cpp
template <class forwardItr, class outputItr, class Type>
outputItr replace_copy(forwardItr first, forwardItr last,
                       outputItr destFirst,
                       const Type& oldValue,
                       const Type& newValue);
```

```cpp
template <class forwardItr, class outputItr,
          class unaryPredicate, class Type>
outputItr replace_copy_if(forwardItr first, forwardItr last,
                          outputItr destFirst,
                          unaryPredicate op,
                          const Type& newValue);
```

函数`replace_copy`将范围`first...last-1`中的所有元素复制到从`destFirst`开始的容器中。如果该范围中某个元素的值等于`oldValue`，则将其替换为`newValue`。函数`replace_copy_if`将范围`first...last-1`中的所有元素复制到从`destFirst`开始的容器中。如果对于该范围中的任何元素，`op(element)`为`true`，则在目标位置将其值替换为`newValue`。这两个函数都返回一个`outputItr`（指针），它指向目标位置最后复制元素之后的位置。

示例21-20中的程序展示了如何使用函数`replace`、`replace_if`、`replace_copy`和`replace_copy_if`。

### 示例 21-20

```cpp
//STL functions replace, replace_if, replace_copy, and
//                 replace_copy_if

#include <iostream>                                      //line 1
#include <cctype>                                        //line 2
#include <algorithm>                                     //line 3
#include <iterator>                                      //line 4
#include <vector>                                        //line 5

using namespace std;                                     //line 6

bool lessThanEqualTo50(int num);                         //Line 7

int main()                                               //Line 8
{
    vector<char> charList = {'A', 'a', 'A', 'B', 'A',
                             'c', 'D', 'e', 'F', 'A'};   //Line 10

    ostream_iterator<char> screen(cout, " ");            //Line 11

    cout << "Line 12: Character list: ";                 //Line 12
    copy(charList.begin(), charList.end(), screen);       //Line 13
    cout << endl;                                         //Line 14

    //replace
    replace(charList.begin(), charList.end(),
            'A', 'Z');                                    //Line 15

    cout << "Line 16: Character list after "
         << "replacing A with Z: " << endl
         << "        ";                                  //Line 16
    copy(charList.begin(), charList.end(), screen);       //Line 17
    cout << endl;                                         //Line 18

    //replace_if
    replace_if(charList.begin(), charList.end(),
               isupper, '*');                             //Line 19

    cout << "Line 20: Character list after "
         << "replacing the uppercase " << endl
         << "        letters with *: ";                   //Line 20
    copy(charList.begin(), charList.end(), screen);       //Line 21
    cout << endl;                                         //Line 22

    vector<int> intList = {12, 34, 56, 21, 34,
                           78, 34, 55, 12, 25};           //Line 23

    ostream_iterator<int> screenOut(cout, " ");           //Line 24

    cout << "Line 25: intList: ";                         //Line 25
    copy(intList.begin(), intList.end(), screenOut);      //Line 26
    cout << endl;                                         //Line 27

    vector<int> temp1(10);                                 //Line 28

    //replace_copy
    replace_copy(intList.begin(), intList.end(),
                 temp1.begin(), 34, 0);                   //Line 29

    cout << "Line 30: temp1 list after copying "
         << "intList and " << endl
         << "        replacing 34 with 0: ";              //Line 30
    copy(temp1.begin(), temp1.end(), screenOut);           //Line 31
    cout << endl;                                         //Line 32

    vector<int> temp2(10);                               //Line 33

    //replace_copy_if
    replace_copy_if(intList.begin(), intList.end(),
                    temp2.begin(), lessThanEqualTo50, 50); //Line 34

    cout << "Line 35: temp2 after copying intList "
         << "and replacing any " << endl
         << "         numbers less than 50 "
         << "with 50: " << endl << "          ";
    copy(temp2.begin(), temp2.end(), screenOut);                                //Line 36
    cout << endl;                                                               //Line 37

    return 0;                                                                   //Line 38
}                                                                               //Line 39

bool lessThanEqualTo50(int num)                                                 //Line 40
{                                                                               //Line 41
    return (num <= 50);                                                         //Line 42
}                                                                               //Line 43
```

### 示例运行：

```text
Line 12: Character list: A a A B A c D e F A
Line 16: Character list after replacing A with Z:
          Z a Z B Z c D e F Z
Line 20: Character list after replacing the uppercase
          letters with *: * a * * * * * e * *
Line 25: intList: 12 34 56 21 34 78 34 55 12 25
Line 30: temp1 list after copying intList and
          replacing 34 with 0: 12 0 56 21 0 78 0 55 12 25
Line 35: temp2 after copying intList and replacing any
          numbers less than 50 with 50:
          50 50 56 50 50 78 50 55 50 50
```

第10行的语句创建并初始化vector对象`charList`。第11行的语句声明一个ostream迭代器`screen`。第13行的语句输出`charList`的值。第15行的语句使用函数`replace`将`charList`中所有出现的`'A'`替换为`'Z'`。第17行的语句输出`charList`的元素。在输出中，标记为Line 16的行包含第16行到第18行的输出。第19行的语句使用函数`replace_if`将列表`charList`中的大写字母替换为`'*'`。第21行的语句输出`charList`的元素。在输出中，标记为Line 20的行包含第20行到第22行的输出。

第23行的语句创建并初始化vector对象`intList`。第26行的语句输出`intList`的元素。第28行的语句声明一个`int`类型的vector `temp1`。第29行的语句复制所有元素
