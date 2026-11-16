

停止节点与目标节点非常相似，只有在从开放列表中移除后才能使用，而不能在此之前。在考虑所有更改后，我们现在准备以伪代码形式呈现一个派生的路径查找算法：

```
List OpenList, ClosedList
BeyondAStarPathfinder(List
List
Node
MovementCriteria
Path
StartList,
StopList,
TargetNode,
MovementCriteria,
PathFound)
{
Node StartNode, BestNode, SuccessorNode
Cost NewCost
reset OpenList and ClosedList
for each StartNode in StartList
{
if (StartNode fails MovementCriteria) continue
set StartNode cost to 0
set StartNode estimate to heuristic estimate of remaining
cost to TargetNode
set StartNode value to sum of cost and estimate
set StartNode parent to NoParent
add StartNode to OpenList
}
while OpenList is not empty
{
remove best node BestNode from OpenList
if BestNode is in StopList
{
construct path and save it in PathFound
return as success
}
for each successor SuccessorNode of BestNode
{
if (SuccessorNode fails MovementCriteria) continue
set NewCost to sum of BestNode cost and cost of
moving from BestNode to SuccessorNode
if ((SuccessorNode is in OpenList or ClosedList) and
(NewCost is not less than SuccessorNode cost))
continue
set SuccessorNode cost to NewCost
set SuccessorNode estimate to heuristic estimate of
remaining cost to TargetNode
set SuccessorNode value to sum of cost and estimate
set SuccessorNode parent to BestNode
if SuccessorNode is in ClosedList
remove SuccessorNode from ClosedList
if SuccessorNode is not in OpenList
add SuccessorNode to OpenList
}
add BestNode to ClosedList
}
return as failure
}
```

与 A* 算法相比，派生算法有几个主要区别：其参数列表接受多个起始节点和停止节点，多个起始节点都会变成开放节点，并且任何停止节点都可以停止算法遍历。

我们如何知道派生算法保证能产生最小成本路径？虽然证明这一点超出了本文的范围，但我们将就此主题提供一些指导。首先，我们需要将任何保证能找到通往目标的最优路径的算法定义为 *可接受的*。接下来，我们需要查看 A* 算法 [Nilsson98] 的可接受性，并以此作为起点。我们证明的关键是引入一个连接到所有起始节点的额外节点。这个新节点充当单个起始节点，并基本上将我们的派生算法转换为标准 A* 算法。

## 实现细节

派生算法的典型实现与典型 A* 实现并无太大不同。由于 A* 实现的细节已广为人知 [Pinter01]，我们将专注于如何实现派生算法特有的功能。

派生算法传入多个起始节点和停止节点。正如我们所料，将多个起始节点和停止节点作为参数传递会增加涉及的数据量，并给性能带来额外开销。为降低这种开销，我们将多个节点数据存储在数组中，这些数组本身按引用传递。此外，许多处理类似问题的实际实现会分别存储节点数据，并使用数组存储引用、句柄或对象 ID，以便访问实际节点数据。

派生算法还使用多个停止节点来停止算法的执行。建议明确地将停止节点标记为停止节点。标签应存储在某种节点数据结构中，该结构还包含所有其他节点运行时数据（成本值和指向父节点的链接）。通过对节点进行标记，我们不再需要将每个遍历的节点与整个停止节点列表进行比较。相反，可以立即检查节点标记。在遍历 m 个节点以查找 n 个停止节点中的一个时，使用未标记停止节点的实现需要 m x n 次比较。使用标记节点可将比较次数减少到 m，即每个遍历节点一次。

## 实际示例

在实际应用中，派生算法允许实现一些高级功能。让我们考虑一个典型的即时战略（RTS）游戏，其中游戏对象可以驻扎单位，并分配集结点，驻扎单位在退出后应移动到这些集结点。为本文之目的，我们将这些游戏对象称为 *包含游戏对象*。在实际游戏中，包含游戏对象通常实现为建筑物或运输车辆的变体。

## 多个起始节点的示例

与驻扎相关的常见问题之一是如何在包含游戏对象周围的所有退出位置中选择放置退出单位的位置。最简单、最快速的方法是使用预定义的退出位置顺序，并选择第一个无障碍的位置。由于此方法未考虑集结点的位置，退出单位通常不得不先绕过其退出的对象，然后再前往集结点。

为避免此问题，我们可能会选择到集结点直线距离最短的退出位置。尽管这显然是一种更好的方法，但它仍有其问题。首先，它没有考虑退出位置与集结点之间可能存在的任何障碍。因此，无法保证所选退出位置是通往集结点的最小成本路径的起点的最优退出位置。更糟糕的是，有时障碍物会将所选退出位置与集结点隔开，导致退出单位停滞，并彻底降低该单位对玩家的价值。

考虑障碍物的一种方法是找出每个退出位置与集结点之间的最小成本路径，并选择产生总成本最低路径的退出位置。不幸的是，除了退出位置非常少的情况外，此实现的性能成本是禁止性的。

如果我们不多次连续调用 A* 算法，而是只调用一次我们的派生算法，就可以避免这个问题。可能的退出位置将为我们提供多个起始节点，而集结点将为我们提供一个目标节点，该节点也将充当停止节点。通过使用这些参数，派生算法将在一次搜索空间遍历中找到最优退出位置及其通往集结点的关联最小成本路径。

图 3.7.1 展示了一个示例，其中包含一个作为包含对象的建筑物、十几个或更多退出位置、一个被类墙结构阻挡的集结点，以及一个作为通往集结点的最小成本路径起点的最优退出位置。该示例还演示了，到目标直线距离最短的退出位置（在此例中为建筑物最右下角的位置）不一定是最优退出位置。

多个起始节点的路径查找算法还有其他实际用途。其中之一是确定，在几个可能的建筑物中，哪一个是在给定目标位置（例如争夺激烈的区域）所需单位的最佳生产选择。所选建筑物将是能够生产能够最快到达战场的单位的建筑物。调用派生算法可以

![](img/672fe9a2d008ba627b1991e15d70f43e_415_0.png)

- 退出位置
- 最优退出位置
- 移动障碍
- 集结点位置
- 最优路径

### 图 3.7.1 使用多个起始节点查找最优退出位置的示例。

为这一请求提供快速答案。所有建筑物的退出位置将为我们提供多个起始节点，而目标位置将为我们提供一个目标节点。通过这些参数，派生算法将毫无问题地找到通往目标位置的最小成本路径，这也将为我们提供最优退出位置及其关联的建筑物。

图 3.7.2 展示了一个示例，其中建筑物 A、B 和 C 是在目标位置生产所需单位的候选对象。建筑物 B 恰好有一个最优退出位置，它是通往最小成本路径的起点。需要注意的是，建筑物 A 拥有到目标位置直线距离更短的退出位置，但由于建筑物右侧的类墙障碍物，这些退出位置并非最优。

