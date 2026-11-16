```
else
{
    tv = pv -> vlink;
    pv->vlink = pv->vlink->vlink;
    free(tv);
}
for(pv = adjlist; pv != NULL; pv = pv->vlink)
{
    if(pv->elink == NULL)
        continue;
    if(pv->elink->vName == vDel)
    {
        te = pv->elink;
        pv->elink = pv->elink->elink;
        free(te);
        continue;
    }
    for(pe = pv->elink; pe->elink != NULL && pe -> elink -> vName != vDel,
        pe = pe -> elink);
    if (pe->elink!= NULL)
    {
        te = pe->elink;
        pe->elink = pe->elink->elink;
        free(te);
    }
}
```

```
void deleteEdge(int Vstart, int VEnd)
{
    vnode *pv, *tv;
    enode *pe, *te;
    if(adjlist == NULL)
        return;
    for(pv = adjlist; pv != NULL && pv->Vname!=VStart;pv=pv->vlink);
```