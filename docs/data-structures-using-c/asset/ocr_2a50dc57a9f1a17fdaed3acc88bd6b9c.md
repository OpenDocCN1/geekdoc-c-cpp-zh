is placed in the current node, and the successor is deleted. After deletion, the function checks to see if enough entries remain in the appropriate node, and if not, move entries as required.

```
void btree :: del_node(int key, btnode *curr)
{
    int pos;
    if(!curr)
    {
        cout << "\\nTarget Not Found";
        return ;
    }
    else
    {
        if(search_node(key, curr, &pos))
        {
            if(curr->child[pos - 1])
            {
                /* targetkey found, replace data [pos] by
                it successor */
                successor(curr,
                successor(curr, pos);
                del_node(curr->data[pos], curr->child[pos]);
            }
            else
                remove_key(curr,pos); /* removes key from
                pos of *current */
        }
        else /* Target key not found in the current
        node, search a subtree */
        del_node(key, curr->child[pos]);
        if(curr->child[pos])
        {
            if(curr->child[pos]->count < min)
                restore(curr, pos);
        }
    }
}
```

The remove_key() function removes the target key from pos in the curr node and shifts the remaining keys one position ahead. The implementation of this operation is as in Program Code 13.10.