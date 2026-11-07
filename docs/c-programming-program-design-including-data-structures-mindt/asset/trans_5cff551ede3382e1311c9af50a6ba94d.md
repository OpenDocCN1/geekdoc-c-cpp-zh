

```cpp
char setC[5] = {'A', 'E', 'I', 'O', 'U'};          //Line 9
ostream_iterator<char> screen(cout, " ");          //Line 10

cout << "Line 11: setA: ";                         //Line 11
copy(setA, setA + 5, screen);                      //Line 12
cout << endl;                                      //Line 13

cout << "Line 14: setB: ";                         //Line 14
copy(setB, setB + 10, screen);                     //Line 15
cout << endl;                                      //Line 16

cout << "Line 17: setC: ";                         //Line 17
copy(setC, setC + 5, screen);                      //Line 18
cout << endl;                                      //Line 19

if (includes(setB, setB + 10, setA, setA + 5))     //Line 20
    cout << "Line 21: setA is a subset of "        //Line 21
         << "setB." << endl;
else                                                //Line 22
    cout << "Line 23: setA is not a subset "       //Line 23
         << "of setB." << endl;

if (includes(setB, setB + 10, setC, setC + 5))     //Line 24
    cout << "Line 25: setC is a subset of "        //Line 25
         << "setB." << endl;
else                                                //Line 26
    cout << "Line 27: setC is not a subset "       //Line 27
         << "of setB." << endl;                    //Line 27

return 0;                                           //Line 28
}                                                   //Line 29
```

## 示例运行

```text
Line 11: setA: A B C D E
Line 14: setB: A B C D E F I J K L
Line 17: setC: A E I O U
Line 21: setA is a subset of setB.
Line 27: setC is not a subset of setB.
```

前面的输出不言自明。具体细节留作练习。

算法 `set_intersection` 用于找出两个元素范围中的公共元素。该算法有两种形式，如下面的原型所示：

```cpp
template <class inputItr1, class inputItr2,
          class outputItr>
outputItr set_intersection(inputItr1 first1, inputItr1 last1,
                           inputItr2 first2, inputItr2 last2,
                           outputItr destFirst);
```

```cpp
template <class inputItr1, class inputItr2, class outputItr,
          class binaryPredicate>
outputItr set_intersection(inputItr1 first1, inputItr1 last1,
                           inputItr2 first2, inputItr2 last2,
                           outputItr destFirst,
                           binaryPredicate op);
```

两种形式都会创建一个有序元素序列，其中的元素是两个已排序范围 `first1...last1-1` 和 `first2...last2-1` 所共有的。所创建的序列被放入从 `destFirst` 开始的容器中。两种形式都返回一个迭代器，它指向目标范围中最后一个被复制元素之后的位置。第一种形式假定元素按升序排列；第二种形式假定两个范围都使用 `op` 指定的操作进行排序。源范围中的元素不会被修改。

假设

```cpp
setA[5] = {2, 4, 5, 7, 8};
setB[7] = {1, 2, 3, 4, 5, 6, 7};
setC[5] = {2, 5, 8, 8, 15};
setD[6] = {1, 4, 4, 6, 7, 12};
setE[7] = {2, 3, 4, 4, 5, 6, 10};
```

那么：

```cpp
AintersectB = {2, 4, 5, 7}
AintersectC = {2, 5, 8}
DintersectE = {4, 4, 6}
```

注意，因为 8 在 `setA` 中只出现一次，所以即使 8 在 `setC` 中出现两次，8 在 `AintersectC` 中也只出现一次。然而，因为 4 在 `setD` 和 `setE` 中都出现两次，所以 4 在 `DintersectE` 中也出现两次。

算法 `set_union` 用于找出包含在两个元素范围中的元素。该算法有两种形式，如下面的原型所示：

```cpp
template <class inputItr1, class inputItr2,
          class outputItr>
outputItr set_union(inputItr1 first1, inputItr1 last1,
                    inputItr2 first2, inputItr2 last2,
                    outputItr destFirst);
```

```cpp
template <class inputItr1, class inputItr2,
          class outputItr, class binaryPredicate>
outputItr set_union(inputItr1 first1, inputItr1 last1,
                    inputItr2 first2, inputItr2 last2,
                    outputItr result, binaryPredicate op);
```

