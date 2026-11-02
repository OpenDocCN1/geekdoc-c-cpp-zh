```
void gs_dot_graph(gs_graph_t *g, FILE *file, int dir)
{
    int n;
    elem_t *elem;

    if(dir)
        fprintf(file, "digraph test \n");
    else
        fprintf(file, "graph test \n");
    fprintf(file, "node [height=0.2,width=0.2,label=\"\",fixedsize=true]\n");

    for(n=0; n<g->num_nodes; n++)    /* go through all node */
    {
        fprintf(file, "\n\d\n", n);
        elem = g->node[n].neighbors;
        while(elem != NULL)            /* loop over all neighbors */
        {
            if(dir)
                fprintf(file, "\d -> \d\n", n, elem->info);
            else
                if(n <= elem->info)    /* print each pair only once */
                    fprintf(file, "\d -- \d\n", n, elem->info);
            elem = elem->next;         /* next neighbor */
        }
    }
    fprintf(file, "}\n");
}
```

Depending on the variable dir, a directed or an undirected graph is printed (lines 6-9). Here, the graph is always called “test”. If you prefer to have a variable name, you have to include the graph name as parameter (or include it in the data structure of the graph). Next (line 10), some global node properties are set. In lines 12-26 the graph is printed by iterating over all nodes. First the node is printed (line 15), then all neighbors are visited (lines 16-25) and the corresponding directed or undirected edge is printed. Finally (line 27), the closing bracket of the dot file is written.

You could also use your C program automatically convert the dot file to an image file by using the system command to call, for example, dot with the name of the written file as a parameter, as exemplified in the following lines (assuming that name contains the prefix of the filename and g the graph):