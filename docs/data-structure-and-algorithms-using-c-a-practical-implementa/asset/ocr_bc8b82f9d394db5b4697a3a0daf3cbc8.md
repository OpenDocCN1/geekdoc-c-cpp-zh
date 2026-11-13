```
Data type member2;
................
................
Data type membern;
Struct link *var1,*var2;
}
```

# Ex:

```
Struct Dlink
{
int info;
struct Dlink *next,*prev ;
};
```

# Graphically

![](bbox=[0.1, 0.41, 0.9, 0.67])

# LOGIC FOR CREATION

```
Struct link
{
int info;
struct link *next,*prev;
};

Struct link start,*node;
Node=&start;
Allocate a memory to node->next
Node->next ->prev = node
Node = node->next
Node->next = NULL
```