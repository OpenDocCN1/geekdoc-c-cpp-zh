```
if (*curErr) {
    errorHandler();
    *curErr = 0;
}
```

cannot modify the address that curErr contains:

```
curErr = &myError; // illegal
```

# Constant Pointer to const

To make both the pointer and the object being pointed to constant, they mustoth be declared const.

```
syntax:      const <type> *const cpc;
```

Here, cpc is a constant pointer to a constant value of type <type>.

For example:

```
const char *const cpc = "Haley";
```

defines a constant pointer to a constant. cpc is a constant pointer to characters
that are constant. In this case neither the value of the object addressed by cpc
nor the address itself may be changed, i.e., cpc can't change and the thing it
points to can't change:

```
cpc[3] = 'x'; // error
*cpc = 'x'; // error
cpc = "Samantha"; // error
```