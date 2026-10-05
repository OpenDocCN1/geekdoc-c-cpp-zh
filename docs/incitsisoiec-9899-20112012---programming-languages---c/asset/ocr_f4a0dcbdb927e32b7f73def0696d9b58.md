If both types are function types with parameter lists, the type of each parameter in the composite parameter type list is the composite type of the corresponding parameters.

These rules apply recursively to the types from which the two types are derived.

For an identifier with internal or external linkage declared in a scope in which a prior declaration of that is visible.¹56) if the prior declaration specifies internal or external linkage, the type of the identifier at the later declaration becomes the composite type.

Forward references: array declarations (6.7.6.2).

EXAMPLE Given the two file scope declarations:

```
int f(int (*)), double (*) [3]);
int f(char *), double (*) [3]);
```

The resulting composite type for the function is:

```
int f(char *), double (*) [3]);
```

# 6.2.8 Alignment of objects

Complete objects have alignment requirements which place restrictions on the addresses at objects of that type may be allocated. An alignment is an implementation-defined integer value representing the number of bytes between successive addresses at a given object can be allocated. An object type imposes an alignment requirement on every object of that type: stricter alignment can be requested using the _Alignas keyword.

A fundamental alignment is represented by an alignment less than or equal to the greatest alignment supported by the implementation in all contexts, which is equal to _Alignof(max_align_t).

An extended alignment is represented by an alignment greater than _Alignof(max_align_t). It is implementation-defined whether extended alignments are supported and the contexts in which they are supported. A type having an over-aligned type.¹57)

Alignments are represented as values of the size_t. Valid alignments include only those values returned by an _Alignof expression for fundamental types, plus an additional implementation-defined set of values, which may be empty. Every valid alignment value shall be a nonnegative integral power of two.

> 56) As specified in 6.2.1, the later declaration might hide the prior declaration.

> 57) Every over-aligned type is, or contains, a structure or union type with a member to which an extended alignment has been applied.