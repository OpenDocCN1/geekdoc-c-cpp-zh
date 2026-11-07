
```cpp
else
{
    for (int i = location; i < length - 1; i++)
        list[i] = list[i+1];
    length--;
} //end removeAt
```

函数 retrieveAt 的定义很直接。要检索项的索引以及要检索该项的位置作为参数传递给该函数。该函数的定义如下：

```cpp
void arrayListType::retrieveAt(int location, int& retItem) const
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be retrieved is "
             << "out of range" << endl;
    else
        retItem = list[location];
} //end retrieveAt
```

函数 clearList 从列表中删除元素，使列表为空。由于成员变量 length 表示列表中元素的数量，因此只需将 length 设为 0 即可删除这些元素。因此，该函数的定义如下：

```cpp
void arrayListType::clearList()
{
    length = 0;
} //end clearList
```

现在讨论构造函数和析构函数的定义。构造函数创建用户指定大小的数组，并将列表的 length 初始化为 0，将 maxSize 初始化为用户指定的数组大小。数组大小作为参数传递给构造函数。默认数组大小为 100。析构函数释放保存列表元素的数组所占用的内存。构造函数和析构函数的定义如下：

```cpp
arrayListType::arrayListType(int size)
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

    list = new int[maxSize];
} //end constructor
```

```cpp
arrayListType::~arrayListType()
{
    delete [] list;
} //end destructor
```

接下来描述复制构造函数。回想一下，当对象作为（值）参数传递给函数时，以及当使用同类型另一个对象的值声明并初始化对象时，会调用复制构造函数。它将实际对象的成员变量值复制到形参以及正在创建的对象的相应成员变量中。其定义如下：

```cpp
arrayListType::arrayListType(const arrayListType& otherList)
{
    maxSize = otherList.maxSize;
    length = otherList.length;

    list = new int[maxSize]; //create the array

    for (int j = 0; j < length; j++)  //copy otherList
        list[j] = otherList.list[j];
} //end copy constructor
```

### 无序列表

如上一节所述，我们从抽象类 arrayListType 派生出类 unorderedArrayListType，并实现操作 insertAt、insertEnd、replaceAt、seqSearch、insert 和 remove。

类 unorderedArrayListType 的定义如下：（为节省篇幅，我们列出成员函数时不附带文档说明。这些函数的描述与类 arrayListType 中函数的描述相同。）

```cpp
class unorderedArrayListType: public arrayListType
{
public:
    void insertAt(int location, int insertItem);
    void insertEnd(int insertItem);
    void replaceAt(int location, int repItem);
    int seqSearch(int searchItem) const;
    void remove(int removeItem);

    unorderedArrayListType(int size = 100);
      //Constructor.
};
```

我们将类 unorderedArrayListType 的 UML 类图及其继承层次结构留作练习。

函数 insertAt 将一项插入列表中的特定位置。要插入的项以及数组中的插入位置作为参数传递给该函数。为了将该项插入列表中间某处，我们必须先为新项腾出空间。也就是说，我们需要将某些元素向下移动一个数组槽位。考虑图 12-24 中的列表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_926_0.png)

当前列表中的元素数量为 6，因此 length 为 6。因此，插入一个新元素后，列表的 length 为 7。如果要将该项插入到例如位置 6，我们可以通过将该项复制到 list[6] 中轻松完成。另一方面，如果要将该项插入到例如位置 3，我们首先需要将元素 list[3]、list[4] 和 list[5] 向右移动一个数组槽位，以便为新项腾出空间。因此，我们必须按此顺序先将 list[5] 复制到 list[6]，将 list[4] 复制到 list[5]，并将 list[3] 复制到 list[4]。然后就可以将新项复制到 list[3] 中。

当然，诸如尝试向已满列表插入等特殊情况必须单独处理。其中一些情况可以通过其他成员函数完成。

函数 insertAt 的定义如下：

```cpp
    void unorderedArrayListType::insertAt(int location,
                                          int insertItem)
    {
        if (location < 0 || location >= maxSize)
            cout << "The position of the item to be inserted "
                 << "is out of range." << endl;
        else if (length >= maxSize)  //list is full
            cout << "Cannot insert in a full list" << endl;
        else
        {
            for (int i = length; i > location; i--)
                list[i] = list[i - 1];  //move the elements down

            list[location] = insertItem;  //insert the item at
                                          //the specified position

            length++;  //increment the length
        }
    } //end insertAt
```

函数 insertEnd 可以通过使用函数 insertAt 来实现。然而，函数 insertEnd 不需要移动元素。因此，我们直接给出其定义。

```cpp
    void unorderedArrayListType::insertEnd(int insertItem)
    {
        if (length >= maxSize)  //the list is full
            cout << "Cannot insert in a full list." << endl;
        else
        {
            list[length] = insertItem; //insert the item at the end
            length++; //increment the length
        }
    } //end insertEnd
```

第 8 章描述了**顺序或线性**查找。为便于参考并保证完整性，下面给出基于数组的列表的顺序查找算法：

```cpp
int unorderedArrayListType::seqSearch(int searchItem) const
{
    int loc;
    bool found = false;

    loc = 0;

    while (loc < length && !found)
        if (list[loc] == searchItem)
            found = true;
        else
            loc++;

    if (found)
        return loc;
    else
        return -1;
} //end seqSearch
```

函数 remove 从列表中删除一项。要删除的项作为参数传递给该函数。为了删除该项，该函数调用成员函数 seqSearch 来确定要删除的项是否在列表中。如果要删除的项在列表中找到，则从列表中删除该项，并将列表的 length 减 1。如果要删除的项在列表中找到，函数 seqSearch 返回要删除的项在列表中的索引。现在可以使用函数 seqSearch 返回的索引，并使用函数 removeAt 从列表中删除该项。因此，函数 remove 的定义如下：

```cpp
void unorderedArrayListType::remove(int removeItem)
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
```

函数 replaceAt 的定义如下：

```cpp
void unorderedArrayListType::replaceAt(int location, int repItem)
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be "
             << "replaced is out of range." << endl;
```
