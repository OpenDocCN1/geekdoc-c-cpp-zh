
```cpp
int funcAdd (plus<int> sum, int x, int y)
{
    return sum(x, y);
}
```

### Sample Run

```text
Line 3: num = 90
Line 8: str = Hello There
Line 9: Sum of 34 and 26 = 60
Line 13: intList: 1 2 3 4 5 6 7 8
Line 17: Sum of the elements of intList = 36
Line 19: Product of the elements of intList = 40320
```

Table 21-27 describes the relational STL function objects.

### TABLE 21-27 Relational STL Function Objects

| Function object name | Description |
| --- | --- |
| `equal_to<Type>` | Returns true if the two arguments are equal, and false otherwise. For example, `equal_to<int> compare;` `bool isEqual = compare(5, 5);` The value of isEqual is true. |
| `not_equal<Type>` | Returns true if the two arguments are not equal, and false otherwise. For example, `not_equal<int> compare;` `bool isNotEqual = compare(5, 6);` The value of isNotEqual is true. |
| `greater<Type>` | Returns true if the first argument is greater than the second argument, and false otherwise. For example, `greater<int> compare;` `bool isGreater = compare(8, 5);` The value of isGreater is true. |
| `greater_equal<Type>` | Returns true if the first argument is greater than or equal to the second argument, and false otherwise. For example, `greater_equal<int> compare;` `bool isGreaterEqual = compare(8, 5);` The value of isGreaterEqual is true. |
| `less<Type>` | Returns true if the first argument is less than the second argument, and false otherwise. For example, `less<int> compare;` `bool isLess = compare(3, 5);` The value of `isLess` is true. |
| `less_equal<Type>` | Returns true if the first argument is less than or equal to the second argument, and false otherwise. For example, `less_equal<int> compare;` `bool isLessEqual = compare(8, 15);` The value of `isLessEqual` is true. |

The STL relational function objects can also be applied to containers, as shown next. The STL algorithm adjacent_find searches a container and returns the position in the container where the two elements are equal. This algorithm has a second form that allows the user to specify the comparison criteria. For example, consider the following vector, vecList:

```cpp
vecList = {2, 3, 4, 5, 1, 7, 8, 9};
```

The elements of vecList are supposed to be in ascending order. To see if the elements are out of order, we can use the algorithm adjacent_find as follows:

```cpp
intItr = adjacent_find(vecList.begin(), vecList.end(),
                       greater<int>());
```

in which intItr is an iterator of the vector type. The function adjacent_find starts at the position vecList.begin()—that is, at the first element of vecList—and looks for the first set of consecutive elements such that the first element is greater than the second. The function returns a pointer to element 5, which is stored in intItr.

The program in Example 21-12 further illustrates how to use the relational function objects.

### EXAMPLE 21-12

This example shows how the relational STL function objects work.

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <iterator>
#include <vector>
#include <functional>

using namespace std;

