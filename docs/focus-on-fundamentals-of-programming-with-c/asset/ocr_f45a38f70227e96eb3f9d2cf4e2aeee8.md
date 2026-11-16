```
// deletes the node after the node pointed to by p
NODEPTR deleteNodeAfter(NODEPTR *list, NODEPTR p) {
    NODEPTR q;
    if (p == NULL || (p->next == NULL)) {
        error("Invalid deletion.");
    }
    q = p->next;
    p->next = q->next;
    return q;
}

// returns the number of nodes in the list
int numElements(NODEPTR list) {
    int count=0;
    while (list) {
        count++;
        list = list->next;
    }
    return count;
}

// frees all the nodes in a list
void freeList(NODEPTR *list) {
    NODEPTR p;
    while (*list) {
        p = *list;
        *list = p->next;
        freeNode(p);
    }
}

// display an error message and aborts the program
void error(char *msg) {
    puts(msg);
    exit(1);
}
```

Output from your program should be sent to the terminal window (your screen) as well as the requested csis.txt output file. Be sure to read the document on Capturing Program Output. Your full name and Palomar ID number must appear as a comment in the source file that contains main(). Be sure to include the csis.txt output file in your zip archive.