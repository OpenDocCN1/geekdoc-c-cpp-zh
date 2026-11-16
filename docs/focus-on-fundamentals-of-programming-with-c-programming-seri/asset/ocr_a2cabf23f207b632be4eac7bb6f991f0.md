```
// adds a node to the end of a list
void addNodeLast(NODEPTR *list, NODEPTR t) {
    NODEPTR p;

    if (*list == NULL) {
        *list = t;
    }
    else {
        p = *list;
        while (p->next) {
            p = p->next;
        }
        p->next = t;
    }
}

// deletes the node at the end of a list
NODEPTR deleteNodeLast(NODEPTR *list) {
    NODEPTR p = NULL, q;

    if (*list) {
        p = *list;
        q = NULL;
        while (p->next) {
            q = p;
            p = p->next;
        }
        if (!q) {
            *list = NULL;
        }
        else {
            q->next = NULL;
        }
    }
    return p;
}
```