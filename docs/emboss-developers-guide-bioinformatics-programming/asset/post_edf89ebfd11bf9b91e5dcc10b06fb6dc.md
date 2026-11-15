
```c
ajint comp(const void* x, const void* y)
{
    const char* sx;
    const char* sy;

    sx = (const char*) x;
    sy = (const char*) y;

    return (ajint) ajCharCmpCase(sx, sy);
}
```

The following hash function may be used:

```c
ajuint hash(const void* key, ajuint hashsize)
{
    ajuint hash;
    const char* s;

    s = (const char*) key;

    for(hash = 0; *s; s++)
        hash = (hash * 127 + toupper((ajint)*s)) % hashsize;

    return hash;
}
```

### 6.18.5.2 Default object destruction

You must free the memory for an object once you are finished with it. A default destructor function is provided for generic and string hash tables:

```c
void	 ajTableFree (AjPTable* Ptable);
void	 ajTablestrFree (AjPTable* Ptable);
```

It is the responsibility of the calling function to destroy any objects once they are finished with:

```c
AjPTable table = NULL;

table = ajTableNewFunctionLen(50, comp, hash);

/* Do something with the instantiated table */

ajTableFree(&table);

/* The memory is freed and the pointer reset to NULL, ready for re-use. */

table = ajTablestrNew(50);

/* The pointer variable is reallocated. Do something else with the new table. */

ajTableFree(&table);

/* Done with the object so the memory is freed. */
```

### 6.18.5.3 Alternative object construction and loading

To create a generic hash table with an explicit (rather than estimated) number of key:value pairs use:

```c
AjPTable ajTableNewLen (ajint n,
    ajint cmp(const void* x, const void* y),
    unsigned hash(const void* key, unsigned hashsize));
```

### 6.18.6 Table hash functions

A few table hash functions used during hash table construction (see above) are provided for convenience for string tables only. These provide case-sensitive and case-insensitive hashing for hash tables of EMBOSS strings (AjPStr) and C-type (char *) strings:

```c
/* Case-insensitive hashing of EMBOSS strings */
unsigned ajTableStrHash (const void* key, unsigned hashsize);
/* Case-sensitive hashing of EMBOSS strings */
unsigned ajTableStrHashCase (const void* key, unsigned hashsize);
```

### 6.18.7 Table comparison functions

A few table comparison functions used during hash table construction (see above) are provided for convenience for string tables only. These provide case-sensitive and case-insensitive comparison for hash tables of EMBOSS strings (AjPStr):

```c
/* Case-sensitive comparison of EMBOSS strings */
ajint ajTableStrCmp (const void* ptrx, const void* ptry);
/* Case-insensitive comparison of EMBOSS strings */
ajint ajTableStrCmpCase (const void* ptrx, const void* ptry);
```

### 6.18.8 Table edit functions

Key:value pairs may be added to a table, removed from a table or the value associated with a key may be changed.

ajTablePut is used to set the value associated with a given key in a hash table. It will return the previous value or, if the table does not hold the specified key, it will add the key and value and return NULL.

```c
void* ajTablePut (AjPTable table, const void* key, void* value);
```

ajTableRemove will remove the key:value pair from a table and returns the removed value. If the table does not hold the specified key then the function merely returns NULL:

```c
void* ajTableRemove (AjPTable table, const void* key);
```

### 6.18.9 Table query functions

The true key or value associated with a given key may be returned by using:

```c
/* Return the value */
void* ajTableFetch (const AjPTable table, const void* key);

/* Return the key */
void* ajTableFetchKey (const AjPTable table, const void* key);
```

ajTableFetch is the standard function that returns a value given a query key.
ajTableFetchKey is provided to return the true key (with any capitalisation) in cases where a case-insensitive hash table is used.

To return the number of key:value pairs in a hash table use:

```c
ajint ajTableGetLength (const AjPTable table);
```

### 6.18.10 Table map functions

It is possible to apply a function to each key:value in a hash table using:

```c
void ajTableMap (AjPTable table, void apply(const void* key, void** Pvalue, void* ptr), void* ptr);
void ajTableMapDel (AjPTable table, void apply(const void** Pkey, void** Pvalue, void* ptr), void* ptr);
```

The function called by ajTableMap should not delete any keys (although values can be modified) whereas the function called by ajTableMapDel may delete keys. In both cases a function must be provided.

Assume that you have a hash table with EMBOSS string keys and integer values and that you want to apply one function to print the key:value pair and another to free a key:value pair.
The print functions will look something like:

