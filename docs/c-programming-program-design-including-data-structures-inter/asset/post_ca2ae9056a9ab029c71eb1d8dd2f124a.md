
```cpp
cout << "Line 6: vecList1: ";                    //Line 6
copy(vecList1.begin(), vecList1.end(),
     screenOut);                                  //Line 7
cout << endl;                                     //Line 8

copy(vecList1.begin(), vecList1.end(),
     inserter(vecList2, vecList2.begin()));       //Line 9

cout << "Line 10: vecList2: ";                  //Line 10
copy(vecList2.begin(), vecList2.end(),
     screenOut);                                  //Line 11
cout << endl;                                     //Line 12

list<int> tempList;                               //Line 13

copy(vecList2.begin(), vecList2.end(),
     front_inserter(tempList));                   //Line 14

cout << "Line 15: tempList: ";                   //Line 15
copy(tempList.begin(), tempList.end(),
     screenOut);                                  //Line 16
cout << endl;                                     //Line 17

return 0;
}
```

**Sample Run:**

```
Line 6: vecList1: 1 2 3 4 5 6 7 8
Line 10: vecList2: 1 2 3 4 5 6 7 8
Line 15: tempList: 8 7 6 5 4 3 2 1
```

## STL Algorithms

The following sections describe most of the STL algorithms. For each algorithm, we give the function prototypes, a brief description of what the algorithm does, and a program showing how to use it. In the function prototypes, the parameter types indicate for which type of container the algorithm is applicable. For example, if a parameter is of type randomAccessIterator, then the algorithm is applicable only on random access type containers, such as vectors. Throughout, we use adjectives such as outputItr to mean output iterator, inputItr to mean input iterator, forwardItr to mean forward iterator, and so on.

### The Functions `fill` and `fill_n`

The function fill is used to fill a container with elements; the function fill_n is used to fill in the next n elements. The element that is used as a filling element is passed as a parameter to these functions. Both of these functions are defined in the header file algorithm. The prototypes of these functions are:

The statements in Lines 1 and 2 declare vecList to be a sequence container of size 8 and screen to be an ostream iterator initialized to cout with the delimiter character space. The statement in Line 3 uses the function fill to fill vecList with 2; that is, all eight elements of vecList are set to 2. Recall that vecList.begin() returns an iterator to the first element of vecList, and vecList.end() returns an iterator one past the last element of vecList. The statement in Line 5 outputs the elements of vecList using the copy function. The statement in Line 7 uses the function fill_n to store 5 in the elements of vecList. The first parameter of fill_n is vecList.begin(), which specifies the starting position to begin copying. The second parameter of fill_n is 3, which specifies the number of elements to be filled. The third parameter, 5, specifies the filling character. Therefore, 5 is copied into the first three elements of vecList. The statement in Line 9 outputs the elements of vecList.

### The Functions generate and generate_n

The functions generate and generate_n are used to generate elements and fill a sequence. These functions are defined in the header file algorithm. The prototypes of these functions are:

```cpp
template <class forwardItr, class function>
void generate(forwardItr first, forwardItr last, function gen);

template <class forwardItr, class size, class function>
void generate_n(forwardItr first, size n, function gen);
```

The function generate fills a sequence in the range first...last-1, with successive calls to the function gen(). The function generate_n fills a sequence in the range first...first+n-1 that is, starting at position first, with successive calls to the function gen(). Note that gen can also be a pointer to a function. Moreover, if gen is a function, it must be a value-returning function without parameters. The program in Example 21-15 illustrates how to use these functions.

**EXAMPLE 21-15**

```cpp
//STL Functions generate and generate_n

#include <iostream>
#include <algorithm>
#include <iterator>
#include <vector>

using namespace std;

int nextNum();

int main()
{
    vector<int> vecList(8);

    ostream_iterator<int> screen(cout, " ");

    generate(vecList.begin(), vecList.end(), nextNum); //Line 1

    cout << "Line 4: vecList after filling with "
         << " numbers: "; //Line 4

    copy(vecList.begin(), vecList.end(), screen); //Line 5
    cout << endl; //Line 6

    generate_n(vecList.begin(), 3, nextNum); //Line 7

    cout << "Line 8: vecList after filling the "
         << "first three elements " << endl
         << " with the next number: "; //Line 8

    copy(vecList.begin(), vecList.end(), screen); //Line 9
    cout << endl; //Line 10

    return 0;
}

int nextNum()
{
    static int n = 1;

    return n++;
}
```

