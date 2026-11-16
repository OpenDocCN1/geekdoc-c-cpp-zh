```
if(pv == NULL)
return;
if(pv->elink == NULL)
return;
if(pv->elink->vName == vEnd)
{
te = pv->elink;
pv->elink = pv->elink->elink;
free(te);
return;
}
for(pe = pv->elink; pe->elink != NULL && pe -> elink -> vName != vEnd;
pe = pe->elink);
if(pe->elink!= NULL)
{
te = pe->elink;
pe->elink = pe->elink->elink;
free(te);
}
}
void createGraph()
{
int r, c, v, nVertex;
printf("\n Enter the no. of Vertices : ");
scanf("%d", &nVertex);
adjList = NULL;
for(v = 0; v < nVertex; v++)
insertVertex();
for(r = 0; r < nVertex; r++)
for(c = 0; c < nVertex; c++)
if(r != c)
insertEdge(r+1, c+1);
}
void viewGraph()
{
int edges = 0, wStatus = 0, nVertex = 0;
vnode *pv; enode *pe;
```