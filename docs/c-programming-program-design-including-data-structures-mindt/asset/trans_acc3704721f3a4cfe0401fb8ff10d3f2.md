

```cpp
template <class elemType>
void arrayListType<elemType>::removeAt(int location)
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be removed "
             << " is out of range." << endl;
    else
    {
        for (int i = location; i < length - 1; i++)
            list[i] = list[i + 1];

        length--;
    }
}    //end removeAt

template <class elemType>
void arrayListType<elemType>::retrieveAt(int location,
                                         elemType& retItem) const
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be retrieved is "
             << " out of range." << endl;
    else
        retItem = list[location];
}    //end retrieveAt

template <class elemType>
arrayListType<elemType>::arrayListType(int size)
{
    if (size <= 0)
    {
        cout << "The array size must be positive. Creating "
             << " an array of the size 100. " << endl;
        maxSize = 100;
    }
    else
        maxSize = size;

    length = 0;
    list = new elemType[maxSize];
}    //end constructor

template <class elemType>
arrayListType<elemType>::~arrayListType()
{
    delete [] list;
}    //end destructor
```

接下来，因为我们正在为类 `arrayListType` 重载赋值运算符，所以给出用于重载赋值运算符的函数模板定义。

```cpp
template <class elemType>
const arrayListType<elemType>& arrayListType<elemType>::operator=
                                      (const arrayListType<elemType>& otherList)
{
    if (this != &otherList)  //avoid self-assignment
    {
        delete [] list;
        maxSize = otherList.maxSize;
        length = otherList.length;

        list = new elemType[maxSize];

        for (int i = 0; i < length; i++)
            list[i] = otherList.list[i];
    }

    return *this;
}  //end overloading operator=
```

我们将为类 **arrayListType** 提供其余函数模板的定义留作练习。（参见本章末尾的编程练习 22。）

回想一下，类 **arrayListType** 是一个抽象类。因此，不能实例化它的对象。接下来我们描述从类 **arrayListType** 派生出的非抽象类 **unorderedArrayListType**。

```cpp
template <class elemType>
class unorderedArrayListType: public arrayListType<elemType>
{
public:
    void insertAt(int location, const elemType& insertItem);
    void insertEnd(const elemType& insertItem);
    void replaceAt(int location, const elemType& repItem);
    int seqSearch(const elemType& searchItem) const;
    void remove(const elemType& removeItem);

    unorderedArrayListType(int size = 100);
};    //Constructor
```

与类 **arrayListType** 的情况一样，类 **unorderedArrayListType** 的成员函数定义与第 12 章给出的定义类似。例如，函数 insertAt、seqSearch、replaceAt 和 remove 以及构造函数的定义如下：

```cpp
template <class elemType>
void unorderedArrayListType<elemType>::insertEnd
                                      (const elemType& insertItem)
{
    if (length >= maxSize) //the list is full
        cout << "Cannot insert in a full list." << endl;
    else
    {
        list[length] = insertItem; //insert the item at the end
        length++; //increment the length
    } //end insertEnd

template <class elemType>
int unorderedArrayListType<elemType>::seqSearch
                              (const elemType& searchItem) const
{
    int loc;
    bool found = false;

    for (loc = 0; loc < length; loc++)
        if (list[loc] == searchItem)
        {
            found = true;
            break;
        }

    if (found)
        return loc;
    else
        return -1;
} //end seqSearch

template <class elemType>
void unorderedArrayListType<elemType>::remove
                              (const elemType& removeItem)
{
    int loc;

    if (length == 0)
        cout << "Cannot delete from an empty list." << endl;
    else
    {
        loc = seqSearch(removeItem);

        if (loc != -1)
            removeAt(loc);
        else
            cout << "The item to be deleted is not in the list."
                 << endl;
    }
} //end remove

template <class elemType>
void unorderedArrayListType<elemType>::replaceAt(int location,
                                      const elemType& repItem)
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be "
             << "replaced is out of range." << endl;
    else
        list[location] = repItem;
}   //end replaceAt

template <class elemType>
unorderedArrayListType<elemType>::
                 unorderedArrayListType(int size)
                 : arrayListType<elemType>(size)
{
}   //end constructor
```

我们将为类 `unorderedArrayListType` 提供其余函数模板的定义留作练习。（参见本章末尾的编程练习 22。）

下面的示例说明如何使用类 `unorderedArrayListType` 处理一个字符串列表。

## 示例 13-10

下面的程序测试基于数组的列表上的各种操作。

```cpp
#include <iostream>                         //Line 1
#include <string>                           //Line 2
#include "unorderedArrayListType.h"        //Line 3

using namespace std;                        //Line 4

int main()                                  //Line 5
{                                           //Line 6
    unorderedArrayListType<string> stringList(25);   //Line 7

    string str;                             //Line 8

    cout << "Line 9: Enter 5 strings: ";   //Line 9

    for (int count = 0; count < 5; count++) //Line 10
    {                                       //Line 11
        cin >> str;                         //Line 12
        stringList.insertEnd(str);         //Line 13
    }                                       //Line 14

    cout << endl;                           //Line 15

    cout << "Line 16: stringList: ";           //Line 16
    stringList.print();                        //Line 17
    cout << endl;                              //Line 18

    cout << "Line 19: Enter the string to be " //Line 19
         << "deleted: ";                       //Line 20
    cin >> str;                                //Line 21
    cout << endl;                              //Line 22

    stringList.remove(str);                    //Line 23
    cout << "Line 23: After removing " << str //Line 24
         << " stringList: ";                   //Line 25
    stringList.print();                        //Line 26
    cout << endl;                              //Line 27

    cout << "Line 26: Enter the search item: "; //Line 28

    cin >> str;                                //Line 29
    cout << endl;                              //Line 30

    if (stringList.seqSearch(str) != -1)       //Line 29
        cout << "Line 30: " << str             //Line 30
             << " found in stringList." << endl; //Line 31
    else                                       //Line 32
        cout << "Line 32: " << str             //Line 32
             << " is not in stringList." << endl; //Line 33

    return 0;                                  //Line 34
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Line 9: Enter 5 strings: fall winter spring summer green
Line 16: stringList: fall winter spring summer green
Line 19: Enter the string to be deleted: winter
Line 23: After removing winter stringList: fall spring summer green
Line 26: Enter the search item: summer
Line 30: summer found in stringList.
```

前面的程序按如下方式工作。第 7 行的语句将 `stringList` 声明为 `unorderedArrayListType` 类型的对象。`stringList` 的成员变量 `list` 是一个包含 25 个分量的数组，分量类型为 `string`。第 8 行的语句声明 `string` 变量 `str`。第 9 行的语句提示用户输入 5 个字符串。第 12 行的语句从输入流中获取下一个字符串。第 13 行的语句使用 `stringList` 的成员函数 `insertEnd` 将该字符串存储到 `stringList` 中。第 17 行的语句使用 `stringList` 的成员函数 `print` 输出 `stringList` 的元素。第 19 行的语句提示用户输入要从 `stringList` 中删除的字符串，第 20 行的语句获取要删除的字符串

