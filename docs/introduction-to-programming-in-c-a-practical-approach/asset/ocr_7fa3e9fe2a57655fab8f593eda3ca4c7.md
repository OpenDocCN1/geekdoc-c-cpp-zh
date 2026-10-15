The dynamic allocation of memory will allow us to manage quantities of data at the moment the program is executed and not at the moment of compilation.

In the previous example, if the size of an integer is 2 bytes, memory will be reserved for 100 integers.

The previous case can also be defined in the form

```
int *p = (int *) malloc (100 * sizeof (int));
```

It should be noted that the memory reserved with malloc is controlled by the programmer, not the compiler, and it is he who must release it when he does not use it.

The free function must be used to free the dynamically allocated memory.

E.g.

```
free (p);
```