**Sample Run:**

```
Line 4: vecList after filling with numbers: 1 2 3 4 5 6 7 8
Line 8: vecList after filling the first three elements
        with the next number: 9 10 11 4 5 6 7 8
```

This program contains a value-returning function, nextNum, which contains a static variable n initialized to 1. A call to this function returns the current value of n and then increments the value of n. Therefore, the first call of nextNum returns 1, the second call returns 2, and so on.

The statements in Lines 1 and 2 declare vecList to be a sequence container of size 8 and screen to be an ostream iterator initialized to cout with the delimiter character space. The statement in Line 3 uses the function generate to fill vecList by successively calling the function nextNum. Notice that after the statement in Line 3 executes, the value of the static variable n of nextNum is 9. The statement in Line 5 outputs the elements of vecList. The statement in Line 7 calls the function generate_n to fill the first three elements of vecList by calling the function nextNum three times. The starting position is vecList.begin(), which is the first element of vecList, and the number of elements to be filled is 3, given by the second parameter of generate_n (see Line 7). The statement in Line 9 outputs the elements of vecList.

### The Functions find, find_if, find_end, and find_first_of

The functions find, find_if, find_end, and find_first_of are used to find the elements in a given range. These functions are defined in the header file algorithm. The prototypes of the functions find and find_if are:

```cpp
template <class inputItr, class size, class Type>
inputItr find(inputItr first, inputItr last,
              const Type& searchValue);

template <class inputItr, class unaryPredicate>
inputItr find_if(inputItr first, inputItr last, unaryPredicate op);
```

The function find searches the range of elements first...last-1 for the element searchValue. If searchValue is found in the range, the function returns the position in the range where searchValue is found; otherwise, it returns last. The function find_if searches the range of elements first...last-1 for the element for which op(rangeElement) is true. If an element satisfying op(rangeElement) is true is found, it returns the position in the given range where such an element is found; otherwise, it returns last.

The program in Example 21-16 illustrates how to use the functions find and find_if.

**EXAMPLE 21-16**

```cpp
//STL Functions find and find_if

#include <iostream>
#include <cctype>
#include <algorithm>
#include <iterator>
#include <vector>

using namespace std;

int main()
{
    char cList[10] = {'a', 'i', 'C', 'd', 'e',
                      'f', 'o', 'H', 'u', 'j'};

    vector<char> charList(cList, cList + 10);        //Line 2

    ostream_iterator<char> screen(cout, " ");          //Line 3

    cout << "Line 4: Character list: ";                  //Line 4
    copy(charList.begin(), charList.end(), screen);      //Line 5
    cout << endl;                                        //Line 6

    vector<char>::iterator position;                     //Line 7

            //find it
    position = find(charList.begin(),
                   charList.end(), 'd');                 //Line 8

    if (position != charList.end())                      //Line 9
        cout << "Line 10: The element is found at "
             << "position "
             << (position - charList.begin())            //Line 10
             << endl;                                    //Line 11
    else
        cout << "Line 12: The element is not in "
             << "the list." << endl;                    //Line 12

            //find_if
    position = find_if(charList.begin(),
                       charList.end(), isupper);         //Line 13

    if (position != charList.end())                      //Line 14
        cout << "Line 15: The first uppercase "
             << "letter is found at position "
             << (position - charList.begin())            //Line 15
             << endl;                                    //Line 16
    else
        cout << "Line 17: The element is not in "
             << "the list." << endl;                    //Line 17

    return 0;
}
```

**Sample Run:**

```
Line 4: Character list: a i C d e f o H u j
Line 10: The element is found at position 3
Line 15: The first uppercase letter is found at position 2
```

The statement in Line 1 creates and initializes a character array, cList, of 10 components. The statement in Line 2 creates the vector container charList and initializes it using the character array cList. The statement in Line 3 creates an ostream iterator. The statement in Line 5 outputs charList. (In the output, the line marked Line 4 contains the output of Lines 4 through 6 of the program.) The statement in Line 7 declares the iterator position of type vector<char>. The statement in Line 8 searches charList for the first occurrence of 'd' and returns an iterator, which is stored in position. The statements in Lines 9 through 12 output the result of the search. Because 'd' is the fourth character in charList, its position is 3.
