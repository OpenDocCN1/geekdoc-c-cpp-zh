
比较。因此，在递归的第1层，比较次数为 $2(n / 2 - 1) = n - 2 = O(n)$。一般来说，在递归的第 $k$ 层，对函数 `mergeList` 的调用总数为 $2^k$。这些调用中的每一个都合并两个子列表，每个子列表的大小为 $n / 2^{k+1}$，这最多需要 $n / 2^k - 1$ 次比较。因此，在递归的第 $k$ 层，最大比较次数为：

$2^k\left(\frac{n}{2^k}-1\right)=n-2^k=O(n)$。

由此可知，递归每一层的最大比较次数为 $O(n)$。由于递归层数为 $m$，归并排序算法所作的最大比较次数为 $O(nm)$。现在，$n=2^m$ 意味着 $m=\log_2 n$。因此，归并排序算法所作的最大比较次数为 $O(n\log_2 n)$。

如果用 $W(n)$ 表示排序 $L$ 在最坏情况下的关键字比较次数，那么 $W(n)=O(n\log_2 n)$。

令 $A(n)$ 表示平均情况下的关键字比较次数。在平均情况下，归并过程中，其中一个子列表会先于另一个列表耗尽。由此可知，平均而言，当合并两个总规模为 $n$ 的有序子列表时，比较次数将小于 $n-1$。平均而言，可以证明归并排序的比较次数由以下公式给出：如果 $n$ 是2的幂，则 $A(n)=n\log_2 n-1.25n=O(n\log_2 n)$。当 $n$ 不是2的幂时，这也是一个很好的近似。

**注意** 我们也可以通过构造并求解某些方程来获得对归并排序算法的分析，如下所示。如前所述，在归并排序中，所有比较都在过程 `mergeList` 中进行，该过程合并两个有序子列表。如果一个子列表的大小为 $s$，另一个子列表的大小为 $t$，那么在最坏情况下合并这些列表最多需要 $s+t-1$ 次比较。因此：

$W(n)=W(s)+W(t)+s+t-1$。

注意 $s=n/2$ 且 $t=n/2$。假设 $n=2^m$。那么，$s=2^{m-1}$ 且 $t=2^{m-1}$。由此可得 $s+t=n$。因此：

$W(n)=W(n/2)+W(n/2)+n-1=2W(n/2)+n-1,\ n>0$。

此外：

$W(1)=0$。

已知当 $n$ 是2的幂时，$W(n)$ 由以下公式给出：

$W(n)=n\log_2 n-(n-1)=O(n\log_2 n)$。

> **注意：** *（堆排序）* 本章还讨论堆排序算法。所需材料在文件 Heap_Sort.pdf 中。该文件可在 *www.cengagebrain.com* 获取。要找到该文件，请通过输入本文的 ISBN 导航到本书页面，然后单击 Free Materials。

## 编程示例：选举结果

![](img/d0be7fc6d804b63484835c6c8bc67a07_1366_0.png)

你们当地大学的学生会主席选举即将举行。选举委员会主席希望将投票计算机化，并已要求你编写一个程序来分析数据并报告获胜者。

该大学有四个主要分区，每个分区有若干系。在选举中，这四个分区分别标记为区域1、区域2、区域3和区域4。每个分区中的每个系自行处理投票，并将每位候选人获得的票数报告给选举委员会。投票数据按以下形式报告：

```
firstName lastName regionNumber numberOfVotes
```

选举委员会希望输出为以下表格形式：

```
------------------Election Results------------------
```

| 候选人姓名 | 票数：区域1 | 票数：区域2 | 票数：区域3 | 票数：区域4 | 总计 |
|---|---|---|---|---|---|
| Sheila Bower | 23 | 70 | 133 | 267 | 493 |
| Danny Dillion | 25 | 71 | 156 | 97 | 349 |
| Lisa Fisher | 110 | 158 | 0 | 0 | 268 |
| Greg Goldy | 75 | 34 | 134 | 0 | 243 |
| Peter Lamba | 285 | 56 | 0 | 46 | 387 |
| Mickey Miller | 112 | 141 | 156 | 67 | 476 |

