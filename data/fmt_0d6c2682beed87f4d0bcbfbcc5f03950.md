
第一条语句声明 `x` 为 `int` 变量并将 `x` 初始化为 90。第二条语句声明 `list` 为一个包含四个元素的 `int` 数组，并将 `list` 的元素初始化为 2、3、4 和 5。在示例 15-5 和 16-6 中，我们声明 `intList` 为一个类型为 `int` 的 `vector` 对象，然后使用 `push_back` 函数将 `int` 值存储在 `intList` 中。具体来说，以下语句用于声明 `intList` 为一个 `vector<int>` 对象并将 24、39、90 和 66 存储在 `intList` 中。

```cpp
intList.push_back(24);
intList.push_back(39);
intList.push_back(90);
intList.push_back(66);
```

C++11 允许同时声明并初始化 `vector`。例如，接述语句声明 `intList` 为一个 `vector<int>` 对象并在其中存储了 24、39、90 和 66。

```cpp
vector<int> intList = {24, 39, 90, 66};
```

也就是说，在 C++11 中，之前用于声明和初始化 `intList` 的五条语句可以被上述语句代替。

> 注意 数据类型（类）`vector` 是 C++ 标准模板库（STL）的一部分。要了解更多关于 STL 的信息，请参见附录 H。

## 编程示例：选举结果

你当地大学的学生会主席选举即将举行。由于保密性原因，选举委员会主席希望将投票数字化。主席正在寻找某人编写一个程序来分析数据并报告获胜者。让我们为选举委员会编写一个程序。

该大学有四个大部门，每个部门有若干个系。为了选举，部门被标记为 Region 1、Region 2、Region 3 和 Region 4。每个部门中的每个系都管理自己的投票过程，并直接向选举委员会报告结果。投票报告的形式如下：

```
candidateName regionNumber numberOfVotesForTheCandidate
```

选举委员会希望以以下表格形式输出：

| 姓名 | Region1 | Region2 | Region3 | Region4 | 总计 |
|---|---|---|---|---|---|
| Ashley | 23 | 89 | 0 | 160 | 272 |
| Danny | 25 | 71 | 89 | 97 | 282 |
| Donald | 110 | 158 | 0 | 0 | 268 |
| Mia | 34 | 56 | 56 | 78 | 224 |
| Mickey | 56 | 56 | 29 | 78 | 219 |

获胜者：???
投票票数：???

输出中的候选人姓名必须按字母顺序排列。我们假设该程序有六位候选人竞选学生会主席。该程序可以修改以适应任意数量的候选人。数据在两个文件中。一个文件 `candData.txt` 包含候选人的姓名。文件中的姓名没有特定顺序。第二个文件 `voteData.txt` 的每行包含如下形式的投票结果：

```
candidateName regionNumber numberOfVotesForTheCandidate
```

也就是说，`voteData.txt` 中的每行包含候选人姓名、地区编号和该候选人的票数。
