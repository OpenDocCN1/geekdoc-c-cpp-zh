```
struct node *bptr;
if(ptr==NULL)
{
    ptr = (struct node *) malloc(sizeof(struct node));
    ptr->val = data;
    ptr->left_child = NULL;
    ptr->right_child = NULL;
    ptr->balance = 0;
    *ht_inc = TRUE;
    return (ptr);
}
if(data < ptr->val)
{
    ptr->left_child = insert(data, ptr->left_child, ht_inc);
    if(*ht_inc==TRUE)
    {
        switch(ptr->balance)
        {
            case -1: /* Right heavy */
            ptr->balance = 0;
            *ht_inc = FALSE;
            break;
            case 0: /* Balanced */
            ptr->balance = 1;
            break;
            case 1: /* left heavy */
            aptr = ptr->left_child;
            if(aptr->balance == 1)
            {
                printf("Left to Left Rotation\n");
                ptr->left_child = aptr->right_child;
                aptr->right_child = ptr;
                ptr->balance = 0;
                aptr->balance=0;
                ptr = aptr;
            }
            else
            {
                printf("Left to right rotation\n");
                bptr = aptr->right_child;
                aptr->right_child = bptr->left_child;
                bptr->left_child = aptr;
                ptr->left_child = bptr->right_child;
                bptr->right_child = ptr;
                if(bptr->balance == 1)
                ptr->balance = -1;
                else
                ptr->balance = 0;
                if(bptr->balance == -1)
                aptr->balance = 1;
                else
                aptr->balance = 0;
                bptr->balance=0;
                ptr = bptr;
            }
            *ht_inc = FALSE;
        }
    }
}
if(data > ptr->val)
```