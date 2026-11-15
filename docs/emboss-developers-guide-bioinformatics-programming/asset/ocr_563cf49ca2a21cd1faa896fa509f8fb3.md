# 6.20 HANDLING GRAPHICAL OUTPUT

```
gdata = ajGraphdataNew();

/* Set up graph data */

ajGraphDataAdd(graphs,gdata);

/* Do something with the graph */

ajGraphdataDel(&gdata);
ajGraphxyDel(&graphs);
```

ajGraphDataReplace and ajGraphDataReplaceI are used to replace one graph in a graph object with another. The new graph data (held in a AJPGraphdata object) is passed and graph data object that is replaced is deleted. The function returns 1 on success (0 otherwise):

```
ajint ajGraphDataReplace (AJPGraph thys, AJPGraphdata graphdata);
ajint ajGraphDataReplaceI (AJPGraph thys, AJPGraphdata graphdata, ajint num);
```

ajGraphDataReplace replaces the first graph whereas ajGraphDataReplaceI replaces the numbered graph.
ajGraphInitSeq is used to define default values for a graph object based on a sequence that is passed:

```
void ajGraphInitSeq (AJPGraph thys, const AJPSeq seq);
```

The title of the plot is set to the name of the sequence and the x-axis is set to the sequence size. It is used as follows:

```
int main(int argc, char **argv)
{
    AJPSeq seq      = NULL;
    AJPGraph graph  = NULL;

    embInit("isochore", argc, argv);

    seq   = ajAcdGetSeq("sequence");
    graph = ajAcdGetGraphxy("graph");

    ajGraphInitSeq(graph, seq);
}
```

Finally, ajGraphxySetRanges will calculate the minimum and maximum of the data points and store the values in the graph object:

```
void ajGraphxySetRanges (AJPGraph thys);
```

To delete all the drawable objects connected to the graph object (to reuse it for a new graph page) call: