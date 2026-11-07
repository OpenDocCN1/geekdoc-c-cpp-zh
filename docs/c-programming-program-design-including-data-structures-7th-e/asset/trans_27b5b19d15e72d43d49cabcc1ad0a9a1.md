
现在我们给出实现 `personType` 类各种操作的函数定义。

成员函数 `setName`、`getFirstName`、`getLastName` 以及构造函数的定义与第 10 章给出的定义相同。因此，我们考虑重载关系运算符和流运算符的函数的定义。

如果两个人的名和姓都相同，则他们的姓名相同。因此，重载相等运算符的函数的定义如下：

```cpp
bool personType::operator==(const personType& right) const
{
    return (firstName == right.firstName
            && lastName == right.lastName);
}
```

如果两个人的名或姓不同，则他们的姓名不同。因此，重载不等于运算符的函数的定义如下：

```cpp
bool personType::operator!=(const personType& right) const
{
    return (firstName != right.firstName
            || lastName != right.lastName);
}
```

类似地，重载其余关系运算符的函数的定义如下：

```cpp
bool personType::operator<=(const personType& right) const
{
    return (lastName <= right.lastName ||
            (lastName == right.lastName &&
             firstName <= right.firstName));
}
```

```cpp
bool personType::operator<(const personType& right) const
{
    return (lastName < right.lastName ||
            (lastName == right.lastName &&
             firstName < right.firstName));
}
```

```cpp
bool personType::operator>=(const personType& right) const
{
    return (lastName >= right.lastName ||
            (lastName == right.lastName &&
             firstName >= right.firstName));
}
```

```cpp
bool personType::operator>(const personType& right) const
{
    return (lastName > right.lastName ||
            (lastName == right.lastName &&
             firstName > right.firstName));
}
```

接下来给出重载流提取运算符和流插入运算符的函数的定义。

```cpp
istream& operator>>(istream& isObject, personType& pName)
{
    isObject >> pName.firstName >> pName.lastName;

    return isObject;
}
```

```cpp
ostream& operator<<(ostream& osObject, const personType& pName)
{
    osObject << pName.firstName << " " << pName.lastName;

    return osObject;
}
```

如前所述，本程序的主要组件是 candidate。每位候选人都有一个姓名，并且可以接收选票。因为有四个地区，我们可以使用一个包含四个组件的数组来存储所获得的选票。

共有六位候选人。因此，我们声明一个包含六个 `candidateType` 类型候选人的列表。本章通过说明如何包含本章开发的搜索和排序算法，扩展了 `unorderedArrayListType` 类。我们将使用这个类来维护候选人列表。这个候选人列表将被排序和搜索。因此，我们必须为 `candidateType` 类定义（即重载）赋值运算符和关系运算符，因为搜索和排序算法会使用这些运算符。

包含候选人数据的文件中的数据仅由候选人姓名组成。因此，除了重载赋值运算符以便一个对象的值可以赋给另一个对象之外，我们还为 `candidateType` 类重载赋值运算符，以便只能将候选人的姓名（`personType` 的）赋给一个 candidate 对象。也就是说，我们重载赋值运算符两次：一次用于 `candidateType` 类型的对象，一次用于 `candidateType` 和 `personType` 类型的对象。

```cpp
//***************************************************************
// Author: D.S. Malik
//
// class candidateType
// This class specifies the members to implement the properties
// of a candidate. It overloads the assignment operator
// and relational operators for comparison.
//************************************************************

#include <string>
#include "personType.h"

const int NO_OF_REGIONS = 4;

class candidateType: public personType
{
public:
    const candidateType& operator=(const candidateType&);
        //Overload the assignment operator for objects of the
        //type candidateType.

    const candidateType& operator=(const personType&);
        //Overload the assignment operator for objects so that
        //the value of an object of type personType can be
        //assigned to an object of type candidateType.

    void updateVotesByRegion(int region, int votes);
        //Function to update the votes of a candidate for a
        //particular region.
        //Postcondition: Votes for the region specified by
        //               the parameter are updated by adding
        //               the votes specified by the parameter
        //               votes.

    void setVotes(int region, int votes);
        //Function to set the votes of a candidate for a
        //particular region.
        //Postcondition: Votes for the region specified by
        //               the parameter region are set to the votes
        //               specified by the parameter votes.

    void calculateTotalVotes();
        //Function to calculate the total votes received by a
        //candidate.
        //Postcondition: The votes in each region are added
        //               and assigned to totalVotes.

    int getTotalVotes() const;
        //Function to return the total votes received by a
        //candidate.
        //Postcondition: The value of totalVotes is returned.

    void printData() const;
        //Function to output the candidate's name, the votes
        //received in each region, and the total votes received.

    candidateType();
        //Default constructor.
        //Postcondition: Candidate's name is initialized to
        //              blanks, the number of votes in each
        //              region, and the total votes are
        //              initialized to 0.

    //Overload the relational operators.
    bool operator==(const candidateType& right) const;
    bool operator!=(const candidateType& right) const;
    bool operator<(const candidateType& right) const;
    bool operator<=(const candidateType& right) const;
    bool operator>(const candidateType& right) const;
    bool operator>=(const candidateType& right) const;

private:
    int votesByRegion[NO_OF_REGIONS];    //array to store the
                                         //votes received in
                                         //each region
    int totalVotes; //variable to store the total votes
};
```

图 18-39 展示了类 `candidateType` 的 UML 图。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1372_0.png)

**图 18-39**  类 `candidateType` 的 UML 类图

接下来给出 `candidateType` 类的函数定义。

要设置特定地区的选票，将地区编号和选票数量作为参数传递给函数 `setVotes`。因为数组索引从 0 开始，所以地区 1 对应于位置 0 的数组组件，依此类推。因此，要设置正确数组组件的值，需要从地区编号中减去 1。函数 `setVotes` 的定义如下：

```cpp
void candidateType::setVotes(int region, int votes)
{
    votesByRegion[region - 1] = votes;
}
```

要更新特定地区的选票，将地区编号和该地区的选票数量作为参数传递。然后将选票加到该地区的先前值上。函数 `updateVotesByRegion` 的定义如下：

```cpp
void candidateType::updateVotesByRegion(int region, int votes)
{
    votesByRegion[region - 1] = votesByRegion[region - 1]
                             + votes;
}
```

函数 `calculateTotalVotes`、`getTotalVotes`、`printData` 以及默认构造函数的定义相当直接，如下所示。

```cpp
void candidateType::calculateTotalVotes()
{
    int i;

    totalVotes = 0;

    for (i = 0; i < NO_OF_REGIONS; i++)
        totalVotes += votesByRegion[i];
}

int candidateType::getTotalVotes() const
{
    return totalVotes;
}

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

