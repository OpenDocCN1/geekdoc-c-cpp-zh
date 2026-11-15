
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

### 6.16.11 List sorting

A list may be sorted on up to three fields (elements of the C data structure) of the node data. Where more than one field is used the list is first sorted by field 1. Nodes with the same sort order for field 1 are then re-sorted by field 2 such that the relative sort order from field 1 is maintained. Similarly, if a third field is used, nodes with the same sort order for fields 1 and 2 are re-sorted by field 3 such that the relative sort order from sorting by fields 1 and 2 is preserved. The functions are :

```
void ajListSort (AjPList list,int (*sort1) (const void*, const void*));
void ajListSortTwo (AjPList list,int (*sort1) (const void*, const void*),
int (*sort2) (const void*, const void*));
void ajListSortTwoThree (AjPList list,int (*sort1) (const void*, const void*),
int (*sort2) (const void*, const void*),
int (*sort3) (const void*, const void*));
```

Lists may also be sorted (by up to two fields) and duplicate nodes (nodes with the same sort order) removed. The functions are:

```
void ajListSortUnique (AjPList list,
int (*compar) (const void*, const void*),
void (*nodelete)(void**, void*));
void ajListSortTwoUnique(AjPList list,
int (*sort1) (const void*, const void*),
int (*sort2) (const void*, const void*),
void (*nodelete)(void**, void*));
```

One or more comparison functions sort* must be provided. These take two generic void * arguments for the two objects passed, and return the sort order of the objects as an integer: which should be -1 if the first object sorts higher than the second and +1 otherwise. For the ajListSortUnique* functions, a destructor function is the same as for ajListMap (see above): it must be of void return type and take a generic void ** argument and a (usually NULL) second argument which can be used to pass external data to the function.

Let us assume you have a list of sequences (AjPSeq objects) you want to sort by length (shortest first) and make unique, removing any sequences whose length is the same as another sequence in the list such that the final list of sequences have unique lengths. The comparison function would be as follows:

```
int Compare(const void *ptr1, const void * ptr2)
{
    if(ajSeqGetLen((AjPSeq)ptr1) < ajSeqGetLen((AjPSeq)ptr2))
        return -1;
    return 1;
}
```

The destructor function is the same as for list deletion collection above.

To sort the list and remove sequences of duplicate length you would call:

```
void ajListSortUnique (list, Compare, mySeqDelWrap);
```

### 6.16.11.1 String comparison functions

Various string comparison functions are provided in ajstr.c and are useful for sorting lists of strings. The functions perform case-sensitive and case-insensitive comparison, with and without wildcard characters. Variants of the function support string objects (AjPStr) and C-type (char *) strings (not all shown):

```
/* String to C-type string */
int ajStrCmpC (const AjPStr thys, const char *text);

/* String to string */
int ajStrCmpS (const AjPStr str, const AjPStr str2);

/* Case-insensitive string to string */
int ajStrCmpCaseS (const AjPStr str1, const AjPStr str2);

/* String to C-type string using the first len characters only */
ajint ajStrCmpLenC (const AjPStr thys, const char *text, ajuint len);

/* String to string using the first len characters only */
int ajStrCmpLenS (const AjPStr str, const AjPStr str2, ajuint len);

/* String to C-type string with wildcards.*/
int ajStrCmpWildC (const AjPStr thys, const char* text);

/* String to string with wildcards.*/
int ajStrCmpWildS (const AjPStr thys, const AjPStr str);

/* Case-insensitive string to C-type string with wildcards.*/
int ajStrCmpWildCaseC (const AjPStr thys, const char* text);

/* Case-insensitive string to string with wildcards.*/
int ajStrCmpWildCaseS (const AjPStr thys, const AjPStr str);

/* Same as ajStrCmpS but strings are cast as void */
int ajStrVcmp (const void* str1, const void* str2);
```

There are also comparison functions for handling C-type strings:

```
/* Case-insensitive C-type string to C-type string */
int ajCharCmpCase (const char* txt1, const char* txt2);

/* Case-insensitive C-type string to C-type string using the first len characters only */
int ajCharCmpCaseLen (const char* txt1, const char* txt2, ajuint len);

/* C-type string to C-type string using wildcards. */
ajint ajCharCmpWild (const char* txt1, const char* txt2);

/* Case-insensitive C-type string to C type string using wildcards. */
ajint ajCharCmpWildCase (const char* txt1, const char* txt2);
```

The functions return an integer representing the sort order which is -1 if the first string should sort before the second, +1 if the second string should sort first, or 0 if they are identical.

### 6.16.12 List conversion

A list may be converted to an array by using:

```
ajint ajListToarray (const AjPList list, void*** PParray);
ajint ajListstrToarray (const AjPList list, AjPStr** PParray);
```

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

ajListFree(&list);

/* Delete the iterator */
ajListIterDel(&iter);

/* Free the array */
AJFREE(seqarray);
```

### 6.16.13 List node functions

To invoke a function on all the nodes in a list use one of:

```
void ajListMap (AjPList list, void apply(void** Pptr, void* ptr), void* cl);
void ajListstrMap (AjPList list, void apply(AjPStr* Pstr, void* ptr), void* cl);
void ajListMapread (const AjPList list, void apply(void* ptr, void* cl), void* cl);
void ajListstrMapread (const AjPList list, void apply(AjPStr str, void* ptr), void* cl);
```

The function that is applied is again of the same type as the comparison function used for garbage collection (see above). The *MapRead functions ensure that the function (apply) that's applied does not modify the list elements and, as such, takes a list that is const. In contrast, any type of operation is permitted with ajListMap and ajListstrMap.

## 6.17 Handling arrays

### 6.17.1 Introduction

Array handling is greatly simplified in EMBOSS. AJAX provides dynamic array objects which grow automatically as required thereby saving you the bother of managing the memory yourself. This makes your code cleaner and less error-prone. Objects are provided for handling arrays of various dimensions (1D, 2D or 3D) of the following C datatypes:

- Character (char)
- Short integer (ajshort)
- Unsigned integer (ajuint)
- Integer (ajint)
- Floating point number (float)
- Long floating point number (ajlong)
- Double-precision floating point number (double).

The objects can be allocated to a default or a specified reserved size. Each object keeps track of the reserved space available (in case a function is called which must extend the array) and the actual length of the array. Arrays of higher dimensions can nest arrays of lower dimensions.

Functions are provided for returning the current length and for getting and setting array elements. The array elements should only ever be accessed using these functions. If you assign a value to an element which is beyond the current size of the array, then the array will be dynamically reallocated to a sufficient size to accommodate the new element. In contrast, if you try to retrieve an element beyond the current size of the array an error will be generated.

The C-type array may be retrieved from any of the array objects should this be required. This allows standard array notation to be used to access array elements. Functions are provided to sort C-type arrays of integers, unsigned integers and floating point numbers in various ways.

Array objects are typically created directly within the C source code. A floating point array can however be specified in the ACD file (the array ACD datatype) and a pointer to a corresponding AJAX object (AjPFloat) retrieved by the program.

### 6.17.2 AJAX library files

AJAX library files for handling arrays are listed in the table below. Library file documentation, including a complete description of datatypes and functions, is available at: http://emboss.open-bio.org/rel/dev/libs/

| Library file documentation | Description |
|---|---|
| ajarr | General array handling |
| ajsort | Array sorting |
