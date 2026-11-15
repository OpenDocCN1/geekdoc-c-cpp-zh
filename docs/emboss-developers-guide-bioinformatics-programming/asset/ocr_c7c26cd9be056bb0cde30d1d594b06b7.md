A string list may be appended to an existing array by using:

```
ajint ajListstrToarrayAppend (const AjPList list, AjPStr** PParray);
```

The functions return the size of the array and in all cases memory for the array is (re)allocated as needed and the original list left untouched. The node data are not duplicated, so once these functions return, the list, the array and the node data must be freed. In the example below, code to create the list of sequences is not shown:

```
AjPSeq *seqarray = NULL;
AjPList list = NULL;
AjPSeq seqtmp = NULL;
AjIList iter = NULL;

... /* Code to allocate list of sequences */

ajListToarray(list, &seqarray);

/* Do something with the array */

/* Free the list and node data */
iter = ajListIterNew(list);

while(seqtmp = (AjPSeq) ajListIterGet(iter))
    ajSeqDel(&seqtmp);

ajListFree(&listnew);

/* Delete the iterator */
ajListIterDel(&iter);

/* Free the array */
AJFREE(seqarray);
```

# 6.16.13 List node functions

To invoke a function on all the nodes in a list use one of:

```
void ajListMap (AjPList list, void apply(void** Pptr, void* ptr), void* cl);
void ajListstrMap (AjPList list, void apply(AjPStr* Pstr, void* ptr), void* cl);
void ajListMapread (const AjPList list, void apply(void* ptr, void* ptr), void* cl);
void ajListstrMapread (const AjPList list, void apply(AjPStr str, void* ptr), void* cl);
```

The function that is applied is again of the same type as the comparison function used for garbage collection (see above). The *MapRead functions ensure that the function (apply) that's applied does not modify the list elements and, as such, takes a list that is const. In contrast, any type of operation is permitted with ajListMap and ajListstrMap.