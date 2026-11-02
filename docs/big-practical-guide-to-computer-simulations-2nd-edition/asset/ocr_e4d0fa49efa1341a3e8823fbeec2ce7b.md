# ## (10) Random graph

Design, implement and test a function for generating an Erdős–Rényi random graph. This is a graph containing n nodes and m edges. The edges are randomly drawn with equal probability from all possible pairs i,j ∈ V. The function is similar to gs_preferential_attachment(), but simpler. The function prototype reads as follows:

| SOLUTION SOURCE CODE |
| --- |
| DIR: algorithms<br>FILE(S): graph_r.c |

```
```c
/********************** gs_random_graph() **********************/
/** Function adds exactly m randomly chosen edges to   **/
/** the graph.                                        **/
/** No self loops are allowed. No edge is allowed to   **/
/** appear twice!                                      **/
/** PARAMETERS: (*)= return-parameter                  **/
/**             (*) g: graph                           **/
/**                 m: number of edges to be added per node **/
/** RETURNS:                                           **/
/**     (nothing)                                      **/
/******************************************************/
void gs_random_graph(gs_graph_t *g, int m)
```
```