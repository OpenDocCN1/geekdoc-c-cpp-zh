46 Chapter 1. C/C++ Review

# llist

![](bbox=[0.25, 0.173, 0.772, 0.313])

```
int len(struct node *llist){
    int len = 0;
    while (llist != NULL){
        llist = llist->next;
        len++;
    }
    return len;
```

The element selection through pointer operator -> occurs frequently in the context of linked lists, trees, and graphs.

# Abstraction features of C++

The C++ language has a number of powerful features to bring programming closer to ideas and concepts intrinsic to the problem domain. Classes that arise later are all defined, provide a single service, and do not use these features. The Vector class defined above attempts to capture the abstract notion of vectors. C++ has a number of abstraction features beyond the basic class mechanism we have studied.++ supports object-oriented programming through inheritance of classes, multiple inheritance, and virtual and pure virtual functions. On many occasions, a single problem morphs into multiple instances, each of which has its own features while sharing a great deal in common with other instances. Object-oriented programming is the best way to tackle such problems.

An example of a problem well suited to object-oriented programming is the implementation of file systems. A file system creates the concept of file, which may be read, written, opened, and closed in standard ways. File systems vary in the way