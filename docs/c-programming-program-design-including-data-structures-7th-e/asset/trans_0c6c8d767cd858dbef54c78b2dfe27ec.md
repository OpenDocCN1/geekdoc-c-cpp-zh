

```cpp
candidateType::candidateType()
{
    for (int i = 0; i < NO_OF_REGIONS; i++)
        votesByRegion[i] = 0;

    totalVotes = 0;
}
```

为了重载类 `candidateType` 的关系运算符，需要对候选人的姓名进行比较。例如，如果两个候选人的姓名相同，则他们是同一个人。这些函数的定义与类 `personType` 的重载关系运算符函数的定义类似，具体如下所示。

```cpp
bool candidateType::operator==(const candidateType& right) const
{
    return (firstName == right.firstName
            && lastName == right.lastName);
}

bool candidateType::operator!=(const candidateType& right) const
{
    return (firstName != right.firstName
            || lastName != right.lastName);
}

bool candidateType::operator<=(const candidateType& right) const
{
    return (lastName <= right.lastName ||
            (lastName == right.lastName &&
             firstName <= right.firstName));
}

bool candidateType::operator<(const candidateType& right) const
{
    return (lastName < right.lastName ||
            (lastName == right.lastName &&
             firstName < right.firstName));
}

bool candidateType::operator>=(const candidateType& right) const
{
    return (lastName >= right.lastName ||
            (lastName == right.lastName &&
             firstName >= right.firstName));
}

bool candidateType::operator>(const candidateType& right) const
{
    return (lastName > right.lastName ||
            (lastName == right.lastName &&
             firstName > right.firstName));
}
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_1376_0.png)

**图 18-40** `candidateList`

在图 18-40 中，数组 `votesByRegion` 和变量 `totalVotes` 由类 `candidateType` 的默认构造函数初始化为 0。为了节省空间，在需要时我们会将对象 `candidateList` 绘制成如图 18-41 所示的形式。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1376_1.png)

**图 18-41** `candidateList`

程序要做的第一件事是将候选人的姓名读入 `candidateList`。因此，我们编写一个函数来完成此任务。文件 `candData.txt` 在函数 `main` 中打开。因此，输入文件的名称和 `candidateList` 作为参数传递给函数 `fillNames`。由于对象 `candidateList` 的成员变量 `list` 是 `protected` 的，因此不能直接访问。因此，我们创建一个 `candidateType` 类型的对象 `temp` 来存储候选人的姓名，并使用（`list` 的）函数 `insertEnd` 将每位候选人的姓名存储到对象 `candidateList` 中。函数 `fillNames` 的定义如下：

```cpp
void fillNames(ifstream& inFile,
               unorderedLinkedListType<candidateType>& cList)
{
    string firstN;
    string lastN;
    int i;
    candidateType temp;

    for (i = 0; i < NO_OF_CANDIDATES; i++)
    {
        inFile >> firstN >> lastN;
        temp.setName(firstN, lastN);
        cList.insertEnd(temp);
    }
}
```

图 18-42 显示了调用函数 `fillNames` 之后对象 `candidateList` 的状态。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1378_0.png)

**图 18-42** 调用函数 `fillNames` 后的对象 `candidateList`

## 排序姓名

读取候选人的姓名后，接下来我们使用本章讨论的任何一种（基于数组的）排序算法对对象 `candidateList` 的数组列表进行排序。由于 `candidateList` 是 `unorderedArrayListType` 类型的对象，我们使用成员函数 `sort` 对 `candidateList` 进行排序。（为了便于说明，我们在函数 `sort` 中使用选择排序。实际上，你可以使用本章讨论的任何基于数组的排序算法。）以下语句完成此任务：

```cpp
candidateList.sort();
```

此语句执行后，`candidateList` 如图 18-43 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1379_0.png)

**图 18-43** 语句 `candidateList.sort();` 执行后的对象 `candidateList`

## 处理投票数据

处理投票数据非常简单。文件 `voteData.txt` 中的每个条目格式如下：

```
firstName lastName regionNumber numberOfVotes
```

从文件 `voteData.txt` 读取一个条目后，我们在数组 `list`（即对象 `candidateList` 的）中找到与特定候选人对应的行，并更新由 `regionNumber` 指定的条目。

分量 `votesByRegion` 是数组 `list` 的每个分量的**私有**成员。此外，`list` 是 `candidateList` 的**私有**成员。要更新某位候选人的票数，唯一的方法是先将该候选人的记录复制到一个临时对象中，更新该对象，然后用临时对象的新值替换旧值，将其复制回 `list`。我们可以使用成员函数 `retrieveAt` 复制需要更新票数的候选人记录。更新临时对象后，我们可以使用成员函数 `replaceAt` 将临时对象复制回 `list`。假设读取到的下一个条目是：

```
Lisa Fisher 2 35
```

该条目表示 Lisa Fisher 从第 2 选区获得了 35 票。假设在处理该条目之前，`candidateList` 如图 18-44 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1380_0.png)

**图 18-44** 处理条目 `Lisa Fisher 2 35` 之前的对象 `candidateList`

我们复制与 Lisa Fisher 对应的行（见图 18-45）。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1380_1.png)

**图 18-45** 对象 `temp`

接下来，以下语句更新第 2 选区的投票数据。（此处，region = 2，votes = 35。）

```cpp
temp.updateVotesByRegion(region, votes);
```

此语句执行后，对象 `temp` 如图 18-46 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1381_0.png)

**图 18-46** `temp.updateVotesByRegion(region, votes);` 执行后的对象 `temp`

现在我们将对象 `temp` 复制到 `list` 中（见图 18-47）。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1381_1.png)

**图 18-47** 复制 `temp` 后的 `candidateList`

由于 `candidateList` 的成员 `list` 已排序，我们可以使用二分查找算法在 `list` 中找到需要更新票数的候选人所在的行位置。本质上，函数 `processVotes` 的定义如下：

```cpp
void processVotes(ifstream& inFile,
                  unorderedArrayListType<candidateType>& cList)
{
    string firstN;
    string lastN;
    int region;
    int votes;
    int candLocation;

    candidateType temp;

    inFile >> firstN >> lastN >> region >> votes;

    temp.setName(firstN, lastN);
    temp.setVotes(region, votes);

    while (inFile)
    {
        candLocation = cList.binSearch(temp);

        if (candLocation != -1)
        {
            cList.retrieveAt(candLocation, temp);
            temp.updateVotesByRegion(region, votes);
            cList.replaceAt(candLocation, temp);
        }

        inFile >> firstN >> lastN >> region >> votes;

        temp.setName(firstN, lastN);
        temp.setVotes(region, votes);
    }
}
```

## 累加票数

处理完投票数据后，下一步是计算每位候选人获得的总票数。这可以通过将每个选区的票数相加来完成。

现在 `votesByRegion` 是 `candidateType` 的私有成员，而 `list` 是 `candidateList` 的受保护成员。因此，要为每位候选人累加票数，我们使用函数 `retrieveAt` 制作每位候选人数据的临时副本，在临时对象中累加票数，然后将临时对象复制回 `candidateList`。以下函数完成此操作：

```cpp
void addVotes(unorderedArrayListType<candidateType>& cList)
{
    int i;

    candidateType temp;

    for (i = 0; i < NO_OF_CANDIDATES; i++)
    {
        cList.retrieveAt(i, temp);
        temp.calculateTotalVotes();
        cList.replaceAt(i, temp);
    }
}
```

