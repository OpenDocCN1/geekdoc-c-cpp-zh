# 6.16.6 List object memory management

# 6.16.6.1 Default object construction

To use a list you must first instantiate the list object pointer. The default constructor functions allocate an empty list (no nodes or node data):

```
/* Default generic list constructor */
AjPList ajListNew (void)

/* Default string list constructor */
AjPList ajListstrNew (void);
```

All constructors return the address of a new list. The pointers do not need to be initialised to NULL but it is good practice to do so:

```
AjPList list = NULL;
AjPList liststr = NULL;

list = ajListNew();
liststr = ajListstrNew();

/* The objects are instantiated and ready for use */
```

# 6.16.6.2 Default object destruction

You must free the memory for a list once you are finished with it. The default destructor functions will free the list and the nodes but not the node data itself:

```
/* Default generic list destructor */
AjPList ajListFree (AjPList* Plist);

/* Default string list destructor */
AjPList ajListstrFree (AjPList* Plist);
```

Typical code for object destruction is as follows:

```
AjPList list = NULL;
AjPList liststr = NULL;

list = ajListNew();
liststr = ajListstrNew();

/* The objects are instantiated and ready for use ... do something with the list */

ajListFree(&list);
ajListFree(&liststr);

/* The lists are freed and the pointers reset to NULL, ready for reuse.
```