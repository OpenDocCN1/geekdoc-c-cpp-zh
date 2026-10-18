shared_ptr can also take responsibility for the lifetime of an array of objects. It overloads the constructor to permit an ordinary pointer to such an array. Again, there can be more than one shared_ptr attached to such an array of objects – in the previous example, there are two such shared pointers: sp_4 and sp_5. This time the output is as follows:

```
sp_4 count = 1
sp_4 = 4, 2, sp_5 count = 2

AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
```

Note that at first, sp_4 count is 1. Then all eight empty strings accessed via sp_4 are displayed. After that, sp_4 has been joined with sp_5, which causes the reference counter to be increased to 2, as did the next line. Finally, all AClass objects are deleted, as manifested by messages from the AClass destructor. This happens since all shared_ptr objects went out of scope and have been deleted, which entailed disposal of all their held objects. These are two AClass objects and eight AClass objects from the array.

shared_ptr frequently used function members:

| Member | Description |
|---|---|
| `shared_ptr` | Class default and parametric constructors |
| `operator *` | Pointer dereferencing the held object |
| `operator ->` | Pointer access to the held object |
| `operator bool` | Checks whether there is an associated object (or empty) |
| `get` | Return pointer to the object |
| `reset` | Gets a new object; deletes the old one |
| `use_count` | Returns the number of shared `ptr(s)` attached to the same object |