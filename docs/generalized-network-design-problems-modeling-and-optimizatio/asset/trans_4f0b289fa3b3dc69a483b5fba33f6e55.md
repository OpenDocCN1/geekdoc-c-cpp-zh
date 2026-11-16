

## 算法

在每次迭代中，客户构建一个全局巡回路径，即全局图中的哈密顿回路。顾问的策略也由一个全局巡回路径表示，顾问将其宣传给他的客户。算法应用局部搜索过程，以改进代表客户的全局解或处于休假模式的顾问策略的全局巡回路径。然后，使用第 3.2 节中描述的簇优化过程，算法找到最佳广义巡回路径，它对应于局部搜索过程返回的全局巡回路径。

为了比较休假期间构建的策略，顾问使用每个策略对应的广义巡回路径的成本。同样，客户的成功基于广义解的成本进行评估。我们算法的伪代码如算法 3.6 所示。

虚拟人员可能处于正常模式或休假模式之一。在初始化阶段（第 2-5 行），创建虚拟人员并将其置于休假模式。基于其模式，在算法的每次迭代中（第 7-31 行），虚拟人员构建问题的全局解（第 19 行）或全局顾问策略（第 9 行）。在本小节后面，我们将描述构建全局解或策略所涉及的操作，以及客户为当前迭代选择顾问所使用的方法（第 17 行）。

全局策略和全局解通过应用局部搜索过程得到改进（第 10 行和第 20 行）。然后使用第 3.2 节中描述的 clusterOptimization 过程，找到与当前全局策略对应的最佳广义策略（第 11 行）或与当前全局解对应的最佳广义解（第 21 行）。构建全局策略后，处于休假模式的虚拟人员检查对应的广义策略是否是自休假开始以来找到的最佳广义策略（第 12-15 行）。同样，构建全局解后，客户检查对应的广义解，以决定他是否取得了成功，如果是，他会更新其顾问的策略（第 22-26 行）。每次迭代结束时，每个虚拟人员的声誉和行动模式都会被更新（第 30-31 行）。

算法 3.7 详细说明了如何根据客户取得的成功来更新顾问的声誉。

声誉随时间以恒定速率衰减，该速率由参数 fadingRate 给出（第 4 行）。顾问的声誉随其每个客户取得的每一次成功而增加（第 5 行），并且为找到迄今最佳解而获得额外 10 分的奖励（第 6-9 行）。

顾问的声誉不能超过最大值（第 10-12 行），并且算法防止最佳顾问（即找到迄今最佳解的顾问）的声誉低于给定值（第 13-17 行）。

常量参数 initialReputation 表示在休假结束时分配给顾问的声誉。

算法 3.8 详细说明了如何更新每个虚拟人员的行动模式。声誉低于最低水平的顾问被置于休假模式，而休假期结束的顾问被置于正常模式。

算法 3.9 显示了将虚拟人员置于休假或正常行动模式所采取的操作。

## 算法 3.6 (CGS-GTSP 算法)。

```
procedure CGS-GTSP()
   create the set P of virtual persons
   foreach p ∈ P do
setSabbaticalMode(p)
   end foreach
   while (termination condition not met) do
     foreach virtual person p do
       if actionMode[p] = sabbatical then
         currStrategy[p] ← constructStrategy(p)
         applyLocalSearch(currStrategy[p])
         genStrategy ← clusterOptimization(currStrategy[p])
         if cost(genStrategy) < bestStrategyCost then
           bestStrategy[p] ← currStrategy[p]
           bestStrategyCost[p] ← cost(currStrategy[p])
         end if
       else
         c ← chooseConsultant(p)
         if c ≠ null then
           currSol[p] ← constructSolution(p,c)
           applyLocalSearch(currSol[p])
           currGenSol[p] ← clusterOptimization(currSol[p])
           if currGenSol[p] is better than all solutions found by a client
             of c since last sabbatical then
             successCount[c] ← successCount[c] + 1
             strategy[c] ← currSol[p]
           end if
         end if
       end if
     end foreach
   end while
   updateReputations()
   updateActionModes()
end procedure
```

## 算法 3.7 (更新声誉的过程)。

```
procedure updateReputations()
    foreach p ∈ P do
        if actionMode[p] = normal then
            rep[p] ← rep[p] * (1 - fadingRate)
            rep[p] ← rep[p] + successCount[p]
        if cost(currGenSol[p]) < cost(bestSoFarSol) then
            bestSoFarSol ← currGenSol[p]
            rep[p] ← rep[p] + 10    // reputation bonus
        end if
        if rep[p] > 10 * initialReputation then
            rep[p] ← 10 * initialReputation
        end if
        if p is the best consultant then
            if rep[p] < initialReputation then
                rep[p] ← initialReputation
            end if
        end if
    end foreach
end procedure
```

## 算法 3.8 (更新行动模式的过程)。

```
procedure updateActionModes()
    foreach p ∈ P do
        if actionMode[p] = normal then
            if rep[p] < 1 then
                setSabbaticalMode(p)
            end if
        else
            sabbaticalCountdown ← sabbaticalCountdown - 1
            if sabbaticalCountdown = 0 then
                setNormalMode(p)
            end if
        end if
    end foreach
end procedure
```

## 算法 3.9 (设置休假和正常模式的过程)。

```
procedure setSabbaticalMode(p)
    actionMode[p] ← sabbatical
    bestStrategy[p] ← null
    bestStrategyCost[p] ← infinity
    sabbaticalCountdown ← 20
end procedure
procedure setNormalMode(p)
    actionMode[p] ← normal
    rep[p] ← initialReputation
    strategy(p) ← bestStrategy[p]
end procedure
```

## 策略与解的构建

休假期间用于构建新策略的启发式方法基于全局图中超节点之间的虚拟距离。我们将两个超节点之间的虚拟距离计算为两个对应簇质心之间的距离。选择此启发式方法的理由是，我们的算法设计用于一类问题，即具有欧几里得距离的对称实例，其中簇内的节点在空间上彼此靠近。

通过在簇之间引入虚拟距离，我们有可能使用候选列表，以限制每个构建步骤中可用的选择数量。对于每个簇 \( V_i \)，我们考虑一个包含最接近的 \( cand \) 个簇的候选列表，其中 \( cand \) 是一个参数。这样，簇 \( V_i \) 中人员 \( k \) 的可行邻域表示簇 \( V_i \) 的候选列表中该人员 \( k \) 尚未访问的簇集合。几种 TSP 的启发式算法在解构建阶段使用候选列表（参见 [13]，作为其在蚁群优化算法中应用的示例），但候选列表尚未广泛用于构建 GTSP 的解。我们的算法在策略解的构建过程中都使用候选列表。

使用候选列表可能会显著提高算法所需的时间，但也可能导致遗漏良好解。因此，选择适当的候选列表大小和元素对于算法的工作至关重要。在 TSP 的情况下，大小为 20 的候选列表经常被使用，但 10 到 40 之间的其他值也很常见 [91]。对于 GTSP，由空间上彼此靠近的节点组成的簇的实例，适当的候选列表大小要小得多。我们的实验表明，在这种情况下，4 或 5 的值是足够的。

