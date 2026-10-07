Interestingly, something will be printed most likely. If this happens to have a value that looks to the running program like a valid pointer we will get the contents of a few memory locations interpreted as an int, independently of what they actually contain.

It is far worse to say:

```
*third = 3;      // Serious error - changing a random memory location
```

A pointer can get a valid value by assigning it NULL, or another pointer known to be valid. You can assign it the result of calling operator new. You can also get a valid pointer using the "address of" operator &.

```
third = NULL;
third = second;    // second was valid, so third is also valid
third = new int;     // OK, but see Losing Cells, below
third = &fixed;     // Third points to fixed. *third IS fixed (alias)
```

# Aliasing Problems

Having more than one name for the same cell can add flexibility to our programs, but there are some dangers. For example, after executing:

```
third = new int;
```

we will eventually want to execute:

```
delete third;
```

to reclaim the storage that third occupies. However it is an error to delete a cell not allocated with new:

```
third = &fixed;     // Error, third does not point to the free store
delete third;
```