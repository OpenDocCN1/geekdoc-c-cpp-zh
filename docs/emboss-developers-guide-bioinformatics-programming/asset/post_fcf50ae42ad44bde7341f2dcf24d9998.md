
/* @data AjPPdbtosp ***********************************************************
**
** Ajax Pdbtosp object.
**
** Holds swissprot codes and accession numbers for a PDB code.
**
** AjPPdbtosp is implemented as a pointer to a C data structure.
**
** @alias AjSPdbtosp
** @alias AjOPdbtosp
**
** @attr Pdb [AjPStr] PDB code
** @attr Acc [AjPStr*] Accession numbers
** @attr Spr [AjPStr*] Swissprot codes
** @attr n [ajint] No. entries for this pdb code
** @attr Padding [char[4]] Padding to alignment boundary
**
** @@
********************************************************************************/

typedef struct AjSPdbtosp
{
    AjPStr Pdb;
    AjPStr *Acc;
    AjPStr *Spr;
    ajint n;
    char Padding[4];
} AjOPdbtosp;
#define AjPPdbtosp AjOPdbtosp*

There is nothing new here other than Acc and Spr which are both pointers to AjPStr objects. These would have better been declared by using AjPPStr but that is not done here. As an AjPStr is itself a pointer (to a string object proper) you can see that we're dealing with pointers to pointers. In this case Acc and Spr are used to create two arrays of strings as you can see in the constructor function (below).

### 5.5.1.2 Object construction

Here is the constructor function:

```
/* @func ajPdbtospNew ***********************************************************
**
** Pdbtosp object constructor. Fore-knowledge of the number of entries is
** required. This is normally called by the ajPdbtospReadCNew /
** ajPdbtospReadNew functions.
**
** @param [r] n [ajint] Number of entries
**
** @return [AjPPdbtosp] Pointer to a Pdbtosp object
** @@
********************************************************************************/
AjPPdbtosp ajPdbtospNew(ajint n) /* 1. */
{
    AjPPdbtosp ret = NULL; /* 2. */
    ajint i = 0;

    AJNEW0(ret); /* 3. */
    ret->Pdb = ajStrNew(); /* 5. */

    if (n)
    {
        AJCNEW0(ret->Acc, n); /* 4. */
        AJCNEW0(ret->Spr, n); /* 4. */
        for (i = 0; i < n; i++)
        {
            ret->Acc[i] = ajStrNew(); /* 6. */
            ret->Spr[i] = ajStrNew(); /* 6. */
        }
    }

    ret->n = n; /* 7. */

    return ret;
}
```

The commented lines are as follows:

- 1. The first line declares that the function returns an object pointer of type AjPPdbtosp. The parameter ajint n is the size the Acc and Spr arrays should be, i.e. the number of pairs of Acc / Spr values that the object will hold.

- 2. The next line declares a variable called ret. This is the object pointer that is going to have memory allocated to it and will be returned to the calling function.

- 3. AJNEW0(ret); is the line that allocates an object proper to the pointer ret. This will now point to an instance of an AjPPdbtosp memory. By the time AJNEW0(ret); returns, memory space for an AjPPdbtosp object is reserved. This means enough space for an AjPStr, an ajint and two pointers (AjPStr *). Note that the two arrays or any string objects proper have not yet been allocated!

AJNEW0 sets all the structure elements to 0, this means the element n is set to 0 and the three pointers are set to NULL. AJNEW0 is a macro: it will allocate a single object of the correct type to any pointer that is passed to it – it can be used with any object.

- 4. Compare AJNEW0 to the two AJCNEW0 lines. AJCNEW0 will allocate an array of objects of any type and initialises the new variables to 0 or NULL as required. In this case, arrays of n objects each will be created. It is important to bear in mind here that ret->Acc and ret->Spr are passed to the macro. These are of the type AjPStr *, which means that the ‘object’ which they point to is in fact another pointer variable. Therefore these macro calls will allocate arrays of n pointers, not arrays of instances of AjPStr objects as one might (incorrectly) first imagine.

