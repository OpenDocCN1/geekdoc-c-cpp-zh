
```cpp
ostream_iterator<int> screen(cout, " ");              //Line 10

cout << "Line 11: intArray: ";                          //Line 11
copy(intArray, intArray + 9, screen);                    //Line 12
cout << endl;                                            //Line 13

copy(intArray, intArray + 9, vecList.begin());           //Line 14

cout << "Line 15: vecList: ";                           //Line 15
copy(vecList.begin(), vecList.end(), screen);            //Line 16
cout << endl;                                            //Line 17

copy(intArray + 1, intArray + 9, intArray);              //Line 18

cout << "Line 19: After shifting the elements"           //Line 19
     << " one position to the left, " << endl
     << "                intArray: ";

copy(intArray, intArray + 9, screen);                    //Line 20

cout << endl;                                            //Line 21

copy(vecList.rbegin() + 2, vecList.rend(),
                         vecList.rbegin());              //Line 22
cout << "Line 23: After shifting the "
     << "elements down by two positions, "
     << endl << "        vecList: ";                    //Line 23

copy(vecList.begin(), vecList.end(), screen);            //Line 24

cout << endl;                                            //Line 25

return 0;                                                //Line 26
}                                                        //Line 27
```

**Sample Run:**

```text
Line 11: intArray: 5 6 8 3 40 36 98 29 75
Line 15: vecList: 5 6 8 3 40 36 98 29 75
Line 19: After shifting the elements one position to the left,
          intArray: 6 8 3 40 36 98 29 75 75
Line 23: After shifting the elements down by two positions,
          vecList: 5 6 5 6 8 3 40 36 98
```

## Range-Based for Loops

In the previous section, we described how to use the copy function to output the elements of a vector container. Moreover, Chapter 8 introduced range-based for loops, which is a feature of C++11 Standard, and discussed how it can be effectively used to process the elements of an array. In Chapter 12, we explained that if a formal parameter of a function is an array, a range-based `for` loop cannot be used on that formal parameter, and we explained why a range-based `for` loop cannot be used on dynamic arrays. However, a range-based `for` loop can be used on sequence containers such as vector objects, even if they are declared as formal parameters to a function. Next, we explain how to use range-based `for` loops to process the elements of a vector object.

Consider the following statements:

```cpp
vector<int> intList;        //Line 1
intList.push_back(13);     //Line 2
intList.push_back(75);     //Line 3
intList.push_back(28);     //Line 4
intList.push_back(35);     //Line 5
```

As in Example 21-4, the statement in Line 1 declares the `vector intList` of type `int`. The statements in Lines 2 through 5 use the function `push_back` to insert four numbers—13, 75, 28, and 35—into `intList`.

Next, consider the following `for` loop:

```cpp
for (auto p : intList)
    cout << p << " ";
cout << endl;
```

In this `for` loop, after the statement `auto p : intList` executes, p will point to the first element of `intList`. We used `auto` so that the compiler can infer the correct type for p. In this `for` loop, p ranges over the elements of `intList`. You can read this as “for all p in `intList`.” As we can see, this `for` loop outputs the elements of `intList`.

In Example 21-4, we used a `for` loop to multiply each element of `intList` by 2. Next, we illustrate how to use a range-based `for` loop to multiply each element of `intList` by 2. In fact, we write a function that uses a formal parameter of type `vector<int>` to multiply each element of a `vector` object of type `int` by 2. So consider the following function:

```cpp
void doubleList(vector<int> &list)
{
    for (auto &p : list)  //p is a reference to allow us to
                           //change the elements of list
        p = p * 2;
}
```

The function `doubleList` takes as a parameter a reference to an object of type `vector<int>`. (Notice that the formal parameter, `list`, of the function `doubleList` is a reference parameter.) The body of this function multiplies each element of `list` by 2. Note that the definition of this function uses a range-based `for` loop to process the elements of `list`.

Example 21-6 further illustrates how to use a range-based `for` loop on vector objects.

### EXAMPLE 21-6

