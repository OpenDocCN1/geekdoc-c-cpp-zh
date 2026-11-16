```
// returns a pointer to a new list containing the intersection of
// two lists

NODEPTR intersect(NODEPTR list1, NODEPTR list2) {
    NODEPTR p, q, r, s, newlist;
    int found;

    p = list1;
    newlist = NULL;
    r = NULL;
    while (p) {
        q = list2;
        found = 0;
        while (q && !found) {
            if (p->info == q->info) {
                found = 1;
            }
            else {
                q = q->next;
            }
        }
        if (found) {
            s = getNode();
            s->info = p->info;
            s->next = newlist;
            if (!r) {
                newlist = s;
            }
            else {
                r->next = s;
            }
            r = s;
        }
        p = p->next;
    }
    return newlist;
}
```

```
// display an error message and aborts the program

void error(char *msg) {
    puts(msg);
    exit(1);
}
```