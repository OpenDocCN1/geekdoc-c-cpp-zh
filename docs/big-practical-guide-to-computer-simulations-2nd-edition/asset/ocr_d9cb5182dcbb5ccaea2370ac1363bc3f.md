![](bbox=[0.18, 0.18, 0.88, 0.58])

Fig. 6.26 Neighbor-list based representation of the undirected graph shown in Fig. 6.24 (left) and of the directed graph shown in Fig. 6.25 (right).

```
```c
gs_graph_t *gs_create_graph(int num_nodes)
{
    gs_graph_t *g;
    int n;

    g = (gs_graph_t *) malloc(sizeof(gs_graph_t)); /* allocate */
    g->num_nodes = num_nodes; /* initialize */
    g->node = (gs_node_t *) malloc(num_nodes*sizeof(gs_node_t));

    for(n=0; n<num_nodes; n++)
        g->node[n].neighbors = NULL;

    return(g);
}
```
```

The function just has to allocate memory of the type gs_graph_t (line 6), store the number of nodes in the element num_nodes (line 7), and allocate for the element node an array of this size (line 8). Finally all neighbor lists are initialized as being empty 10-11.

For an object-oriented design, one needs also a function which destroys