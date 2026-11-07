
## 基于数组的列表（再论）

在第12章中，我们设计了类 `arrayListType`、`unorderedArrayListType` 和 `orderedArrayListType`，用于处理数组中的列表。然而，按照第12章的设计，这些类只能处理元素类型为 `int` 的列表。既然我们已经讨论了如何使用类模板来创建泛型代码，那么在本节中，我们将重新设计这些类，使它们能够用于处理任意类型的列表。此外，在本章中，我们讨论了如何重载赋值运算符。因此，除了第12章中讨论的操作之外，我们还为类 `arrayListType` 重载了赋值运算符，因为它有一个指针成员变量。

下面的类模板将抽象类 `arrayListType` 定义为 ADT。（为节省篇幅，我们只列出这些函数。这些函数的文档说明与第12章给出的类似。本书配套网站上的源代码文件包含这些函数的文档说明。）

```cpp
template <class elemType>
class arrayListType
{
public:
    const arrayListType<elemType>&
                    operator=(const arrayListType<elemType>&);

                    //Overloads the assignment operator

    bool isEmpty() const;
    bool isFull() const;
    int listSize() const;
    int maxListSize() const;
    void print() const;
    bool isItemAtEqual(int location, const elemType& item) const;
    virtual void insertAt(int location, const elemType& insertItem) = 0;
    virtual void insertEnd(const elemType& insertItem = 0);
    void removeAt(int location);
    void retrieveAt(int location, elemType& retItem) const;
    virtual void replaceAt(int location, const elemType& repItem) = 0;
    void clearList();
    virtual int seqSearch(const elemType& searchItem) const = 0;
    virtual void remove(const elemType& removeItem) = 0;
    arrayListType(int size = 100);
    arrayListType (const arrayListType<elemType>& otherList);
    virtual ~arrayListType();

protected:
    elemType *list;  //array to hold the list elements
    int length;      //variable to store the length of the list
    int maxSize;     //variable to store the maximum
                     //size of the list
};
```

实现类 `arrayListType` 各操作的函数定义与第12章给出的类似。在这里，实现这些操作的函数是函数模板。例如，函数 `print`、`isItemAtEqual`、`removeAt`、`retrieveAt`、构造函数和析构函数的定义如下：

```cpp
template <class elemType>
void arrayListType<elemType>::print() const
{
    for (int i = 0; i < length; i++)
        cout << list[i] << " ";
    cout << endl;
}

template <class elemType>
bool arrayListType<elemType>::isItemAtEqual(int location,
                                            const elemType& item) const
{
    if (location < 0 || location >= length)
    {
        cout << "The location of the item to be removed "
             << "is out of range." << endl;
        return false;
    }
    else
        return (list[location] == item);
} //end isItemAtEqual

template <class elemType>
void arrayListType<elemType>::removeAt(int location)
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be removed "
             << "is out of range." << endl;
    else
    {
        for (int i = location; i < length - 1; i++)
            list[i] = list[i + 1];

        length--;
    }
} //end removeAt

template <class elemType>
void arrayListType<elemType>::retrieveAt(int location,
                                         elemType& retItem) const
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be retrieved is "
             << "out of range" << endl;
    else
        retItem = list[location];
} //end retrieveAt
```

```cpp
template <class elemType>
arrayListType<elemType>::arrayListType(int size)
{
    if (size <= 0)
    {
        cout << "The array size must be positive. Creating "
             << "an array of the size 100. " << endl;

        maxSize = 100;
    }
    else
        maxSize = size;

    length = 0;

    list = new elemType[maxSize];
}
```

```cpp
template <class elemType>
arrayListType<elemType>::~arrayListType()
{
    delete [] list;
}
```

接下来，由于我们正在为类 arrayListType 重载赋值运算，因此给出用于重载赋值运算符的函数模板的定义。

```cpp
template <class elemType>
const arrayListType<elemType>& arrayListType<elemType>::
    operator=(const arrayListType<elemType>& otherList)
{
    if (this != &otherList)    //avoid self-assignment
    {
        delete [] list;
        maxSize = otherList.maxSize;
        length = otherList.length;

        list = new elemType[maxSize];

        for (int i = 0; i < length; i++)
            list[i] = otherList.list[i];
    }
    return *this;
}
```

我们将为类 arrayListType 提供其余函数模板的定义留作练习。（参见本章末尾的编程练习20。）

回顾一下，类 arrayListType 是一个抽象类，因此不能实例化它的对象。接下来我们描述派生自类 arrayListType 的非抽象类 unorderedArrayListType。

```cpp
template <class elemType>
class unorderedArrayListType: public arrayListType <elemType>
{
public:
    void insertAt(int location, const elemType& insertItem);
    void insertEnd(const elemType& insertItem);
    void replaceAt(int location, const elemType& repItem);
    int seqSearch(const elemType& searchItem) const;
    void remove(const elemType& removeItem);

    unorderedArrayListType(int size = 100);
        //Constructor
};
```

与类 arrayListType 的情况一样，类 unorderedArrayListType 的成员函数定义与第12章给出的类似。例如，函数 insertEnd、seqSearch、replaceAt 和 remove 以及构造函数的定义如下：

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
    }
} //end insertEnd
```

```cpp
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
```

```cpp
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
} //end replaceAt

template <class elemType>
unorderedArrayListType<elemType>::
          unorderedArrayListType(int size)
              : arrayListType<elemType>(size)
{
}
```

我们将为类 unorderedArrayListType 提供其余函数模板的定义留作练习。（参见本章末尾的编程练习20。）

下面的示例说明如何使用类 unorderedArrayListType 处理字符串列表。
