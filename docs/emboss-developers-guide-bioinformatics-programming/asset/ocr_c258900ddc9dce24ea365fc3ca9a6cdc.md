# 2 YOUR FIRST EMBOSS APPLICATION

function (ajStrNew) and destructor function (ajStrDel) are provided for this purpose.
Their use is shown below:

```
```c
/* newstr is NULL, no memory is allocated */
AJPStr newstr=NULL;

/* newstr now points to a string object in memory and is ready for use by
our program */
newstr = ajStrNew();

/* memory for the string object is freed. The program can terminate without
potentially leaking memory. */
ajStrDel(&newstr);
```
```

You do not need to call the constructor function for ACD variables because memory is
allocated for these by the call to embInitP. There is risk of memory error if you do. In the
following rather contrived and bugged code the call to ajAcdGetString will overwrite the
pointer to memory allocated and returned by the (unnecessary) call to ajStrNewC:

```
```c
/* This code is bugged */
AJPStr astring=NULL;

/* allocates memory for all ACD data items */
embInitP("stringplay", argc, argv, "myemboss");

/* newstr now points to a string object in memory */
astring = ajStrNewC("Hello");

/* this call will break the handle to the memory allocated by ajStrNewC */
astring = ajAcdGetString("astring");
```
```

The correct code is:

```
```c
AJPStr astring=NULL;

/* allocates memory for all ACD data items */
embInitP("stringplay", argc, argv, "myemboss");

/* Get a string value from ACD */
astring = ajAcdGetString("astring");

/* memory for the string object is freed. The program can terminate without
potentially leaking memory. */
ajStrDel(&astring);
```
```

A string object was created by embInitP and must be freed once you are done with it. That is
what the call ajStrDel(&astring); is for.