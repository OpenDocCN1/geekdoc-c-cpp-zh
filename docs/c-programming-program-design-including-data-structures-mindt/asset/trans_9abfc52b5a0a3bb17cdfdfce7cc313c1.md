
接下来给出 `class candidateType` 中函数的定义。

要设置特定区域的票数，将区域编号和票数作为参数传递给函数 `setVotes`。因为数组下标从 0 开始，所以区域 1 对应位置 0 的数组元素，依此类推。因此，为了设置正确数组元素的值，需要从区域编号中减去 1。函数 `setVotes` 的定义如下：

```cpp
void candidateType::setVotes(int region, int votes)
{
    votesByRegion[region - 1] = votes;
}
```

要更新特定区域的票数，将区域编号和该区域的票数作为参数传入。然后将这些票数加到该区域先前的值上。函数 `updateVotesByRegion` 的定义如下：

```cpp
void candidateType::updateVotesByRegion(int region, int votes)
{
    votesByRegion[region - 1] = votesByRegion[region - 1]
                              + votes;
}
```

函数 `calculateTotalVotes`、`getTotalVotes`、`printData` 以及默认构造函数的定义相当直接，下面给出。

```cpp
void candidateType::calculateTotalVotes()
{
    totalVotes = 0;

    for (int i = 0; i < NO_OF_REGIONS; i++)
        totalVotes += votesByRegion[i];
}
```

```cpp
int candidateType::getTotalVotes() const
{
    return totalVotes;
}
```

```cpp
void candidateType::printData() const
{
    cout << left
         << setw(8) << firstName << " "
         << setw(8) << lastName << " ";

    cout << right;
    for (int i = 0; i < NO_OF_REGIONS; i++)
        cout << setw(8) << votesByRegion[i] << " ";
    cout << setw(7) << totalVotes << endl;
}
```

```cpp
candidateType::candidateType()
{
    for (int i = 0; i < NO_OF_REGIONS; i++)
        votesByRegion[i] = 0;

    totalVotes = 0;
}
```

要为 `class candidateType` 重载关系运算符，需要比较候选人的姓名。例如，如果两个候选人的姓名相同，则它们相同。这些函数的定义与为 `class personType` 重载关系运算符的函数定义类似，下面给出。

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

```cpp
const candidateType& candidateType::operator=
                                      (const candidateType& right)
{
    if (this != &right)  // avoid self-assignment
    {
        firstName = right.firstName;
        lastName = right.lastName;

        for (int i = 0; i < NO_OF_REGIONS; i++)
            votesByRegion[i] = right.votesByRegion[i];

        totalVotes = right.totalVotes;
    }

    return *this;
}

const candidateType& candidateType::operator=
                                      (const personType& right)
{
    firstName = right.getFirstName();
    lastName = right.getLastName();

    return *this;
}
```

## 主程序

既然 `class` `candidateType` 已经设计和实现完毕，我们现在重点关注主程序的设计。

因为有六名候选人，我们创建一个列表 `candidateList`，其中包含六个 `candidateType` 类型的元素。程序首先应该做的，是从文件 `candData.txt` 中将每位候选人的姓名读入列表 `candidateList`。然后，我们对 `candidateList` 进行排序。

下一步是处理来自文件 `voteData.txt` 的投票数据，该文件保存投票数据。处理完投票数据后，程序应计算每位候选人获得的总票数并打印这些数据，如前所示。因此，总体算法如下：

- 1. 将每位候选人的姓名读入 `candidateList`。
- 2. 对 `candidateList` 排序。
- 3. 处理投票数据。
- 4. 计算每位候选人获得的总票数。
- 5. 打印结果。

下面的语句创建对象 `candidateList`：

```cpp
unorderedArrayListType<candidateType> candidateList(NO_OF_CANDIDATES);
```

图 18-40 显示了对象 `candidateList`。数组列表的每个元素都是 `candidateType` 类型的对象。

![](img/b217c421655b51e7494cf3b89bb5432d_1387_0.png)

**图 18-40** `candidateList`

在图 18-40 中，数组 `votesByRegion` 和变量 `totalVotes` 由 `candidateType` 类的默认构造函数初始化为 0。为了节省空间，在需要时，我们将按图 18-41 所示绘制对象 `candidateList`。

![](img/b217c421655b51e7494cf3b89bb5432d_1387_1.png)

**图 18-41** `candidateList`

程序必须做的第一件事，是将候选人姓名读入 `candidateList`。因此，我们编写一个函数来完成这项任务。文件 `candData.txt` 在函数 `main` 中打开。因此，输入文件名和 `candidateList` 被作为参数传递给函数 `fillNames`。由于对象 `candidateList` 的成员变量 list 是受保护的，不能直接访问。因此，我们创建一个 `candidateType` 类型的对象 temp 来存储候选人姓名，并使用函数 `insertEnd`（属于 list）将每位候选人的姓名存入对象 `candidateList`。函数 `fillNames` 的定义如下：

```cpp
void fillNames(ifstream& inFile,
               unorderedArrayListType<candidateType>& cList)
{
    string firstN;
    string lastN;
    candidateType temp;

    for (int i = 0; i < NO_OF_CANDIDATES; i++)
    {
        inFile >> firstN >> lastN;
        temp.setName(firstN, lastN);
        cList.insertEnd(temp);
    }
}
```

图 18-42 显示了调用函数 `fillNames` 之后的对象 `candidateList`。

![](img/b217c421655b51e7494cf3b89bb5432d_1389_0.png)

**图 18-42** 调用函数 fillNames 后的对象 candidateList

### 对姓名排序

读取候选人姓名后，我们接下来使用本章讨论的任意一种（基于数组的）排序算法，对对象 `candidateList` 的数组列表进行排序。因为 `candidateList` 是 `unorderedArrayListType` 类型的对象，所以我们使用成员函数 `sort` 对 `candidateList` 进行排序。（为便于说明，我们在函数 `sort` 中使用选择排序。实际上，你可以使用本章讨论的任意一种基于数组的排序算法。）下面的语句完成这项任务：

```cpp
candidateList.sort();
```

执行该语句后，`candidateList` 如图 18-43 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1390_0.png)

**图 18-43** 语句 `candidateList.sort();` 执行后的对象 candidateList

### 处理：投票数据

处理投票数据相当直接。文件 `voteData.txt` 中的每条记录形式如下：

```text
firstName lastName regionNumber numberOfVotes
```

从文件 `voteData.txt` 读取一条记录后，我们在（对象 `candidateList` 的）数组列表中找到与该特定候选人对应的行，并更新由 `regionNumber` 指定的记录。

分量 `votesByRegion` 是数组列表每个元素的私有成员。此外，`list` 是 `candidateList` 的私有成员。更新某位候选人票数的唯一方法是：将该候选人的记录复制到一个临时对象中，更新该对象，然后通过用临时对象的新值替换旧值，将该临时对象复制回 `list`。我们可以使用成员函数 `retrieveAt` 复制需要更新票数的候选人。更新临时对象后，我们可以使用成员函数 `replaceAt` 将临时对象复制回列表。假设接下来读取的记录是

```text
Lisa Fisher  2  35
```

这条记录表示 Lisa Fisher 从区域 2 获得了 35 票。假设在处理这条记录之前，`candidateList` 如图 18-44 所示。
