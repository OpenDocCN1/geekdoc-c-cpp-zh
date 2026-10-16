Here, **x** really is a copy of **v**, but if **T** is a reference type, **y** is a reference to **v**:

```
void user()
{
int val = 7;
f(val); // call f<int&>(): the ++v in f() will increment val
f(7); // call f<int>(): the ++v in f will increment a local copy
}
```

In both calls, ++x will increment a local copy.

# Sign Modification (§iso.20.9.7.3)

**make_signed<X>** Remove any (explicit or implied) **unsigned** modifier and add **signed**; X must be an integral type (except **bool** or an enumeration)

**make_unsigned<X>** Remove any (explicit or implied) **signed** modifier and add **unsigned**; X must be an integral type (except **bool** or an enumeration)

For built-in arrays, we sometimes want to get the element type or to remove a dimension: **Array Modification (§iso.20.9.7.4)**

**remove_extent<X>  remove_all_extents<X>**

If X is an array type, the element type; otherwise X
If X is an array type, the base type (after removing all array modifiers); otherwise X

For example:

```
int a[10][20];
Remove_extent<decltype(a)> a10; // an array[10]
Remove_all_extents<decltype(a)> i; // an int
```

We can make a pointer type pointing to an arbitrary type, or find the pointed-to type:

# Pointer Modification (§iso.20.9.7.5)

**remove_pointer<X>** If X is a pointer type, the pointed-to type; otherwise X
**add_pointer<X>  remove_reference<X>::type***

For example:

```
template<typename T> void f(T x)
{
Add_pointer<T> p = new Remove_reference<T>{};
T* p = new T{}; // would not work if T is a reference
// ...
}
```

When dealing with memory at the lowest levels of a system, we must sometimes consider alignment (§6.2.9):

# Alignments (§iso.20.9.7.6)

**aligned_storage<n,a>** A POD type with size of at least **n** and whose alignment is a divisor of **a**