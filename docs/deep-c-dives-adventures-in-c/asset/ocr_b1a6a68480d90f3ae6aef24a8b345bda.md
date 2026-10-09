Notice that we are making use of the rule that any pointer type can be cast to a void pointer and this is done automatically. So when we call:

```
```
int array1[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
int *element = get(array1, 1, 5);
```
```

the int  array1 is automatically upcast to void. If you prefer you can make this explicit:

```
```
int *element = get((void*)array1, 1, 5);
```
```

In short a void pointer is never used to process data, only to pass it around when its type isn't determined at compile time.

# ## Final Word

void is a useful construction, but it isn't just one thing. It is an indicator that a function doesn't return a result and it can be used to specify that a function takes no parameters. As a type it is useless for processing data, but excellent for passing data of unknown type to a function, or in any other situation where the data type isn't known until runtime.