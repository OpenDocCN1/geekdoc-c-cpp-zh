Since start points to the first node of linked list, so start->link will point to the second node of link list. After deletion of first node, the second node would become the first one, so start should be assign the address of the second node as-

```
start = start->link;
```

Now we should free the element to be deleted, which is pointed to by tmp.

```
free( tmp );
```

# 10.15.8 Deletion of a Node in Between or at the End

![](bbox=[0.22, 0.27, 0.95, 0.6])

We'll traverse the list and obtain a pointer which points to the node that is just before the node to deleted. Suppose this pointer is q, so the node to be deleted will be pointed by q->link, hence we assign this value to tmp as-

```
tmp = q->link;
```

So now tmp will point to the node to be deleted. Now we'll assign the link part of the node to be deleted to the link part of the previous node. It can be done as-

```
q->link = tmp->link;
```

Now link of previous node will point to node that is just after the node to be deleted. Finally we'll free the deleted node as-

```
free(tmp);
```

If node to be deleted is last node of linked list then second statement can be written as-

```
q->link = NULL;
```

# 10.15.9 Creation Of List

Creation of list is very simple if you have understood the above operations. It is similar to insert of an element at the end of the list. Initially we'll allocate memory for a node as-

```
tmp = malloc(sizeof(struct node));
tmp->info = data;
tmp->link = NULL;
```

If the list is empty and we are inserting the first element, then we'll have to initialize the pointer s as-