```cpp
#include <iostream>                              //Line 1
#include <vector>                                //Line 2

using namespace std;                             //Line 3

void doubleList(vector<int> &list);              //Line 4
void printList(const vector<int> &list);          //Line 5

int main()                                       //Line 6
{
    vector<int> intList;                         //Line 8

    intList.push_back(13);                       //Line 9
    intList.push_back(75);                       //Line 10
    intList.push_back(28);                       //Line 11
    intList.push_back(35);                       //Line 12

    cout << "intList: ";                         //Line 13
    printList(intList);                          //Line 14

    doubleList(intList);                         //Line 15

    cout << "intList after multiplying each "   //Line 16
         << " element by 2: ";                 //Line 17
    printList(intList);

    cout << endl;                                //Line 18

    return 0;                                    //Line 19
}                                                //Line 20

void printList(const vector<int> &list)           //Line 21
{
    for (auto p : list)                          //Line 23
        cout << p << " ";                        //Line 24
    cout << endl;                                //Line 25
}                                                //Line 26

void doubleList(vector<int> &list)               //Line 27
{
    for (auto &p : list)                         //Line 29
        p = p * 2;                               //Line 30
}                                                //Line 31
```

**Sample Run:**

```text
intList: 13 75 28 35
intList after multiplying each element by 2: 26 150 56 70
```

This sample is easy to follow. However, note that the preceding program uses the function `printList` to output the elements of `intList` and the function `doubleList` to multiply each element of `intList` by 2. Both these functions use a range-based `for` loop to process the elements of an object of type `vector<int>`.

## Initializing `vector` Objects during Declaration

C++ allows variables of simple data types or arrays to be initialized when they are declared. For example, consider the following statements:

```cpp
int x = 90;
int list[] = {2, 3, 4, 5};
```

The first statement declares `x` to be an `int` variable and initializes `x` to 90. The second statement declares `list` to be an `int` array of four elements and initializes the elements of `list` to 2, 3, 4, and 5, respectively. In Examples 21-4 and 21-6, we declared `intList` to be a `vector` object of type `int` and then used the function `push_back` to store `int` values in `intList`. To be specific, the following statements were used to declare `intList` to be a `vector<int>` object and store 13, 75, 28, and 35 in `intList`:

```cpp
vector<int> intList;
intList.push_back(13);
intList.push_back(75);
intList.push_back(28);
intList.push_back(35);
```

C++11 allows a `vector` object to be declared and initialized at the same time. For example, the following statement declares `intList` to be a `vector<int>` object and stores 13, 75, 28, and 35 in it.

```cpp
vector<int> intList = {13, 75, 28, 35};
```

That is, in C++11, the five statements used earlier to declare and initialize `intList` can be replaced by the preceding statement.

## Sequence Container: deque

This section describes the **deque** sequence containers. The term deque stands for double-ended queue. Deque containers are implemented as dynamic arrays in such a way that the elements can be inserted at both ends. Thus, a deque can expand in either direction. Elements can also be inserted in the middle. Inserting elements in the beginning or at the end is fast; inserting elements in the middle, however, is time consuming because the elements in the queue need to be shifted.

The name of the class defining the deque containers is **deque**. The definition of the **class deque**, and the functions to implement the various operations on a **deque** object, are also contained in the header file **deque**. Therefore, to use a **deque** container in a program, the program must include the following statement:

```cpp
#include <deque>
```

The **class deque** contains several constructors. Thus, a **deque** object can be initialized in various ways when it is declared, as described in Table 21-7.

**TABLE 21-7** Various Ways to Declare a deque Object

| Statement | Description |
|---|---|
| `deque<elementType> deq;` | Creates an empty deque container **deq**. (The default constructor is invoked.) |
| `deque<elementType> deq(otherDeq);` | Creates the deque container **deq** and initializes it to the elements of **otherDeq**; **deq** and **otherDeq** are of the same type. |
| `deque<elementType> deq(size);` | Creates the deque container **deq** of size **size**. **deq** is initialized using the default constructor. |
| `deque<elementType> deq(n, elm);` | Creates the deque container **deq** of size **n**. **deq** is initialized using **n** copies of the element **elm**. |
| `deque<elementType> deq(beg, end);` | Creates the deque container **deq**. **deq** is initialized to the elements in the range `[beg, end)`; that is, all elements in the range `beg, ..., end−1`. Both **beg** and **end** are iterators. |