int main()
{
    equal_to<int> compare;                         //Line 1
    bool isEqual = compare(6, 6);                  //Line 2

    cout << "Line 3: isEqual = " << isEqual << endl; //Line 3

    greater<string> greaterStr;                    //Line 4

    string str1 = "Hello";                         //Line 5
    string str2 = "There";                         //Line 6

    if (greaterStr(str1, str2))                    //Line 7
        cout << "Line 8: \"" << str1 << "\" is "
             << "greater than \"" << str2 << "\""
             << endl;                              //Line 8
    else
        cout << "Line 10: \"" << str1 << "\" is "
             << "not greater than \"" << str2
             << "\"" << endl;                      //Line 10

    int temp[8] = {2, 3, 4, 5, 1, 7, 8, 9};      //Line 11
    vector<int> vecList(temp, temp + 8);           //Line 12
    vector<int>::iterator intItr1, intItr2;        //Line 13
    ostream_iterator<int> screen(cout, " ");      //Line 14

    cout << "Line 15: vecList: ";
    copy(vecList.begin(), vecList.end(), screen);  //Line 16
    cout << endl;                                  //Line 17

    intItr1 = adjacent_find(vecList.begin(),
                            vecList.end(),
                            greater<int>());       //Line 18
    intItr2 = intItr1 + 1;                          //Line 19

    cout << "Line 20: In vecList, the first set of "
         << "out-of-order elements is: " << *intItr1
         << " and " << *intItr2 << endl;           //Line 20
    cout << "Line 21: In vecList, the first out-of-"
         << "order element is at position "
         << vecList.end() - intItr2 << endl;       //Line 21

    return 0;
}
```

### Sample Run

```text
Line 3: isEqual = 1
Line 10: "Hello" is not greater than "There"
Line 15: vecList: 2 3 4 5 1 7 8 9
Line 20: In vecList, the first set of out-of-order elements is: 5 1
Line 21: In vecList, the first out-of-order element is at position 4
```

Table 21-28 describes the logical STL function objects.

### TABLE 21-28 Logical STL Function Objects

| Function object name | Effect |
| --- | --- |
| `logical_not<Type>` | Returns `true` if its operand evaluates to `false`; otherwise, it returns `false`. This is a unary function object. |
| `logical_and<Type>` | Returns `true` if both of its operands evaluate to `true`; otherwise, it returns `false`. This is a binary function object. |
| `logical_or<Type>` | Returns `true` if at least one of its operands evaluates to `true`; otherwise, it returns `false`. This is a binary function object. |

## PREDICATES

Predicates are special types of function objects that return Boolean values. There are two types of predicates: unary and binary. Unary predicates check a specific property for a single argument; binary predicates check a specific property for a pair—that is, two arguments. Predicates are typically used to specify searching or sorting criteria. In the STL, a predicate must always return the same result for the same value. Therefore, the functions that modify their internal states *cannot* be considered predicates.

## Insert Iterator

Consider the following statements:

```cpp
int list[5] = {1, 3, 6, 9, 12}; //Line 1
vector<int> vList;                //Line 2
```

The statement in Line 1 declares and initializes list to be an array of five components. The statement in Line 2 declares vList to be a vector. Because no size is specified for vList, no memory space is reserved for the elements of vList. Now suppose that we want to copy the elements of list into vList. The statement:

```cpp
copy(list, list + 8, vList.begin());
```

will not work because no memory space is allocated for the elements of vList, and the copy function uses the assignment operator to copy the elements from the source to the destination. One solution to this problem is to use a loop to step through the elements of list and use the function push_back of vList to copy the elements of list. However, there is a better solution, which is convenient and applicable whenever no memory space is allocated at the destination. The STL provides three iterators, called insert iterators, to insert the elements at the destination: back_inserter, front_inserter, and inserter.

- **back_inserter**: This inserter uses the `push_back` operation of the container in place of the assignment operator. The argument to this iterator is the container itself. For example, for the preceding problem, we can copy the elements of `list` into `vList` by using `back_inserter` as follows:

    ```cpp
    copy(list, list + 5, back_inserter(vList));
    ```

- **front_inserter**: This inserter uses the `push_front` operation of the container in place of the assignment operator. The argument to this iterator is the container itself. Because the `vector` class does not support the `push_front` operation, this iterator *cannot* be used for the `vector` container.

- **inserter**: This inserter uses the container’s `insert` operation in place of the assignment operator. There are two arguments to this iterator: the first argument is the container itself; the second argument is an iterator to the container specifying the position at which the insertion should begin.

The program in Example 21-13 illustrates the effect of inserters on a container.

### EXAMPLE 21-13

```cpp
//Inserters

#include <iostream>
#include <algorithm>
#include <iterator>
#include <vector>
#include <list>

using namespace std;

int main()
{
    int temp[8] = {1, 2, 3, 4, 5, 6, 7, 8};             //Line 1
    vector<int> vecList1;                                 //Line 2
    vector<int> vecList2;                                 //Line 3
    ostream_iterator<int> screenOut(cout, " ");           //Line 4
    copy(temp, temp + 8, back_inserter(vecList1));        //Line 5
}
```
