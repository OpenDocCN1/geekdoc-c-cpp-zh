# INSERTION

Consider the linked list shown in Figure 18-7.

![](bbox=[0.182, 0.169, 0.912, 0.256])

**FIGURE 18-7** Linked list before item insertion

Suppose that p points to the node with info 65, and a new node with info 50 is to be created and inserted after p. Consider the following statements:

```
newNode = new nodeType;    //create newNode
newNode->info = 50;        //store 50 in the new node
newNode->link = p->link;
p->link = newNode;
```

Table 18-1 shows the effect of these statements.

**TABLE 18-1** Inserting a Node in a Linked List

| Statement | Effect |
|---|---|
| `newNode = new nodeType;` | A new node is allocated. The list remains `head → 45 → 65 → 34 → 76`; `p` points to 65 and `newNode` is not yet linked. |
| `newNode->info = 50;` | The newly allocated node stores the value `50`. The existing list remains unchanged. |
| `newNode->link = p->link;` | The new node's link is set to the node after `p`, so `newNode → 34`. |
| `p->link = newNode;` | The new node is inserted after `p`: `head → 45 → 65 → 50 → 34 → 76`. |