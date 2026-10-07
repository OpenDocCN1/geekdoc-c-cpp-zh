It is also an error to dereference a pointer after deleting any of its aliases.

```
third = second;
delete second;
cout << *third << endl;  // Error, third is dangling
```

The above code will probably print out a 2, actually, since third still points to the same memory location and those locations have not been changed yet. They soon will be however. The following may produce something very different:

```
third = second;
delete second;
int *fourth = new int;
*fourth = 4;
// Error, third is dangling
```

On some systems 4 will be produced, since the storage that *second (and *third) occupied previous to the delete may be reallocated to *fourth.

# Losing Cells

It is an error to give a new value to a pointer that references a free cell unless you either first:

+   - create an alias of the cell, or
- delete the cell

This is an error that is not caught by the system. It simply results in free store cells that cannot be recycled for later use in the program. A long running program allocates but does not free cells will possibly crash when an attempt to allocate a cell cannot be fulfilled.

```
second = third; // Error, second already references the free store
```