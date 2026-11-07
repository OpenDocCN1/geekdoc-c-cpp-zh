
## 示例 15-9

在本例中，我们将编写一个使用 `class` listType 的程序。包含的部分操作如下：检查列表是否为空、检查列表是否已满、对列表排序以及打印列表。由于我们可以动态分配数组，用户将能够指定数组的大小。默认数组大小为 50。我们将操作一个整数列表和一个字符串列表。由于我们之前定义的 newString 类允许我们使用关系运算符进行比较，并使用赋值运算符进行赋值，因此我们将使用 newString 类来声明字符串。

listType 类的定义如下：

```cpp
#ifndef H_listType
#define H_listType

#include <iostream>
#include <cassert>

using namespace std;

template <class elemType>
class listType
{
public:
    bool isEmpty() const;
        //Function to determine whether the list is empty.
        //Postcondition: Returns true if the list is empty,
                       otherwise it returns false.

    bool isFull() const;
        //Function to determine whether the list is full.
        //Postcondition: Returns true if the list is full,
                       otherwise it returns false.

    int getLength() const;
        //Function to return the number of elements in the list.
        //Postcondition: The value of length is returned.

    int getMaxSize() const;
        //Function to return the maximum number of elements
        //that can be stored in the list.
        //Postcondition: The value of maxSize is returned.

    void sort();
        //Function to sort the list.
        //Postcondition: The list elements are in ascending order.

    void print() const;
        //Outputs the elements of the list.

    void insertAt(const elemType& item, int position);
        //Function to insert item in the list at the location
        //specified by position.
        //Postcondition: list[position] = item; length++;
        //
        //            If position is out of range, the program
        //            is aborted.

    listType(int listSize = 50);
        //Constructor
        //Creates an array of the size specified by the
        //parameter listSize; the default array size is 50.
        //Postcondition: list contains the base address of the
        //            array; length = 0; maxSize = listSize;

    ~listType();
        //Destructor
        //Deletes all the elements of the list.
        //Postcondition: The array list is deleted.

private:
    int maxSize;    //variable to store the maximum size
                    //of the list
    int length;     //variable to store the number of elements
                    //in the list
    elemType *list; //pointer to the array that holds the
                    //list elements
};


template <class elemType>
bool listType<elemType>::isEmpty() const
{
    return (length == 0);
}

template <class elemType>
bool listType<elemType>::isFull() const
{
    return (length == maxSize);
}

template <class elemType>
int listType<elemType>::getLength() const
{
    return length;
}

template <class elemType>
int listType<elemType>::getMaxSize() const
{
    return maxSize;
}

    //Constructor; the default array size is 50
template <class elemType>
listType<elemType>::listType(int listSize)
{
    maxSize = listSize;
    length = 0;
    list = new elemType[maxSize];
}

template <class elemType>
listType<elemType>::~listType()  //destructor
{
    delete [] list;
}

template <class elemType>
void listType<elemType>::sort()   //selection sort
{
    int i, j;
    int min;
    elemType temp;

    for (i = 0; i < length; i++)
    {
        min = i;
        for (j = i + 1; j < length; ++j)
            if (list[j] < list[min])
                min = j;

        temp = list[i];
        list[i] = list[min];
        list[min] = temp;
    }//end for
}//end sort

template <class elemType>
void listType<elemType>::print() const
{
    int i;
    for (i = 0; i < length; ++i)
        cout << list[i] << " ";
    cout << endl;
}//end print

template <class elemType>
void listType<elemType>::insertAt(const elemType& item,
                                  int position)
{
    assert(position >= 0 && position < maxSize);
    list[position] = item;
    length++;
}

#endif
```

请考虑以下程序：

```cpp
//This program shows how to use the class template listType.

#include <iostream>

#include "myString.h"
#include "listType.h"

using namespace std;

int main()
{
        listType<int> intList(100);                    //Line 1
        listType<newString> stringList;                //Line 2
        int index;                                      //Line 3
        int number;                                     //Line 4

        cout << "Line 5: Processing the integer list"
             << endl;                                  //Line 5
        cout << "Line 6: Enter 5 integers: ";         //Line 6

        for (index = 0; index < 5; index++)             //Line 7
        {
                cin >> number;                         //Line 8
                intList.insertAt(number, index);       //Line 9
        }

        cout << endl;                                   //Line 10
        cout << "Line 11: intList: ";                  //Line 11
        intList.print();                                //Line 12
        cout << endl;                                   //Line 13

                //Sort intList
        intList.sort();                                 //Line 14

        cout << "Line 15: After sorting, intList: ";  //Line 15
        intList.print();                                //Line 16
        cout << endl;                                   //Line 17

        newString str;                                  //Line 18

        cout << "Line 19: Processing the string list"
             << endl;                                  //Line 19

        cout << "Line 20: Enter 5 strings: ";         //Line 20

        for (index = 0; index < 5; index++)             //Line 21
        {
                cin >> str;                            //Line 22
                stringList.insertAt(str, index);       //Line 23
        }

        cout << endl;                                   //Line 24
        cout << "Line 25: stringList: ";               //Line 25
        stringList.print();                             //Line 26
        cout << endl;                                   //Line 27

        //Sort stringList
        stringList.sort();                              //Line 28

        cout << "Line 29: After sorting, stringList: ";//Line 29
        stringList.print();                             //Line 30
        cout << endl;                                   //Line 31

        int intListSize;                                //Line 32

        cout << "Line 33: Enter the size of the integer " //Line 33
             << "list: ";                               //Line 33
        cin >> intListSize;                             //Line 34
        cout << endl;                                   //Line 35

        listType<int> intList2(intListSize);            //Line 36

        cout << "Line 37: Processing the integer list"  //Line 37
             << endl;
        cout << "Line 38: Enter " << intListSize
             << " integers: ";

        for (index = 0; index < intListSize; index++)   //Line 39
        {
                cin >> number;                          //Line 40
                intList2.insertAt(number, index);       //Line 41
        }

        cout << endl;                                   //Line 42

        cout << "Line 43: intList2: ";                  //Line 43
        intList2.print();                               //Line 44
        cout << endl;                                   //Line 45

        //Sort intList2
        intList2.sort();                                //Line 46

        cout << "Line 47: After sorting, intList2: ";  //Line 47
        intList2.print();                               //Line 48
        cout << endl;                                   //Line 49

        cout << "Line 50: Length of intList2: "
             << intList2.getLength() << endl;           //Line 50
        cout << "Line 51: Maximum size of intList2: "
             << intList2.getMaxSize() << endl;          //Line 51

        return 0;
}
```
