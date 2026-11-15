The comparison and destructor functions must be provided. As you can see from the prototype the comparison function returns a AjBool (which is ajTrue if the constraint is matched) and takes a generic void * argument whereas the destructor function must be of void return type and take a generic void ** argument.

Let us assume you have a list of sequence (AjPSeq) objects you want to garbage collect, removing all sequences from the list that are longer than 1000 characters. The comparison function would be as follows:

```
AjBool Compare(const void * ptr)
{
    if(ajSeqGetLen((AjPSeq)ptr) > 1000)
        return ajTrue;

    return ajFalse;
}
```

We cannot use the default sequence destructor function because its parameter is of the wrong type:

```
void ajSeqDel (AjPSeq* Pseq);
```

A const pointer is required, which means you must provide a wrapper function around the default destructor function:

```
void mySeqDelWrap(const void **ptr)
{
    ajSeqDel((AjPSeq *) ptr);

    return;
}
```

To perform garbage collection on a list of sequences (list) you would call:

```
void ajListPurge (list, Compare, mySeqDelWrap);
```

# 6.16.11 List sorting

A list may be sorted on up to three fields (elements of the C data structure) of the node data. Where more than one field is used the list is first sorted by field 1. Nodes with the same sort order for field 1 are then re-sorted by field 2 such that the relative sort order from field 1 is maintained. Similarly, if a third field is used, nodes with the same sort order for fields 1 and 2 are re-sorted by field 3 such that the relative sort order from sorting by fields 1 and 2 is preserved. The functions are :