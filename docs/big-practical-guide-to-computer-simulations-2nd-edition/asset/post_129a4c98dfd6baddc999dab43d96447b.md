
To delete a graph. One could split this task into two subtasks: first to remove all edges, i.e., *clear* the graph, and second to free the data structures allocated in `gs_graph_generate()`, i.e., to finally delete a cleared graph. We do not show the details of the implementation, but mention that the source code of these functions is also included in the packages which are available online.

Since it is convenient and failure-safe to hide the graph implementation, next a function for inserting an edge in an undirected graph is presented. The function `gs_insert_edge()` receives the graph (i.e. a pointer) and the IDs of the endpoints of the edge as parameter. The C code looks as follows:

```
~~~c
void gs_insert_edge(gs_graph_t *g, int from, int to)
{
    elem_t *elem1, *elem2, *list;

    list = g->node[from].neighbors;                 /* edge exists? */
    while( list != NULL )
    {
        if(list->info == to)                        /* yes */
            return;
        list = list->next;
    }

    elem1 = create_element(to);                     /* create neighbor for 'from' */
    g->node[from].neighbors =
        insert_element(g->node[from].neighbors, elem1, NULL);
    elem2 = create_element(from);                   /* create neighbor for 'to' */
    g->node[to].neighbors =
        insert_element(g->node[to].neighbors, elem2, NULL);
}
~~~
```

First, it is checked whether the edge is already present in the graph (lines 5-11). If so, nothing has to be done. Note that in lines 6-11, we work directly on the implementation level of the lists. To hide the list implementation, one would have to provide *iterators*, which allow us to access the first and next elements, respectively. Since these examples are of illustrative nature mainly, we do not do this. For powerful general purpose lists, the reader should use available libraries anyway, see Chap. 7. In lines 13-15, the second endpoint is inserted into the neighbor list of the first, while in lines 16-18 the first endpoint is inserted into the neighbor list of the second. Note that the directed version of this function would be even simpler, since one would have to create just one list element containing the second endpoint and insert the list element into the neighbor list of the first one.

For a basic analysis of graphs. As pointed out in Sec. 6.8.1, graphs may exhibit several *connected components*, such that nodes belonging to the same component are connected by paths, while for nodes belonging to different components, there exist no path between them. For example, for a graph describing a communication network, nodes belonging to the same component can communicate among each other, while nodes belonging to different components cannot.

Next, a simple algorithm is discussed which determines the connected components of a graph. This discussion will be performed in three steps: First the basic idea is explained. Next the C code is given. Finally, the operation of the algorithm for a small sample graph is discussed. The basic idea is to start with any (“seed”) node. It is considered as first node of the first component. Subsequently, all neighbors of the “seed” node, i.e. all nodes connected by an edge to it, are attributed to the same component. In the same way, the neighbors of these neighbors belong to the same component, and so on. However, note that for a correct determination of the components, each node does not need to be processed more than once. For example, the “seed” node is processed first and there is no need to process it again when the neighbours of any of its neighbours are considered. To accomplish this, for each node an entry in the array *comp* is kept, which indicates whether the node has not been encountered so far during the determination of the components (then *comp*[node] = −1). Conveniently, this variable will also store an ID, identifying the component to which the node belongs. Initially this variable will be set to −1 for all nodes, indicating that each node has not been considered so far. Since for each node one has to consider all neighbors once, the neighbors will be stored in a “bag” once they are encountered, actually implemented as an array *candidate*. During the component construction, the algorithm takes one node after the other from the bag to check their neighbors. In this way, each node connected to the seed node by a path will be considered and added to the component at some point. Note that the order in which the nodes in the bag are considered does not matter here. If the order is *last-in first-out* (LIFO), as for a stack, then, after the first neighbor of the seed has been considered, in turn its first neighbor will be considered, etc., before the second neighbor of the seed node will be considered. Thus, the algorithm will tend to go as far as possible directly. This is called *depth-first search*. If on the other hand the bag is treated in *first-in first-out* (FIFO) fashion, then all neighbors of the seed are taken from the bag before the neighbors of

continues while there are still candidates left (line 19). One after the other the candidates are taken (line 21) and a loop over all neighbors is performed (lines 22–32). For each neighbor it is checked (line 26) whether it has not been assigned to a component yet. If not, it is added to the component and to the bag of candidates (line 27–30).

```
```c
for(n1=0; n1<g->num_nodes; n1++) /* all possible component seeds */
{
    if(comp[n1] == -1)            /* not yet part of a component ? */
    {
        comp[n1] = num_components;
        candidate[0] = n1;
        num_candidates = 1;
        while(num_candidates > 0)  /* still nodes in current comp. ? */
        {
            n2 = candidate[--num_candidates];        /* next candidate */
            neigh = g->node[n2].neighbors;
            while(neigh != NULL)                      /* go through all neighbors */
            {
                nn = neigh->info;
                if(comp[nn] == -1)                /* not yet part of component ? */
                {
                    comp[nn] = num_components;    /* add to candidates */
                    candidate[num_candidates++] = nn;
                }
                neigh = neigh->next;
            }
        }
        num_components++;
    }
}

free(candidate);
return(num_components);
```
```

To understand how the algorithm operates, we consider the small example graph from Fig. 6.24. Initially all comp values are set to −1. The variable num_components is initialized as 0. The change of the variables during the execution of the algorithm is shown in Fig. 6.28. Within the loop over all nodes, first node 0 is encountered. It has not been assigned to a component, thus, a new component is started with ID 0. Node 0 is added to candidate. Hence, during the iteration of the loop over all candidates

```
~~~
n1=0: comp[0]=0
        candidate={0}    n2=0:
                comp[1]=0
        candidate={1}    n2=1:
                comp[3]=0
                comp[4]=0
        candidate={3,4} n2=4:
                comp[2]=0
        candidate={3,2} n2=2:
        candidate={3}    n2=3:
n1=1:
n1=2:
n1=3:
n1=4:
n1=5: comp[5]=1
        candidate={5}    n2=5:
~~~
```

Fig. 6.28 Operation of `gs_components()` for the sample graph of Fig. 6.24. The graph consists of two components with IDs 0 (nodes 0,1,2,3,4) and 1 (node 5). The first column shows the current node n1 of the main loop. Each entry in the second column represents the start of a new component and the corresponding assignment of the component ID to the seed node n1 (line 16 of the code). In the third column, the state of the candidate array at the beginning of each iteration of the loop in line 19 is displayed. The fourth column shows the current node n2 taken from the candidates. In the fifth column, all neighbors of n2 which are added to the component are indicated via the corresponding component ID assignment (line 28).

(lines 19–33), first node 0 is considered. It exhibits one neighbor, node 1, which is added to the component. Therefore, next node 1 is considered in the candidates loop. Node 1 has three neighbors, nodes 0, 3 and 4. Node 0 is already part of the component (comp[0]=0, i.e., ≠ −1), thus nothing happens here. Nodes 3 and 4 are added to the component and to the candidates. Next, node 4 is considered. Its neighbors 1 and 3 are already part of the component. Hence, only its neighbor node 2 is added to the component and to the bag of candidates. Due to the FIFO operation on the candidates, next node 2 is considered. Its only neighbor node 4 is already part of the component, nothing happens. The same holds for node 3, which has neighbors nodes 1 and 4. Now, the candidate array is empty and the construction of the first component is finished. During the main loop, nodes 1, 2, 3, and 4 are encountered next. Since they have already been assigned
