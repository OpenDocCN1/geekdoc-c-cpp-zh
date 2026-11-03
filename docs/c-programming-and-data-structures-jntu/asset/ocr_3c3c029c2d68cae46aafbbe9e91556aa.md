```
printf("\nkey is not found \n");
else /* insert new node */
{
    new = (node *)malloc(sizeof(node));
    new->number = x;
    new->next = n1->next;
    n1->next = new;
}
}
return(head);
node *find(node *list, int key)
{
    if(list->next->number == key) /* key found */
        return(list);
    else
        if(list->next == NULL) /* end */
            return(NULL);
        else
            find(list->next, key);
}
```

Fig. 15.8 A function for inserting an item into a linked list

However, if the new item is to be inserted after an existing node, then we use the function find recursively to locate the 'key node'. The new item is inserted before the key node using the algorithm discussed above. This is illustrated below:

# Before Insertion

```
new = (node *)malloc(sizeof(node));
new->number = x;
```

![](bbox=[0.1, 0.9, 0.95, 0.97])

# After Insertion

```
new->next = n1->next;
n1->next = new;
```