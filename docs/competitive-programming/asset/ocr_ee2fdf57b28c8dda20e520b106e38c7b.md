```
```cpp
// for each edge with (i, j, weight) format
//   EdgeList.push(make_pair(-weight, make_pair(i, j)));
// alternative implementation: use STL vector and algorithm:sort

mst_cost = 0; initSet(V); // all V are disjoint sets initially, see Section 2.3.2
while (!EdgeList.empty()) { // while there exist more edges, O(E)
    pair<int, ii> front = EdgeList.top(); EdgeList.pop();
    if (!sameSet(front.second.first, front.second.second)) { // if no cycle
        mst_cost += (-front.first); // add (negated) -weight of e to MST
        unionSet(front.second.first, front.second.second); // link these two vertices
    }
}
// note that the number of disjoint sets must eventually be one!
// otherwise, no MST has been formed...
```
```

![](bbox=[0.124, 0.297, 0.905, 0.436])

Figure 4.9: Kruskal’s Algorithm for MST Problem (from UVa 908 [17])

Exercise: The implementation shown here only stop when EdgeList is empty. For some cases, we can stop Kruskal’s algorithm earlier. When and how to modify the code to handle this? Figure 4.9 shows the execution of Kruskal’s algorithm on the graph shown in Figure 4.8, leftmost¹.

# Other Applications

Variants of basic MST problems are interesting. In this section, we will explore some of them.

# ‘Maximum’ Spanning Tree

![](bbox=[0.293, 0.682, 0.747, 0.76])

Figure 4.10: ‘Maximum’ Spanning Tree Problem

This is a simple variant where we want the maximum, instead of the minimum ST. In Figure 4.10, we see a comparison between MST and Maximum ST. Solution: sort edges in non increasing order.