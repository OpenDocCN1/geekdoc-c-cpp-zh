# The -> operator

Suppose we define an array of pointers to Vector objects as

```
Vector *v[100];
```

Each entry may be made to point to a Vector object as explained already. Suppose all those Vector objects are initialized in some way and we want to print the norm of each Vector object. The following syntax will not do:

```
for(int i=0; i < 100; i++)
cout<<v[i].norm()<<endl;
```

The problem is here that *v[i] is a pointer and not a Vector. The correct syntax is as follows:

```
for(int i=0; i < 100; i++)
cout<<(*v[i]).norm()<<endl;
```

The parentheses in (*v[i]).norm() are needed. The * dereferencing operator has lower precedence than the . selection operator. This usage occurs often enough that there is a special operator -> that combines dereferencing and selection. It may be used as follows:

```
for(int i=0; i < 100; i++)
cout<<v[i]->norm()<<endl;
```

We will look at another example of the element selection through pointer operator ->. Consider the C struct

```
struct node{
  double val;
  struct node *next;
};
```

A struct is a package of data items. Here the two data items of struct node are val and a pointer to the next node. The pointer next is a link from one node to the next. A series of nodes may be chained together to form a linked list.

Figure 1.6 shows a linked list with each node pointing to the next. The variable list points to the beginning of the list. The next pointer of the last node is set to NULL.

The following function finds the length of a linked list: