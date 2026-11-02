```
```c
if(his->table == NULL)    /* enough memory ? */
{
    fprintf(stderr, "out of memory in histo_new()");
    exit(1);
}
else
{
    for(t=0; t<n_bins; t++)    /* initalize bins */
        his->table[t] = 0;
    return(his);
}
```
```

The main data structure is allocated in line 6, while the array for the moments is allocated in line 31. Some simple error-checking is included: It is verified that enough memory is available for the main data structure (lines 7-11) and for the moment array (line 32-36). Furthermore, it is verified that from is smaller than to (line 12-17) and that the number of bins is positive (lines 20-24). The histogram is initialized in lines 18-19, 25-28 and 37-39.

The function histo_delete() receives a pointer to a histogram, frees the memory associated with the histogram and returns nothing:

```
```c
void histo_delete(histo_t *his)
{
    free(his->table);
    free(his);
}
```
```

All histogram objects are created dynamically by calling histo_new(), which corresponds to a call of the constructor or new in C++, as explained in Sec. 5.3 The objects are addressed via pointers. Whenever a function concerning an object of the histo class is called, the first argument will always be a pointer to the corresponding histogram. When avoiding direct access to the structure, the realization using C is perfectly equivalent to C++ or other object-oriented languages. Inheritance can be implemented, by including pointers to histo_t objects in other type definitions. When these higher level objects are created, a call to histo_new() must be included, while a call to histo_delete(), corresponding to the destructor in C++, is necessary, to implement a correct deletion of the more complex objects.

As a final example, the functions for inserting an element into the table and calculating the mean are presented. It is easy to figure out how other functions can be realized, such as for calculating the variance/higher mo-