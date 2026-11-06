# Overloaded Assignment Operator

Line 18 of **Fig. 10.10** declares the overloaded assignment operator function for the class. When the compiler sees the expression `integers1 = integers2` in line 44 of **Fig. 10.9**, the compiler invokes member function `operator=` with the call

```
```cpp
integers1.operator=(integers2)
```
```

Member function `operator=`’s implementation (**Fig. 10.11**, lines 37–53) tests for **self-assignment** (line 38) in which an `Array` object is being assigned to itself. When `this` is equal to the `right` operand’s address, a *self-assignment* is being attempted, so the assignment is skipped (i.e., the object already is itself; in a moment we’ll see why self-assignment is dangerous). If it isn’t a self-assignment, then the function determines whether the sizes of the two `Array`s are identical (line 41); in that case, the original array of integers in the left-side `Array` object is *not* reallocated. Otherwise, `operator=` uses `delete[]` (line 42) to release the memory originally allocated to the target `Array`, copies the `size` of the source `Array` to the `size` of the target `Array` (line 43), uses `new` to allocate the memory for the target `Array` and places the pointer returned by `new` into the `Array`’s `ptr` member (line 44). Then the `for` statement in lines 47–49 copies the elements from