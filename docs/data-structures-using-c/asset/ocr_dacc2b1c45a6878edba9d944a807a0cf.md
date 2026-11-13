```
temp->child[1] = temp->child[0];
/* Increase count of right node */
temp->count++;
/* Move data from current to first place of right
node */
temp->data[1] = curr->data[pos];
temp = curr->child[pos - 1];
/* Move last data from left node into current */
curr->data[pos] = temp->data[temp->count];
curr->child[pos]->child[0] = temp->child[temp->count];
/* Decrease count of left node */
temp->count--;
}
```

Similarly, we can write a move_left() function given in Program Code 13.13, which moves data from *curr node into the child[pos - 1] and then moves the leftmost entry from child[pos] into *curr node.

```
PROGRAM CODE 13.13
void btree :: move_left (btnode *curr, int pos)
{
    int p;
    btnode *temp;
    temp = curr->child[pos - 1];
    /* Increase count of right node */
    /* * Move data from current into last place of left
    node and increase its count */
    temp->count++;
    temp->data[temp->count] = curr->data[pos];
    temp->child[temp->count] = curr->child[pos]->child[0];
    /* Set temp to right node of current */
    temp = current->child[pos];
    /* * Move data from first place of right node
    into last place of current and decrease count of
    right node */
    curr->data[pos] = temp->data[1];
    temp->child[0] = temp->child[1];
    temp->count--;
    /* Shift all keys in right node one position left */
    for(p = 1; p <= temp->count; p++)
```