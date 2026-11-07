The algorithm random_shuffle is used to randomly order the elements in a given range. There are two forms of this algorithm, as shown by the following prototypes:

```
~~~cpp
template <class randomAccessItr>
void random_shuffle(randomAccessItr first,
                    randomAccessItr last);

template <class randomAccessItr, class randomAccessGenerator>
void random_shuffle(randomAccessItr first,
                    randomAccessItr last,
                    randomAccessGenerator rand);
~~~
```

The first form reorders the elements in the range first...last-1 using a uniform distribution random number generator. The second form reorders the elements in the range first...last-1 using a random number-generating function object or a pointer to a function.

Example 21-25 illustrates how to use these functions.

# EXAMPLE 21-25

```
~~~cpp
//STL Functions count, count_if, min_element,
//              max_element, random_shuffle

#include <iostream>
#include <cctype>
#include <algorithm>
#include <iterator>
#include <vector>

using namespace std;

void doubleNum(int num);

int main()
{
    char cList[10] = {'Z', 'a', 'Z', 'B', 'Z',
                      'c', 'D', 'e', 'F', 'Z'};        //Line 1

    vector<char>  charList(cList, cList + 10);         //Line 2

    ostream_iterator<char> screen(cout, " ");          //Line 3

    cout << "Line 4: charList: ";                      //Line 4
    copy(charList.begin(), charList.end(), screen);    //Line 5
    cout << endl;                                      //Line 6

    //count
    int noOfZs = count(charList.begin(),
                       charList.end(), 'Z');           //Line 7
~~~
```