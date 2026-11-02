```
for(c1=0; c1<num_points; c1++)                /* initialize */
{
    pos[c1] = c1;
    cluster[c1] = c1;
    node[c1].left = NULL;
    node[c1].right = NULL;
    node[c1].dist = 0.0;
    node[c1].ID = c1;
    node[c1].size = 1;
}
```

Initially, the number of clusters is equal to the number of data points n (line 33) and the next available cluster ID will be n (line 34). The main loop (lines 35-81) will be performed while there are clusters left for being merged. In the main loop, first the smallest current inter-cluster distance is determined (lines 37-44) and the corresponding clusters are obtained via the cluster array (lines 46-47):

```
num_clusters = num_points;
next_ID = num_clusters
while(num_clusters > 1)                /* until all clusters are merged */
{
    entry_min1=0; entry_min2=1;  /* search min. off-diag distance */
    for(c1=0; c1<num_clusters; c1++)
        for(c2=c1+1; c2<num_clusters; c2++)
            if(gsl_matrix_get(distance, c1, c2) <
               gsl_matrix_get(distance, entry_min1, entry_min2))
            {
                entry_min1=c1, entry_min2=c2;
            }
    ID_min1 = cluster[entry_min1];      /* determine cluster IDs */
    ID_min2 = cluster[entry_min2];
```

Now, a new node can be set up. It contains pointers to its two sub clusters, its ID, its size which is the sum of the sizes of the two sub clusters, and the distance of the two sub clusters:

```
node[next_ID].left = &(node[ID_min1]);      /* merge clusters */
node[next_ID].right = &(node[ID_min2]);
node[next_ID].ID = next_ID;
node[next_ID].size = node[ID_min1].size + node[ID_min2].size;
node[next_ID].dist = gsl_matrix_get(distance, entry_min1, entry_min2);
```