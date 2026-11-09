```
```cpp
stack<int> dfs_scc; // additional information for SCC
set<int> in_stack; // for dfs_low update check

void tarjanSCC(int u) {
    dfs_low[u] = dfs_num[u] = dfsNumberCounter++; // dfs_low[u] <= dfs_num[u]
    dfs_scc.push(u); in_stack.insert(u); // ensure u based on order of visitation
    TRVi (AdjList[u], v) {
        if (dfs_num[v->first] == DFS_WHITE) // a tree edge
            tarjanSCC(v->first);
        if (in_stack.find(v->first) != in_stack.end()) // condition for update
            dfs_low[u] = min(dfs_low[u], dfs_low[v->first]); // update dfs_low[u]
    }
    if (dfs_low[u] == dfs_num[u]) { // if this is a root of SCC
        printf("SCC: ");
        while (!dfs_scc.empty() && dfs_scc.top() != u) {
            printf("%d ", dfs_scc.top()); in_stack.erase(dfs_scc.top()); dfs_scc.pop();
        }
        printf("%d\n", dfs_scc.top()); in_stack.erase(dfs_scc.top()); dfs_scc.pop();
    }
}
```
```

Exercise: This implementation can be improved by about $O(\log V)$ factor by using other data structure other than `set<int> in_stack`. How?

# Topological Sort (on a Directed Acyclic Graph)

Topological sort or topological ordering of a Directed Acyclic Graph (DAG) is a linear ordering of the vertices in the DAG so that vertex $u$ comes before vertex $v$ if edge $(u \to v)$ exists in the DAG. Every DAG has one or more topological sorts. There are several ways to implement a Topological Sort algorithm. The simplest is to slightly modify the simplest DFS implementation in this section.

```
```cpp
void topoVisit(int u) {
    dfs_num[u] = DFS_BLACK;
    TRVi (AdjList[u], v)
        if (dfs_num[v->first] == DFS_WHITE)
            topoVisit(v->first);
    topologicalSort.push_back(u); // this is the only change
}

// inside int main()
topologicalSort.clear(); // this global vector stores topological sort in reverse order
memset(dfs_num, DFS_WHITE, sizeof dfs_num);
REP (i, 0, V - 1)
    if (dfs_num[i] == DFS_WHITE)
        topoVisit(i);
reverse(topologicalSort.begin(), topologicalSort.end());
REP (i, 0, topologicalSort.size() - 1)
    printf("%d\n", topologicalSort[i]);
```
```

In topoVisit(u), we append u to the list vertices explored only after visiting all subtrees below u. As vector only support *efficient insertion* from back, we work around this issue by simply reversing the print order in the output phase. This simple algorithm for finding (a valid) topological sort is again due to Tarjan. It again runs in $O(V + E)$ as with DFS.