两种形式都会创建一个有序元素序列，其中的元素出现在两个已排序范围 `first1...last1-1` 或 `first2...last2-1` 中。所创建的序列被放入从 `destFirst` 开始的容器中。两种形式都返回一个迭代器，它指向目标范围中最后一个被复制元素之后的位置。第一种形式假定元素按升序排列。第二种形式假定两个范围都使用 `op` 指定的操作进行排序。源范围中的元素不会被修改。

假设 `setA`、`setB`、`setC`、`setD` 和 `setE` 如前所定义。那么

```text
AunionB = {1, 2, 3, 4, 5, 6, 7, 8}
AunionC = {2, 4, 5, 7, 8, 8, 15}
BunionD = {1, 2, 3, 4, 4, 5, 6, 7, 12}
DunionE = {1, 2, 3, 4, 4, 5, 6, 7, 10, 12}
```

注意，因为 8 在 `setC` 中出现两次，所以它在 `AunionC` 中也出现两次。因为 4 在 `setD` 和 `setE` 中都出现两次，所以 4 在 `BunionD` 中也出现两次。

示例 21-28 说明了函数 `set_union` 和 `set_intersection` 如何工作。

## 示例 21-28

```cpp
// STL set theory functions set_union and set_intersection
// These functions assume that the elements in the given
// ranges are ordered according to some sorting criteria

#include <iostream>                                      //Line 1
#include <algorithm>                                     //Line 2
#include <iterator>                                      //Line 3

using namespace std;                                     //Line 4

int main()                                              //Line 5
{
    int setA[5] = {2, 4, 5, 7, 8};                      //Line 7
    int setB[7] = {1, 2, 3, 4, 5, 6, 7};                //Line 8
    int setC[5] = {2, 5, 8, 8, 15};                     //Line 9
    int setD[6] = {1, 4, 4, 6, 7, 12};                  //Line 10

    int AunionB[10];                                     //Line 11
    int AunionC[10];                                     //Line 12
    int BunionD[15];                                     //Line 13
    int AintersectB[10];                                 //Line 14
    int AintersectC[10];                                 //Line 15

    int *lastElem;                                       //Line 16

    ostream_iterator<int> screen(cout, " ");             //Line 17

    cout << "Line 18: setA = ";                          //Line 18
    copy(setA, setA + 5, screen);                        //Line 19
    cout << endl;                                        //Line 20

    cout << "Line 21: setB = ";                          //Line 21
    copy(setB, setB + 7, screen);                        //Line 22
    cout << endl;                                        //Line 23

    cout << "Line 24: setC = ";                          //Line 24
    copy(setC, setC + 5, screen);                        //Line 25
    cout << endl;                                        //Line 26

    cout << "Line 27: setD = ";                          //Line 27
    copy(setD, setD + 6, screen);                        //Line 28
    cout << endl;                                        //Line 29

    lastElem = set_union(setA, setA + 5,
                         setB, setB + 7,
                         AunionB);                      //Line 30

    cout << "Line 31: Set AunionB: ";                    //Line 31
    copy(AunionB, lastElem, screen);                     //Line 32
    cout << endl;                                        //Line 33

    lastElem = set_union(setA, setA + 5,
                         setC, setC + 5,
                         AunionC);                      //Line 34

    cout << "Line 35: Set AunionC: ";                    //Line 35
    copy(AunionC, lastElem, screen);                     //Line 36
    cout << endl;                                        //Line 37

    lastElem = set_union(setB, setB + 7,
                         setD, setD + 6,
                         BunionD);                      //Line 38

    cout << "Line 39: Set BunionD: ";                    //Line 39
    copy(BunionD, lastElem, screen);                     //Line 40
    cout << endl;                                        //Line 41

    lastElem = set_intersection(setA, setA + 5,
                                setB, setB + 7,
                                AintersectB);            //Line 42

    cout << "Line 43: Set AintersectB: ";                //Line 43
    copy(AintersectB, lastElem, screen);                 //Line 44
    cout << endl;                                        //Line 45

    lastElem = set_intersection(setA, setA + 5,
                                setC, setC + 5,
                                AintersectC);            //Line 46

    cout << "Line 47: Set AintersectC: ";                //Line 47
    copy(AintersectC, lastElem, screen);                 //Line 48
    cout << endl;                                        //Line 49

    return 0;                                            //Line 50
}                                                        //Line 51
```