They create an array of n AjPStr object pointers allocated to each of Acc and Spr. In other words, ret->Acc and ret->Spr will point to blocks of memory each holding n pointer variables which are as yet NULL (unallocated).

- 5. The arrays are created but still no strings yet. ret->Pdb = ajStrNew(); allocates memory for a string object to the pointer Pdb in the new object. Notice that -> is used to dereference the pointer ret; and get to the Pdb element. This is the standard way in C of accessing elements in a data structure when you have a pointer to that data structure.

- 6. The lines ret->Acc[i] = ajStrNew(); and ret->Spr[i] = ajStrNew(); allocate memory for the n string objects for each array. It also illustrates how pointer and array notation can be used together. In this case, the ith element of the arrays that ret->Acc and ret->Spr point to are accessed. The elements in these arrays are AjPStr (object pointers) and a string object is allocated to each of them.

- 7. The rest is obvious. The integer in the object is set to the size of the arrays and the pointer to the new object, complete with an allocated string and two arrays of strings, is returned to the calling function by return ret;. Note that the constructor should be coded to deal with negative arguments in a safe way, but that is not done here.

### 5.5.1.3 Object destruction

It is the job of the destructor function to free the object itself and any memory that its member elements might point to. The destructor safely clears up all of the memory that was allocated by the constructor. This is achieved by calling other destructor functions as appropriate and by using AJFREE. The code is shown below:

```
/* @func ajPdbtospDel *************************************************************
**
** Destructor for Pdbtosp object.
** *
** @param [w] thys [AjPPdbtosp*] Pdbtosp object pointer
**
** @return [void]
** @@
**********************************************************************************/

void ajPdbtospDel(AjPPdbtosp *thys) /* 1. */
{
    AjPPdbtosp pthis = NULL; /* 2. */
    ajint i;

    if (!thys)
        return;

    pthis = *thys;

    if (!pthis)
        return;

    ajStrDel(&pthis->Pdb); /* 3. */

    if (pthis->n)
    {
        for (i = 0; i < pthis->n; i++)
        {
            ajStrDel(&pthis->Acc[i]); /* 4. */
            ajStrDel(&pthis->Spr[i]); /* 4. */
        }

        AJFREE(pthis->Acc); /* 5. */
        AJFREE(pthis->Spr); /* 5. */
    }
    AJFREE(pthis); /* 6. */
    (*thys) = NULL; /* 6. */
    return;
}
```

Again, this is broken down comment by comment:

- 1. The function, like all destructors, takes the address of the object pointer being deleted (AjPPdbtosp *thys).
- 2. For convenience a second pointer is declared and is used in the following lines to dereference thys. This is purely for reasons of clarity. The function returns if either an empty address was passed or if the pointer stored there is NULL.
- 3. The string object in AjPPdbtosp is deleted first by calling the default destructor function with the address of the string.
- 4. The string objects proper, referenced through the arrays, are deleted by calling ajStrDel in a loop for every array element in both arrays.
- 5. AJFREE is then called to delete the arrays themselves, referenced by pthis->Acc and pthis->Spr.
- 6. Once the loop terminates AJFREE is again called, this time freeing memory for the AjPPdbtosp object itself. The pointer is set to NULL so that it's ready for reuse by the calling function.

It should be clear that although AJFREE will free the memory pointed to by its argument, as used here it frees the arrays but not the string objects proper that are pointed to; that is the job of the ajStrDel calls in the preceding code.

### 5.5.1.4 Usage example

Here is a code snippet illustrating how the object constructor and destructor could be used. You'll notice they're used in exactly the same way as any other object:

```
int main()
{
    AjPPdbtosp ptr = NULL;

    ptr = ajPdbtospNew(10);
    ajPdbtospDel(&ptr);

    /* ptr will have been reset to NULL now, and is ready for reuse */
    ptr = ajPdbtospNew(10);
    ajPdbtospDel(&ptr);
}
```
