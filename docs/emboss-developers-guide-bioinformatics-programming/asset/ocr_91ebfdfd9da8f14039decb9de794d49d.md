The function takes the address of the AjPInt2d object (thys) that is to be freed. To get to the object proper you must dereference thys, i.e. everywhere in the function body where you see *thys. You will recall that Ptr references an array of AjPInt object pointers, each of which points to array of integers.

The integer arrays are freed by calling the destructor function ajIntDel in a loop. This destructor takes the address of a AjPInt. Array notation is used to index the ith element of the AjPInt array, having first dereferenced thys ((*thys) ->Ptr[i]). This retrieves an individual AjPInt object, the address of which is needed by the destructor which is why you have ajIntDel(&((*thys) ->Ptr[i])) ;.

AJFREE is then called twice. The first call (AJFREE ( (*thys) ->Ptr) ;) frees the array of AjPInt. The second call (AJFREE (*thys) ;) frees the AjPInt2d object itself. You can see that the pointer (thys) that is passed to the function is set to NULL using the code *thys = NULL;.

# 5.5.3.4 AjPInt2d putting and getting array elements

The function ajInt2dGet is used to retrieve a value from a 2D integer array. The source code is below:

```
/* @func ajInt2dGet *************************************************************
**
** Retrieve an element from an AJAX 2d integer array.
**
** If the given array is a NULL pointer, simply returns.
**
** @param [r] thys [const AjPInt2d] Pointer to the ajint array.
** @param [r] elem1 [ajuint] array element.
** @param [r] elem2 [ajuint] array element.
**
** @return [ajint] contents of array element
** @category cast [AjPInt2d] Retrieve an integer from an array
**
** @@
*******************************************************************************/

ajint ajInt2dGet(const AjPInt2d thys, ajuint elem1, ajuint elem2)
{
    AjPInt t;

    if(!thys || elem1>=thys->Len)
        ajErr("Attempt to access bad ajint array index [%d][%d]\n",elem1,
              elem2);

    t = thys->Ptr[elem1];
    if(!t)
        ajErr("Attempt to access bad 1st dimension [%d]\n",elem1);

    return ajIntGet(t,elem2);
}
```

The element in column elem1 and row elem2 will be retrieved from the array thys. An error is raised if you try to inspect an element that has not been allocated. Otherwise the value of the element is returned.