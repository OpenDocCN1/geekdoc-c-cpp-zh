
Because objectOne is passed by value, the member variables of paramObject should have their own copy of the data. In particular, paramObject.p should have its own memory space. How do we ensure that this is, in fact, the case?

If a class has pointer member variables:

- During object declaration, the initialization of one object using the value of another object would lead to a shallow copying of the data if the default member-wise copying of data is allowed.
- If, as a parameter, an object is passed by value and the default member-wise copying of data is allowed, it would lead to a shallow copying of the data.

In both cases, to force each object to have its own copy of the data, we must override the definition of the copy constructor provided by the compiler; that is, we must provide our own definition of the copy constructor. This is usually done by putting a statement that includes the copy constructor in the definition of the class and then writing the definition of the copy constructor. Then, whenever the copy constructor needs to be executed, the system would execute the definition provided by us, not the one provided by the compiler. Therefore, for the class ptrMemberVarType, we can overcome this shallow copying problem by including the copy constructor in the class ptrMemberVarType. Example 14-6 illustrates this.

The copy constructor automatically executes in three situations (the first two are described previously).

- When an object is declared and initialized by using the value of another object
- When, as a parameter, an object is passed by value
- When the return value of a function is an object

Therefore, once the copy constructor is properly defined for the class ptrMemberVarType, both objectOne.p and objectThree.p will have their own copies of the data. Similarly, objectOne.p and paramObject.p will have their own copies of the data, as shown in Figure 14-21.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_863_0.png)

**FIGURE 14-21** Pointer member variables of objects *objectOne* and *paramObject* with their own data

When the function destroyList exits, the formal parameter paramObject goes out of scope, and the destructor for the object paramObject deallocates the memory space pointed to by paramObject.p. However, this deallocation has no effect on objectOne.

The general syntax to include the copy constructor in the definition of a class is:

```cpp
className(const className& otherObject);
```

Notice that the formal parameter of the copy constructor is a constant reference parameter.

Example 14-7 illustrates how to include the copy constructor in a class and how it works.

### EXAMPLE 14-7

Consider the following class:

```cpp
class ptrMemberVarType
{
public:
    void print() const;
        //Function to output the data stored in the array p.

    void insertAt(int index, int num);
        //Function to insert num into the array p at the
        //position specified by index.
        //If index is out of bounds, the program is terminated.
        //If index is within bounds, but greater than the index
        //of the last item in the list, num is added at the end
        //of the list.

    ptrMemberVarType(int size = 10);
        //Constructor
        //Creates an array of the size specified by the
        //parameter size; the default array size is 10.

    ~ptrMemberVarType();
        //Destructor
        //deallocates the memory space occupied by the array p.

    ptrMemberVarType(const ptrMemberVarType& otherObject);
        //Copy constructor

private:
    int maxSize; //variable to store the maximum size of p
    int length;  //variable to store the number of elements in p
    int *p;      //pointer to an int array
};
```

Suppose that the definitions of the members of the class ptrMemberVarType are as follows:

```cpp
void ptrMemberVarType::print() const
{
    for (int i = 0; i < length; i++)
        cout << p[i] << " ";
}

void ptrMemberVarType::insertAt(int index, int num)
{
    //if index is out of bounds, terminate the program
    assert(index >= 0 && index < maxSize);

    if (index < length)
        p[index] = num;
    else
    {
        p[length] = num;
        length++;
    }
}

ptrMemberVarType::ptrMemberVarType(int size)
{
    if (size <= 0)
    {
        cout << "The array size must be positive." << endl;
        cout << "Creating an array of the size 10." << endl;

        maxSize = 10;
    }
    else
        maxSize = size;

    length = 0;

    p = new int[maxSize];

}

ptrMemberVarType::~ptrMemberVarType()
{
    delete [] p;
}

    //copy constructor
ptrMemberVarType::ptrMemberVarType
                  (const ptrMemberVarType& otherObject)
{
    maxSize = otherObject.maxSize;
    length = otherObject.length;
    p = new int[maxSize];

    for (int i = 0; i < length; i++)
        p[i] = otherObject.p[i];
}
```

Consider the following function main. (We assume that the definition of the class ptrMemberVarType is in the header file ptrMemberVarType.h.)

```cpp
#include <iostream>
#include "ptrMemberVarType.h"

using namespace std;

void testCopyConst(ptrMemberVarType temp);

int main()
{
    ptrMemberVarType listOne;                         //Line 1

    int num;                                           //Line 2
    int index;                                          //Line 3

    cout << "Line 4: Enter 5 integers." << endl;      //Line 4

    for (index = 0; index < 5; index++)                //Line 5
    {
        cin >> num;                                    //Line 6
        listOne.insertAt(index, num);                  //Line 7
    }

    cout << "Line 8: listOne: ";                      //Line 8
    listOne.print();                                   //Line 9
    cout << endl;                                      //Line 10

        //Declare listTwo and initialize it using listOne
    ptrMemberVarType listTwo(listOne);                 //Line 11

    cout << "Line 12: listTwo: ";                     //Line 12
    listTwo.print();                                   //Line 13
    cout << endl;                                      //Line 14

    listTwo.insertAt(5, 34);                           //Line 15
    listTwo.insertAt(2, -76);                          //Line 16

    cout << "Line 17: After modifying listTwo: ";    //Line 17
    listTwo.print();                                   //Line 18
    cout << endl;                                      //Line 19

    cout << "Line 20: After modifying listTwo, "    //Line 20
         << "listOne: ";                             //Line 21
    listOne.print();                                   //Line 22
    cout << endl;                                      //Line 23

    cout << "Line 23: Calling the function testCopyConst"
         << endl;                         //Line 23

    //Call function testCopyConst
    testCopyConst(listOne);                  //Line 24

    cout << "Line 25: After a call to the function "
         << "testCopyConst, " << endl
         << "       listOne is: ";           //Line 25

    listOne.print();                        //Line 26
    cout << endl;                           //Line 27

    return 0;                               //Line 28
}

void testCopyConst(ptrMemberVarType temp)
{
    cout << "Line 29: *** Inside the function "
         << "testCopyConst ***" << endl; //Line 29

    cout << "Line 30: Object temp data: "; //Line 30
    temp.print();                          //Line 31
    cout << endl;                          //Line 32

    temp.insertAt(3, -100);                //Line 33
    cout << "Line 34: After changing temp: "; //Line 34
    temp.print();                          //Line 35
    cout << endl;                          //Line 36

    cout << "Line 37: *** Exiting the function "
         << "testCopyConst ***" << endl; //Line 37
}
```

**Sample Run:** In this sample run, the user input is shaded.

```text
Line 4: Enter 5 integers.
14 8 34 2 58
Line 8: listOne: 14 8 34 2 58
Line 12: listTwo: 14 8 34 2 58
Line 17: After modifying listTwo: 14 8 -76 2 58 34
Line 20: After modifying listTwo, listOne: 14 8 34 2 58
Line 23: Calling the function testCopyConst
Line 29: *** Inside the function testCopyConst ***
Line 30: Object temp data: 14 8 34 2 58
Line 34: After changing temp: 14 8 34 -100 58
Line 37: *** Exiting the function testCopyConst ***
Line 25: After a call to the function testCopyConst,
       listOne is: 14 8 34 2 58
```

In the preceding program, the statement in Line 1 declares listOne to be an object of type ptrMemberVarType. The member variable p of listOne is an array of size 10, which is
