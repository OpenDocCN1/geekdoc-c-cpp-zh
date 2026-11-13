```
{
    if(newkey < curr->data[1])
    {
        *pos = 0;
        return 0;
    }
    else
    {
        *pos = curr->count;
        while((newkey < curr->data[*pos]) && (*pos > 1))
        {
            (*pos)--;
            if(newkey == curr->data[*pos])
                return 1;
            else
                return 0;
        }
    }
}
```

```
btnode * btree :: search(int newkey, btnode *root, int *pos)
{
    if(!root)
    {
        return null;
    }
    else if(search_node(newkey, root, pos))
        return root;
    else
        return search(newkey, root->child[*pos], pos);
}
```

```
btnode * btree :: insert(int newdata, btnode *root)
{
    int meddata;
    btnode *medright, *newroot;
    if(push_down(newdata, root, &meddata, &medright))
    {
        newroot = new btnode;
        newroot->count = 1;
        newroot->data[1] = meddata;
        newroot->child[0] = root;
        newroot->child[1] = medright;
```