```
```cpp
//              store the weights of the edges.
//              edges is an array to store the edges
//              of a minimal spanning tree.
//              edgeWeight is an array to store the
//              weights of the edges of a minimal
//              spanning tree.
```
```

```
```cpp
~msTreeType();
    //Destructor
    //The storage occupied by the vertices and the arrays
    //weights, edges, and edgeWeights is deallocated.

protected:
    int* source;
    double *weights;
    int * edges;
    double *edgeWeights;
};
```
```

We leave the UML class diagram of the class msTreeType and the inheritance hierarchy as an exercise. The definition of the function createSpanningGraph is also left as an exercise for you. This function creates the graph and the weight matrix associated with the graph.

The following C++ function, minimalSpanning, implements Prim’s algorithm, as described previously:

```
```cpp
void msTreeType::minimalSpanning(int sVertex)
{
    int startVertex, endVertex;
    double minWeight;

    source = sVertex;

    bool *mstv;
    mstv = new bool[gSize];

    for (int j = 0; j < gSize; j++)
    {
        mstv[j] = false;
        edges[j] = source;
        edgeWeights[j] = weights[source][j];
    }

    mstv[source] = true;
    edgeWeights[source] = 0;

    for (int i = 0; i < gSize - 1; i++)
    {
        minWeight = DBL_MAX;

        for (int j = 0; j < gSize; j++)
            if (!mstv[j])
            {
                for (int k = 0; k < gSize; k++)
                    if (!mstv[k] && weights[j][k] < minWeight)
```
```