获胜者：Sheila Bower，获得票数：493

总投票数：2216

输出中候选人姓名必须按字母顺序排列。

对于本程序，我们假设有六名候选人竞选学生会主席职位。该程序可以增强以处理任意数量的候选人。

数据提供在两个文件中。一个文件 `candData.txt` 包含竞选主席职位的候选人姓名。该文件中候选人姓名的顺序不限。在第二个文件 `voteData.txt` 中，每一行由以下形式的投票结果组成：

```
firstName lastName regionNumber numberOfVotes
```

文件 voteData.txt 中的每一行由候选人姓名、区域编号以及该候选人在该区域获得的票数组成。每行一个条目。例如，包含投票数据的输入文件如下所示：

```
Greg Goldy 2 34
Mickey Miller 1 56
Lisa Fisher 2 56
Peter Lamba 1 78
Danny Dillion 4 29
Sheila Bower 4 78
.
.
.
```

第一行表示 Greg Goldy 从区域2获得了34票。

- **输入**  两个文件：一个包含候选人姓名，另一个包含如前所述的投票数据。
- **输出**  以表格形式呈现的选举结果（如前所述）以及获胜者的姓名。

### 问题分析与算法设计

从输出可以清楚地看出，程序必须按区域组织投票数据，计算每位候选人获得的总票数以及整个选举的总投票数。此外，候选人姓名必须按字母顺序出现。

本程序的主要组成部分是候选人。因此，首先我们将设计 `class` candidateType 来实现一个候选人对象。此外，在本程序中，我们使用一个 candidateType 对象数组来实现候选人列表。

每位候选人都有姓名并获得票数。由于有四个区域，我们可以使用一个包含四个分量的数组。在示例10–10（第10章）中，我们设计了 `class` personType 来实现人的姓名。回顾一下，personType 类型的对象可以存储名和姓。既然我们已经讨论了运算符重载，我们将重新设计 `class` personType，并定义关系运算符，以便可以比较两个人的姓名。我们还将重载赋值运算符以便于赋值，并使用流提取和插入运算符进行输入/输出。由于每位候选人都是一个人，我们将从 `class` personType 派生 `class` candidateType。

### personType

`class` personType 实现一个人的名和姓。因此，`class` personType 有两个成员变量：firstName 用于存储名，lastName 用于存储姓。我们将这些声明为 protected，以便可以轻松扩展 `class` personType 的定义，以适应实现人名所需的特定应用程序的要求。`class` personType 的定义如下。

```cpp
/************************************************************
// Author: D.S. Malik
//
// class personType
// This class specifies the members to implement a person's
// name. It overloads the stream insertion and extraction
// operators and relational operators for comparison.
//************************************************************

#include <string>

using namespace std;

class personType
{
    friend istream& operator>>(istream&, personType&);
    friend ostream& operator<<(ostream&, const personType&);

public:
    void setName(string first, string last);
        //Function to set firstName and lastName according
        //to the parameters.
        //Postcondition: firstName = first; lastName = last

    string getFirstName() const;
        //Function to return the first name.
        //Postcondition: The value of firstName is returned.

    string getLastName() const;
        //Function to return the last name.
        //Postcondition: The value of lastName is returned.

    personType(string first = "", string last = "");
        //Constructor
        //Sets firstName and lastName according to the
        //parameters. The default values of the parameters are
        //empty strings.
        //Postcondition: firstName = first; lastName = last

        //overload the relational operators
    bool operator==(const personType& right) const;
    bool operator!=(const personType& right) const;
    bool operator<(const personType& right) const;
    bool operator<=(const personType& right) const;
    bool operator>(const personType& right) const;
    bool operator>=(const personType& right) const;

protected:
    string firstName; //variable to store the first name
    string lastName;  //variable to store the last name
};
```
