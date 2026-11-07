
在第1行和第2行的语句中，listType<int> 和 listType<string> 被称为模板实例化，或类模板 listType<elemType> 的实例化，其中 elemType 是模板头中的类参数。模板实例化既可以使用内置类型创建，也可以使用用户定义类型创建。

类模板的函数成员被视为函数模板。因此，在给出类模板的函数成员定义时，必须遵循函数模板的定义。例如，类 listType 的成员 insert 的定义为：

```cpp
template <class elemType>
void listType<elemType>::insert(elemType newElement)
{
    .
    .
    .
}
```

在成员函数定义的头中，类名通过参数 elemType 指定。

第1行中的语句将 intList 声明为包含100个分量的列表。当编译器为 intList 生成代码时，会在类 listType 的定义中将单词 elemType 替换为 int。类 listType 的成员函数定义中的模板参数（例如 insert 定义中的 elemType）也会被替换为 int。

### 类模板的头文件和实现文件

到目前为止，我们将类的定义（放在头文件中）和成员函数的定义（放在实现文件中）放在不同的文件里。目标代码由实现文件生成，并与用户代码链接。然而，这种将类定义与成员函数定义分离的机制对类模板不起作用。向函数传递参数在运行时生效，而向类模板传递参数在编译时生效。由于类的实际参数在用户代码中指定，并且编译器在没有模板实际参数的情况下无法实例化函数模板，我们不能再独立于用户代码编译实现文件。

这个问题有几种可能的解决方案。我们可以将类定义和函数模板的定义直接放在客户端代码中，也可以将类定义和函数模板的定义一起放在同一个头文件中。另一种替代方案是（像通常一样）将类定义和函数定义放在不同文件中，但在头文件末尾包含一条指向实现文件的指令。无论哪种情况，函数定义和客户端代码都会一起编译。为便于说明，我们将把类定义和函数定义放在同一个头文件中。

下面的示例演示类模板的使用。

## 基于数组的列表（再探）

在第13章中，我们设计了类 `arrayListType`、`unorderedArrayListType` 和 `orderedArrayListType`，用于处理数组中的列表。然而，这些类按第13章中的设计只能处理元素类型为 int 的列表。既然我们已经讨论了如何使用类模板创建泛型代码，本节将重新设计这些类，使其可用于处理任意类型的列表。此外，本章还讨论了如何重载赋值运算符。因此，除了第13章讨论的操作外，我们还将为类 `arrayListType` 重载赋值运算符，因为它有一个指针成员变量。

下面的类模板将抽象类 `arrayListType` 定义为 ADT。（为节省篇幅，这里只列出函数。这些函数的文档说明与第13章给出的类似。本书配套网站上的源代码文件包含这些函数的文档说明。）

```cpp
template <class elemType>
class arrayListType
{
public:
    const arrayListType<elemType> &
                 operator=(const arrayListType<elemType>&);
    //overloads the assignment operator

    bool isEmpty() const;
    bool isFull() const;
    int listSize() const;
    int maxListSize();
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
    arrayListType(const arrayListType<elemType>& otherList);
    virtual ~arrayListType();

protected:
    elemType *list;  //array to hold the list elements
    int length;      //variable to store the length of the list
    int maxSize;     //variable to store the maximum
                     //size of the list
};
```

实现 `class` arrayListType 操作的函数定义与第13章给出的类似。这里实现这些操作的函数是函数模板。例如，函数 print、isItemAtEqual、removeAt、retrieveAt、构造函数和析构函数的定义如下：

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

template <class elemType>
arrayListType<elemType>::arrayListType(int size)
{
    if (size <= 0)
    {
        cout << "The array size must be positive. Creating "
             << "an array of the size 100." << endl;

        maxSize = 100;
    }
    else
        maxSize = size;

    length = 0;

    list = new elemType[maxSize];
}

template <class elemType>
arrayListType<elemType>::~arrayListType()
{
    delete [] list;
}
```

接下来，由于我们正在为类 arrayListType 重载赋值运算，因此给出用于重载赋值运算符的函数模板定义。

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

我们将为类 `arrayListType` 提供其余函数模板的定义留作练习。（见本章末尾的编程练习18。）

回顾一下，类 `arrayListType` 是抽象类，因此不能实例化其对象。接下来我们描述从类 `arrayListType` 派生的非抽象类 `unorderedArrayListType`。

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

与类 `arrayListType` 的情况一样，类 `unorderedArrayListType` 的成员函数定义与第13章给出的类似。例如，函数 `insertEnd`、`seqSearch`、`replaceAt` 和 `remove` 以及构造函数的定义如下：

```cpp
template <class elemType>
void unorderedArrayListType<elemType>::insertEnd
                                      (const elemType& insertItem)
{
    if (length >= maxSize)    //the list is full
        cout << "Cannot insert in a full list." << endl;
    else
    {
        list[length] = insertItem; //insert the item at the end
        length++; //increment the length
    } //end insertEnd
}
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
```
