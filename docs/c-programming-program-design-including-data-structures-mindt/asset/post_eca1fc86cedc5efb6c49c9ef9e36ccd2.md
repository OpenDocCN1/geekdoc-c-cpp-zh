
When the function `destroyList` exits, the formal parameter `paramObject` goes out of scope, and the destructor for the object `paramObject` deallocates the memory space pointed to by `paramObject.p`. However, this deallocation has no effect on `objectOne`.

The general syntax to include the copy constructor in the definition of a class is:

```cpp
className(const className& otherObject);
```

Notice that the formal parameter of the copy constructor is a constant reference parameter.

Example 12-8 illustrates how to include the copy constructor in a class and how it works.

## EXAMPLE 12-8

Consider the following class:

```cpp
class ptrMemberVarType
{
public:
    void print() const;
        //Function to output the data stored in the array p.

    void insertAt(int index, int num);
        //function to insert num into the array p at the
        //position specified by index.
        //If index is out of bounds, the program is terminated.
        //If the index is within bounds, but greater than the index
        //of the last item in the list, num is added at the end
        //of the list.

    ptrMemberVarType(int size = 10);
        //Constructor
        //Creates an array of the size specified by the
        //parameter size; the default array size is 10.

    ~ptrMemberVarType();
        //Destructor
        //Deallocates the memory space occupied by the array p.

    ptrMemberVarType(const ptrMemberVarType& otherObject);
        //Copy constructor

private:
    int maxSize;  //variable to store the maximum size of p
    int length;   //variable to store the number of elements in p
    int *p;       //pointer to an int array
};
```

```cpp
p = new int[maxSize];

for (int i = 0; i < length; i++)
    p[i] = otherObject.p[i];
}
```

Consider the following function main. (We assume that the definition of the class ptrMemberVarType is in the header file ptrMemberVarType.h.)

```cpp
#include <iostream>                                     //Line 1
#include "ptrMemberVarType.h"                           //Line 2

using namespace std;                                    //Line 3

void testCopyConst(ptrMemberVarType temp);              //Line 4

int main()                                              //Line 5
{                                                       //Line 6
    ptrMemberVarType listOne;                           //Line 7

    int num;                                            //Line 8

    cout << "Line 9: Enter 5 integers." << endl;        //Line 9

    for (int index = 0; index < 5; index++)             //Line 10
    {                                                   //Line 11
        cin >> num;                                     //Line 12
        listOne.insertAt(index, num);                   //Line 13
    }                                                   //Line 14

    cout << "Line 15: listOne: ";                       //Line 15
    listOne.print();                                    //Line 16
    cout << endl;                                       //Line 17

    //Declare listTwo and initialize it using listOne
    ptrMemberVarType listTwo(listOne);                  //Line 18

    cout << "Line 19: listTwo: ";                       //Line 19
    listTwo.print();                                    //Line 20
    cout << endl;                                       //Line 21

    listTwo.insertAt(5, 34);                            //Line 22
    listTwo.insertAt(2, -76);                           //Line 23

    cout << "Line 24: After modifying listTwo: ";       //Line 24
    listTwo.print();                                    //Line 25
    cout << endl;                                       //Line 26

    cout << "Line 27: After modifying listTwo, "
         << "listOne: ";                                //Line 27
    listOne.print();                                    //Line 28
    cout << endl;                                       //Line 29

    cout << "Line 30: Calling the function testCopyConst"     //Line 30
         << endl;

    //Call function testCopyConst
    testCopyConst(listOne);                                      //Line 31

    cout << "Line 32: After a call to the function "
         << "testCopyConst, " << endl
         << "             listOne is: ";                       //Line 32

    listOne.print();                                            //Line 33
    cout << endl;                                                //Line 34

    return 0;                                                    //Line 35
}                                                                //Line 36

void testCopyConst(ptrMemberVarType temp)                        //Line 37
{
    cout << "Line 39: *** Inside the function "
         << "testCopyConst ***" << endl;                        //Line 39

    cout << "Line 40: Object temp data: ";                      //Line 40
    temp.print();                                               //Line 41
    cout << endl;                                               //Line 42

    temp.insertAt(3, -100);                                      //Line 43
    cout << "Line 44: After changing temp: ";                   //Line 44
    temp.print();                                               //Line 45
    cout << endl;                                               //Line 46

    cout << "Line 47: *** Exiting the function "
         << "testCopyConst ***" << endl;                        //Line 47
}                                                                //Line 48
```

**Sample Run:** In this sample run, the user input is shaded.

```text
Line 9: Enter 5 integers.
25 10 48 2 40
Line 15: listOne: 25 10 48 2 40
Line 19: listTwo: 25 10 48 2 40
Line 24: After modifying listTwo: 25 10 -76 2 40 34
Line 27: After modifying listTwo, listOne: 25 10 48 2 40
Line 30: Calling the function testCopyConst
Line 39: *** Inside the function testCopyConst ***
Line 40: Object temp data: 25 10 48 2 40
Line 44: After changing temp: 25 10 48 2 -100 40
Line 47: *** Exiting the function testCopyConst ***
Line 32: After a call to the function testCopyConst,
               listOne is: 25 10 48 2 40
```

In the preceding program, the statement in Line 7 declares **listOne** to be an object of type **ptrMemberVarType**. The member variable of **listOne** is an array of size 10, which is the default array size. The `for` loop in Line 10 reads and stores five integers in `listOne.p`. The statement in Line 16 outputs the numbers stored in `listOne`, that is, the five numbers stored in `p`. (See the output of the line marked Line 15 in the sample run.)

The statement in Line 18 declares `listTwo` to be an object of type `ptrMemberVarType` and also initializes `listTwo` using the values of `listOne`. The statement in Line 20 outputs the numbers stored in `listTwo`. (See the output of the line marked Line 19 in the sample run.)

The statements in Lines 22 and 23 modify `listTwo`, and the statement in Line 25 outputs the modified data of `listTwo`. (See the output of the line marked Line 24 in the sample run.) The statement in Line 28 outputs the data stored in `listOne`. Notice that the data stored in `listOne` is unchanged, even though `listTwo` modified its data. It follows that the copy constructor used to initialize `listTwo` using `listOne` (at Line 18) provides `listTwo` its own copy of the data.

The statements in Lines 30 through 34 show that when `listOne` is passed as a parameter by value to the function `testCopyConst` (see Line 31), the corresponding formal parameter `temp` has its own copy of data. Notice that the function `testCopyConst` modifies the object `temp`; however, the object `listOne` remains unchanged. See the outputs of the lines marked Line 30 (before the function `testCopyConst` is called) and Line 32 (after the function `testCopyConst` terminates) in the sample run. Also notice that when the function `testCopyConst` terminates, the destructor of the class `ptrMemberVarType` deallocates the memory space occupied by `temp.p`, which has no effect on `listOne.p`.

For classes with pointer member variables, three things are normally done:

- Include the destructor in the class.
- Overload the assignment operator for the class.
- Include the copy constructor.

Chapter 13 discusses overloading the assignment operator. Until then, whenever we discuss classes with pointer member variables, out of the three items in the previous list, we will implement only the destructor and the copy constructor.

## Inheritance, Pointers, and Virtual Functions

Recall that as a parameter, a class object can be passed either by value or by reference. Earlier chapters also said that the types of the actual and formal parameters must match. However, in the case of classes, C++ allows the user to pass an object of a derived class to a formal parameter of the base class type. This is because the derived class has the base class as its foundation. The formal parameter recognizes the base class portion of the derived class and allows it to pass.
