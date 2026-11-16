```
```cpp
struct WeightedEdge
{
    // Which nodes are connected by this edge?
    struct WeightedGraphNode* mFrom;
    struct WeightedGraphNode* mTo;
    // Weight of this edge
    float mWeight;
};

struct WeightedGraphNode
{
    // Stores outgoing edges
    std::vector<WeightedEdge*> mEdges;
};
// (A WeightedGraph has WeightedGraphNodes)
```
```