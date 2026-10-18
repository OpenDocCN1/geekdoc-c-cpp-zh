
φ(y_i) 满足当前阶段在 y_0、y_1、⋯、y_{i−1} 处已分配频率的频率分离要求（C）。约束 (3.4) 确保，如果 φ(y_i) 可以在节点 y_i 处无冲突地分配，那么 φ(y_i) + k × increment（k = 1, 2, 3，⋯）也可以在 y_i 处无冲突地分配。注意，求 φ(y_0) 时只需满足约束 (3.2)。约束 (3.3) 和 (3.4) 对所有 0 < i ≤ m − 1 的 φ(y_i) 都生效。

**Algorithm Find_increment**

```
Y = (y_0, y_1, ···, y_{m−1})
Q = (q_0, q_1, ···, q_{r−1})
φ(Q) = (φ(q_0), φ(q_1), ···, φ(q_{r−1}))
origin
begin
    Set increment = s_0;
    For i = 0 to m − 1 do
        begin
            Find φ(y_i) as the least frequency in [origin, origin + increment] which satisfies constraints (3.2), (3.3) and (3.4) as mentioned under Step 3.2.
            If such φ(y_i) does not exist, set increment = increment + 1.
        end
    Return increment.
end
```

**FIGURE 3.23:** Algorithm for finding increment

**Example 14.** 考虑 X′（如表 3.16 所示）。W 中的最大需求为 45。注意，只有节点 11 在 X′ 中拥有 W 的最大需求。因此，m = 1，Y 仅包含 X′ 中的第一个节点（节点 11）。从 **Find_increment**（Y、Q、φ(Q)、origin）得到的增量值为 s_0 = 5，这是初始值。在后续的分配阶段，需求向量会被修改，从而可能出现多个最大需求节点，此时增量值可能更高。

**Step 4 (assign a single frequency)**

by the algorithm **Find_Assignment**. Note that the value of increment is computed in such a way that the set V must include the first m nodes in X′ having maximum demand. In other words, all the maximum demand nodes must be assigned a frequency by the **Find_Assignment** algorithm. Here, φ(V) represents the first round frequency assignment to V where each node has been assigned a frequency.

![](img/6578f6fc95ac71d2c7109e594d9df12f_175_0.png)

**FIGURE 3.25:** Single channel assignment to benchmark cellular network

**Example 15.** 考虑 X′（如表 3.16 所示），设 origin = 0。步骤 3 中得到的增量值为 5。算法 **Find_Assignment** 生成的集合 V、φ(V) 和 V′ 分别为 V = {11, 10, 9, 6, 8, 13, 7, 20, 19, 18, 12}，φ(V) = {0, 2, 4, 0, 1, 2, 3, 0, 2, 4, 4}，以及 V′ = {17, 14, 5, 16, 15, 4, 3, 2, 1, 0}。

步骤 4 中得到的频率分配 φ(V) 如图 3.25 所示，节点标签 {a} 表示在 V 中的单频率分配过程中，频率 a 已分配给该节点。

**Step 5 (assign multiple frequencies)**

- **Input:** The demand vector W; sets V, V′ and φ(V) as computed in Step 4 and the value of increment as computed in Step 3.
- **Step 5.1:** Compute γ_max and γ′_max to act as the maximum demands among the nodes in V and V′, respectively.
- **Step 5.2:** Compute the number of rounds d_v that the frequencies will be assigned to every node v ∈ V as: d_v = (γ_max − γ′_max) if w_v ≥ (γ_max − γ′_max), otherwise, d_v = w_v. Denote D = (d_v) as the round vector where v ∈ V.
- **Step 5.3:** Assign d_v frequencies to the node v ∈ V using the value of increment and the first round frequency φ(v) already assigned to v as follows: φ(v) + j × increment, where j ∈ {0, 1, ···, (d_v − 1)}.
- **Output:** The set of d_v frequencies assigned to each node v ∈ V.

**Example 16.** 考虑步骤 4 产生的集合 V 和 V′，以及表 3.16 中的当前需求向量 W。γ_max（V = {11, 10, 9, 6, 8, 13, 7, 20, 19, 18, 12} 中的最大需求）为 45，γ′_max（V′ = {17, 14, 5, 16, 15, 4, 3, 2, 1, 0} 中的最大需求）为 30。步骤 5 计算得到的圆向量 D = {15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15}，因为所有 v ∈ V 的 w_v ≥ (γ_max − γ′_max) = (45 − 30) = 15。利用 φ(V) 和增量值，节点 V 的多频率分配如图 3.26 所示，其中标签 {a − b} 表示频率 a、a + increment、a + 2 × increment、⋯、b = a + (d_v − 1) × increment 已分配给该节点，increment = 5，d_v = 15 对所有 v ∈ V 成立。图 3.26 中的最高频率为 74。