```c
static void print(const void* key, void** value, void* cl)
{
    AjPStr keystr;
    ajint *valptr;

    keystr = (AjPStr) key;
    valptr = (ajint *) *value;

    ajUser("type '%S' found %d times", keystr, *valptr);

    return;
}
```

whereas the delete function would be:

```c
static void delete(const void** key, void** value, void* cl)
{
    AjPStr keystr;
    ajint *valptr;

    keystr = (AjPStr) *key;
    valptr = (ajint *) *value;

    ajStrDel(&keystr);
    AJFREE(valptr);

    *key = NULL;
    *value = NULL;

    return;
}
```

To call the functions you would use something like:

```c
AjPTable table = NULL;

/* Allocate table */
ajTableMap(table, print, NULL);
ajTableMapDel(table, delete, NULL);
```

### 6.18.11 Print functions

Functions are provided to print a string hash table of EMBOSS strings (AjPStr):

```c
void ajTablestrPrint (const AjPTable table);
```

## 6.19 Handling menus

### 6.19.1 Introduction

Selecting from a list of options is often necessary in molecular biology programs. Two ACD datatypes (list and selection) provide slightly different styles of list but both present a user with a list of options they can choose from. For the user, the difference between the list and selection datatype is minimal and lies only in the way the choices are labelled. In a selection datatype the choices are numbered automatically from 1 upwards. In a list datatype the choices can be labelled by any arbitrary text. The user can choose one of the options by either typing the number (for a selection type) or the label text (for a list type), or (both list types) a non-ambiguous part of the descriptive text itself given after the number or label. In practice, the list data type is preferred.

### 6.19.2 AJAX library files

There is no specific AJAX library file for handling menus. Selections from menus are handled as strings or arrays of strings. You should consult the documentation for further information about string handling. Library file documentation is available online at: http://emboss.open-bio.org/rel/dev/libs/

| Library file documentation | Description |
|---|---|
| ajstr | String handling |

ajstr.h/c. Defines the string object (AjPStr) used for handling strings from the ACD file (see Section 6.4, ‘Handling simple ACD datatypes’). They contain most of the functions you will ever need for general string handling (Section 6.5, ‘Handling strings’).

### 6.19.3 ACD datatypes

There are two ACD datatypes for handling menus:

- **list**: A list of options (text descriptions) with text labels. The user is presented with a limited list of options they can choose from. The choices can be labelled by any arbitrary text label. The option descriptions are usually more verbose than for the selection datatype.
- **selection**: A list of options (text descriptions) with automatically generated numerical labels. The user is presented with a limited list of options they can choose from. The choices are numbered automatically from 1 upwards.

### 6.19.4 ACD data definition

### 6.19.4.1 list menu

A typical ACD definition for a list menu:

```
list: frame [
  standard: "Y"
  help: "Allows selection from a set of reading frames"
  default: "1"
  minimum: "1"
  maximum: "1"
  header: "Translation frames"
  values: "1:1, 2:2, 3:3, F:Forward three frames, -1:-1, -2:-2, -3:-3, R:
Reverse three
frames, 6:All six frames"
  delimiter: ","
  codedelimiter: "::"
  information: "Frame(s) to translate"
}
```

The user will be presented with the title of the menu from the header: attribute. After that will appear the tag/text information from the values: attribute. Following that will be the prompt from the information: attribute. It will look something like this:

```
Translation frames
1       1
2       2
3       3
F       Forward three frames
-1      -1
-2      -2
-3      -3
R       Reverse three frames
6       All three frames
Frame(s) to translate[1] :
```

The user is allowed (generally) to supply a comma-separated list of options from the above; this depends on the minimum and maximum values. In the above example both the minimum number of selections and the maximum number of selections are set to 1, therefore only one selection value is allowed. Selection is done by typing the tag values, therefore if the maximum count had been set to 3 then a user entry of "-1,F,6" would be a valid input.

The codedelimiter attribute allows you to select any character to separate the tags from the text in the values attribute. The delimiter attribute allows you to choose a character to separate the tag/text pairs within the values attribute.

### 6.19.4.2 selection menu

A typical ACD definition for a selection menu:

```
select: order
[
    casesensitive: "N"
    default: "score"
    delimiter: ","
    header: "Sort order of results"
    help: "Name of the output file which holds the results of the analysis."
    information: "Sort order of results"
    maximum: "1"
    minimum: "1"
    information: "Select sort order of results"
    standard: "Y"
]
```
