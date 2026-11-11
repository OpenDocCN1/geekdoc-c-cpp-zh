The following code snippet shows how to add a node in an empty linked list:

```
```c
void addnode(int q , int pr)
{
...
/* Step-3: ADDING A NODE INTO EMPTY LIST */
if(p==NULL)                         //if no list is currently available
{
        p = temp;                   //new node points to the first node
        p->next = NULL;             //set next address field
}
}
```
```

If initially the pointer p, does not point to any node, then, temp will be the first node as shown in Figure 10:

![](bbox=[0.306, 0.374, 0.769, 0.462])

The following code snippet shows how to add a node in a non-empty linked list:

```
```c
void addnode(int q , int pr)
{
...
else
{
/*Step-4: ADDING A NODE INTO A NON -- EMPTY LIST */
temp->next = p;
p = temp;                    //p now points to the new node
}
}
```
```

Now, *attach p* to the already present node temp’s next field, and shift the pointer p to point the newly created node. This is illustrated in Figure 11:

![](bbox=[0.259, 0.717, 0.802, 0.84])