![](img/6578f6fc95ac71d2c7109e594d9df12f_176_0.png)

**FIGURE 3.26:** Set of assignment paths in first phase

![](img/6578f6fc95ac71d2c7109e594d9df12f_176_1.png)

**FIGURE 3.27:** Set of assignment paths in second phase

**Step 6 (update)**

- **Step 6.1:** Modify the current demand vector W as follows: w_v = w_v if v ∈ V′; w_v = w_v − (γ_max − γ′_max) if v ∈ V and w_v ≥ (γ_max − γ′_max); and w_v = 0 if v ∈ V and w_v < (γ_max − γ′_max). Denote this modified demand vector as the residual demand vector R.
- **Step 6.2:** Reset Q to hold the subset of the nodes in V for which the residual demand is non-zero.
- **Step 6.3:** Reset φ(Q) to hold the last round frequencies assigned at the nodes in Q at Step 5.
- **Step 6.4:** Reset origin to the immediate next frequency of the maximum frequency in φ(Q).
- **Step 6.5:** Consider the residual demand vector R and the sorted node ordering X′ as the current demand vector W and current node ordering X, respectively.
- **Step 7:** Repeat Step 2 – Step 6 until the residual demand vector becomes 0.

**Remark 14.** Note that the next phase of assignment will be started with the frequency immediately next to the highest frequency used in the previous phase of assignment. The reason to hold in φ(Q) the last round frequencies of the nodes in Q is that these are the potential frequencies that may conflict with the frequencies that will be assigned in the first round of the next phase of assignment. Therefore it is required to assign frequencies in the first round of the next phase of assignment satisfying the last round frequencies of the previous phase of assignment held in φ(Q).

**Example 17.** The residual demand vector R, Q, φ(Q) and origin as obtained by Step 6 are R = {30, 25, 25, 30, 15, 15, 15, 25, 10, 25, 10, 5, 5, 5, 15, 15, 12, 8, 5, 5, 5}, Q = {11, 10, 9, 6, 8, 13, 7, 20, 19, 18, 12}, φ(Q) = {70, 72, 74, 70, 71, 72, 73, 70, 72, 74, 74} and origin = 75, respectively. The next phase of assignment obtained by repeating Step 2 through Step 6 with origin = 75 is shown in Figure 3.27. The set W = {30, 25, 25, 30, 15, 15, 15, 25, 10, 25, 10, 5, 5, 5, 15, 15, 12, 8, 5, 5, 5} is then sorted as W′ = {30, 30, 25, 25, 25, 25, 15, 15, 15, 15, 15, 12, 10, 10, 8, 5, 5, 5, 5, 5, 5}, which produces X′ = {17, 11, 10, 9, 14, 5, 16, 6, 8, 15, 13, 4, 7, 20, 3, 2, 18, 19, 12, 1, 0}. The set Y is computed as {11, 17} where both the nodes 11 and 17 have demand 30. The increment is computed as 5. Therefore, the available frequency channels are 75, 76, 77, 78 and 79, which are assigned to the set X′. Now V, φ(V) and V′ are computed as V = {17, 11, 10, 14, 5, 16, 6, 8, 1}, φ(V) = {76, 75, 78, 76, 77, 79, 79, 77, 75}, and V′ = {9, 15, 13, 4, 7, 20, 3, 2, 18, 19, 12, 0}, respectively. Note that the set of nodes in V in the second phase again forms a network structure of a set of sparse paths, as shown in Figure 3.27. The number of rounds that the frequencies in φ(V) will be repeated is given by D = {5, 5, 5, 5, 5, 5, 5, 5, 5} as γ_max − γ′_max = 30 − 25 = 5 and demands of all the nodes in V are greater than or equal to 5. Now the residual demand vector is given by R = {25, 25, 20, 25, 20, 20, 10, 10, 10, 15, 15, 12, 10, 10, 8, 5, 5, 5, 5, 0, 5}. Since demands of all the nodes in V are greater than or equal to 5, the set Q and set V are same. The last round frequencies assigned at the nodes in V is given by φ(Q) = {96, 95, 98, 96, 97, 99, 99, 97, 95}. The origin will now become 100 as 99 is the highest frequency assigned at φ(Q). Following the same procedure, subsequent phases of assignment are shown in Figures 3.28 through 3.31. In the sixth phase of the assignment, the residual demand vector becomes 0 and the process terminates. The highest frequency assigned in Figure 3.31 is 267 which corresponds to the final bandwidth requirement of 268.
