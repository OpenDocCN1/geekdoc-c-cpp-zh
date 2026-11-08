# INSERTION

Consider the linked list shown in Figure 16-7.

![](bbox=[0.307, 0.163, 0.731, 0.222])

FIGURE 16-7  Linked list before item insertion

Suppose that p points to the node with info 65, and a new node with info 50 is to be created and inserted after p. Consider the following statements:

```
newNode = new nodeType;    // create newNode
newNode->info = 50;       // store 50 in the new node
newNode->link = p->link;
p->link = newNode;
```

Table 16-1 shows the effect of these statements.

**TABLE 16-1  Inserting a Node in a Linked List**

| Statement | Effect |
|---|---|
| `newNode = new nodeType;` | A new node is allocated. |
| `newNode->info = 50;` | The value 50 is stored in the new node. |
| `newNode->link = p->link;` | The new node's link is set to the node currently following `p`. |
| `p->link = newNode;` | `p` is linked to the new node, inserting it after `p`. |