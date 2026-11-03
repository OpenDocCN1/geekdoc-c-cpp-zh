The memory space of key node that has been deleted is freed. The figure below shows the relative position of the key node.

![](bbox=[0.12, 0.23, 0.88, 0.38])

```
/* ************************************************************ */
/* FUNCTION DELETE */
/* ************************************************************ */

node *delete(node *head)
{
    node *find(node *p, int a);
    int key;    /* item to be deleted */
    node *n1;   /* pointer to node preceding key node */
    node *p;    /* temporary pointer */

    printf("\nWhat is the item (number) to be deleted?");
    scanf("%d", &key);

    if(head->number == key)  /* first node to be deleted */
    {
        p = head->next;    /* pointer to 2nd node in list */
        free(head);        /* release space of key node */
        head = p;          /* make head to point to 1st node */
    }
    else
    {
        /* find key node and delete it */
        n1 = find(head, key);
        if(n1 == NULL)
            printf("\n key not found\n");
        else
        {
            p = n1->next->next;    /* pointer to the node following the key node */
            free(n1->next);        /* free key node */
            n1->next = p;          /* establish link */
        }
    }
    return(head);
    /* USE FUNCTION Find() HERE */
}
```

Fig. 15.9 A function for deleting an item from linked list

The execution of the following code deletes the key node.

p = n1->next->next;
free (n1->next);