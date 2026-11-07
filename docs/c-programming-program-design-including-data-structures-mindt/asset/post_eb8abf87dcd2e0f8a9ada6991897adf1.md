
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

## Sample Run:

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

## The Functions `count`, `count_if`, `max`, `max_element`, `min`, `min_element`, and `random_shuffle`

The algorithm count counts the occurrences of a given value in a given range. The prototype of the function implementing this algorithm is as follows:

```cpp
template <class InputItr, class T>
iterator_traits<InputItr>::difference_type
        count(InputItr first, InputItr last, const T& value);
```

The function count returns the number of times the value specified by the parameter `value` occurs in the range `first...last-1`.

The algorithm `count_if` counts the occurrences of a given value in a given range, satisfying a certain criterion. The prototype of the function implementing this algorithm is as follows:

```cpp
template <class InputItr, class UnaryPredicate>
iterator_traits<InputItr>::difference_type
        count_if(InputItr first, InputItr last, UnaryPredicate Op);
```

The function count_if returns the number of elements in the range `first...last-1` for which `op(elem)` is true.

The algorithm **max** is used to determine the maximum of two values. It has two forms, as given by the following prototypes:

```
template <class Type>
const Type& max(const Type& aVal, const Type& bVal);
```

```
template <class Type, class compare>
const Type& max(const Type& aVal, const Type& bVal, compare comp);
```

In the first form, the greater-than operator associated with **Type** is used. The second form uses the comparison operation specified by **comp**.

The algorithm **max_element** is used to determine the largest element in a given range. This algorithm has two forms, as given by the following prototypes:

```
template <class forwardItr>
forwardItr max_element(forwardItr first, forwardItr last);
```

```
template <class forwardItr, class compare>
forwardItr max_element(forwardItr first, forwardItr last,
                       compare comp);
```

The first form uses the greater-than operator associated with the data type of the elements in the range **first...last-1**. In the second form, the comparison operation specified by **comp** is used. Both forms return an iterator to the element containing the largest value in the range **first...last-1**.

The algorithm **min** is used to determine the minimum of two values. It has two forms, as given by the following prototypes:

```
template <class Type>
const Type& min(const Type& aVal, const Type& bVal);
```

```
template <class Type, class compare>
const Type& min(const Type& aVal, const Type& bVal, compare comp);
```

In the first form, the less-than operator associated with **Type** is used. In the second form, the comparison operation specified by **comp** is used.

The algorithm **min_element** is used to determine the smallest element in a given range. This algorithm has two forms, as given by the following prototypes:

```
template <class forwardItr>
forwardItr min_element(forwardItr first, forwardItr last);
```

```
template <class forwardItr, class compare>
forwardItr min_element(forwardItr first, forwardItr last,
                       compare comp);
```

The first form uses the less-than operator associated with the data type of the elements in the range **first...last-1**. The second form uses the comparison operation specified by **comp**. Both forms return an iterator to the element containing the smallest value in the range **first...last-1**.

The algorithm `random_shuffle` is used to randomly order the elements in a given range. There are two forms of this algorithm, as given by the following prototypes:

```
template <class randomAccessItr>
void random_shuffle(randomAccessItr first,
                    randomAccessItr last);

template <class randomAccessItr, class randomAccessGenerator>
void random_shuffle(randomAccessItr first, randomAccessItr last,
                    randomAccessGenerator rand);
```

The first form reorders the elements in the range `first...last-1` using a uniform distribution random number generator. The second form reorders the elements in the range `first...last-1` using a random number generating function object or a pointer to a function.

Example 21-25 illustrates how to use these functions.

## EXAMPLE 21-25

```
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
