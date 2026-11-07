

以下语句将 `listType` 定义为一个类模板：

```cpp
template<class elemType>
class listType
{
public:
    bool isEmpty() const;
    //Function to determine whether the list is empty.
    //Postcondition: Returns true if the list is empty,
    //               otherwise it returns false.

    bool isFull() const;
    //Function to determine whether the list is full.
    //Postcondition: Returns true if the list is full,
    //               otherwise it returns false.

    bool search(const elemType& searchItem) const;
    //Function to search the list for searchItem.
    //Postcondition: Returns true if searchItem
    //               is found in the list, and
    //               false otherwise.

    void insert(const elemType& newElement);
    //Function to insert newElement in the list.
    //Precondition: Prior to insertion, the list must
    //              not be full.
    //Postcondition: The list is the old list plus
    //               newElement.

    void remove(const elemType& removeElement);
    //Function to remove removeElement from the list.
    //Postcondition: If removeElement is found in the list,
    //               it is deleted from the list, and the
    //               list is the old list minus removeElement.
    //               If the list is empty, output the message
    //               "Cannot delete from the empty list."

    void destroyList();
    //Function to destroy the list.
    //Postcondition: length = 0;

    void printList();
    //Function to output the elements of the list.

    listType();
    //default constructor
    //Sets the length of the list to 0.
    //Postcondition: length = 0;

protected:
    elemType list[100];    //array to hold the list elements
    int length;            //variable to store the number of
                           //elements in the list
};
```

类模板 `listType` 的这个定义是一个通用定义，只包含列表的基本操作。为了从这个列表派生出特定的列表，并添加或重写操作，我们将包含列表元素的数组和列表长度声明为 `protected`。

接下来，我们描述一个具体的列表。假设你想创建一个用于处理整数数据的列表。语句

```cpp
listType<int> intList;                    //line 1
```

将 `intList` 声明为 `listType` 的一个对象。`protected` 成员 `list` 是一个包含 100 个组件的数组，每个组件的类型都是 `int`。类似地，语句

```cpp
listType<newString> stringList;           //line 2
```

将 `stringList` 声明为 `listType` 的一个对象。`protected` 成员 `list` 是一个包含 100 个组件的数组，每个组件的类型都是 `newString`。

在第 1 行和第 2 行的语句中，`listType<int>` 和 `listType<newString>` 被称为*模板实例化*或*类模板 `listType<elemType>` 的实例化*，其中 `elemType` 是模板头中的类参数。模板实例化可以使用内置类型或用户定义类型创建。

类模板的函数成员被视为函数模板。因此，在给出类模板的函数成员的定义时，我们必须遵循函数模板的定义。例如，类 `listType` 的成员 `insert` 的定义为：

```cpp
template <class elemType>
void listType<elemType>::insert(const elemType& newElement)
{
    .
    .
    .
}
```

在成员函数定义的首部中，类名通过参数 `elemType` 来指定。

第 1 行的语句将 `intList` 声明为包含 100 个组件的列表。当编译器为 `intList` 生成代码时，它会将类 `listType` 定义中的 `elemType` 替换为 `int`。类 `listType` 的成员函数定义中的模板参数（例如，`insert` 定义中的 `elemType`）也会被替换为 `int`。

## 类模板的头文件和实现文件

到目前为止，我们都是将类的定义（放在头文件中）和成员函数的定义（放在实现文件中）放在不同的文件中。目标代码由实现文件生成，并与用户代码链接。然而，这种将类定义和成员函数定义分离的机制不适用于类模板。向函数传递参数在运行时产生效果，而向类模板传递参数则在编译时产生效果。由于类的实际参数是在用户代码中指定的，而且编译器在没有模板实际参数的情况下无法实例化函数模板，因此我们不能再独立于用户代码来编译实现文件。

这个问题有几种可能的解决方案。我们可以将类定义和函数模板的定义直接放在客户代码中，或者将类定义和函数模板的定义放在同一个头文件中。另一种替代方案是像通常那样将类定义和函数定义放在不同的文件中，但在头文件的末尾包含一条指向实现文件的指令。在这种情况下，函数定义和客户代码将一起编译。为了便于说明，我们将类定义和函数定义放在同一个头文件中。

## 基于数组的列表（再探）

在第 12 章中，我们设计了 **arrayListType**、**unorderedArrayListType** 和 **orderedArrayListType** 类来处理数组中的列表。然而，第 12 章中设计的这些类只能处理元素类型为 `int` 的列表。既然我们已经讨论了如何使用类模板创建通用列表，在本节中，我们将重新设计这些类，使它们能够处理任何类型的列表。此外，在本章中，我们讨论了如何重载赋值运算符。因此，除了第 12 章讨论的操作之外，我们还为 **arrayListType** 类重载了赋值运算符，因为它有一个指针成员变量。

下面的类模板将抽象类 `arrayListType` 定义为一个 ADT。（为节省篇幅，我们只列出函数。这些函数的文档说明与第 12 章中给出的类似。本书随附网站上的源代码文件包含这些函数的文档说明。）

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
    virtual void insertEnd(const elemType& insertItem) = 0;
    void removeAt(int location);
    void retrieveAt(int location, elemType& retItem) const;
    virtual void replaceAt(int location, const elemType& repItem) = 0;
    void clearList();
    virtual int seqSearch(const elemType& searchItem) const = 0;
    virtual void remove(const elemType& removeItem) = 0;

    arrayListType(int size = 100);
    //Constructor
    arrayListType(const arrayListType<elemType>& otherList);
    //Copy constructor

    virtual ~arrayListType();

protected:
    elemType *list; //array to hold the list elements
    int length;     //variable to store the length of the list
    int maxSize;    //variable to store the maximum
                    //size of the list
};
```

实现类 `arrayListType` 操作的那些函数定义与第 12 章中给出的类似。这里的这些操作函数都是函数模板。例如，函数 `print`、`isItemAtEqual`、`removeAt`、`retrieveAt`、构造函数和析构函数的定义如下：

```cpp
template <class elemType>
void arrayListType<elemType>::print() const
{
    for (int i = 0; i < length; i++)
        cout << list[i] << " ";
    cout << endl;
}   //end print

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
}   //end isItemAtEqual
```

