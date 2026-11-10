When you use `CASTING`, a data object of a different type can be assigned to the field symbol. Casting allows you to assign a data object to the field symbol that is not compatible with the field symbol.

**Listing 16.16** shows sample code in which a field of type `C` is assigned to the field symbol, which is of type `D`. Once the data object is assigned, the contents of the data object will be interpreted as type `D`.

```
DATA text(8) TYPE c VALUE '20111201'.
FIELD-SYMBOLS <fs> TYPE sy-datum.
ASSIGN text TO <fs> CASTING.
WRITE <fs>.
```

**Listing 16.16** Casting

Casting can be performed implicitly or explicitly. If the field symbol is fully typed or is typed generically using one of the built-in ABAP types (c, n, p, or x), then `CASTING` can be used with the `ASSIGN` statement, which performs an implicit casting to cast the assigned memory to the type of the field symbol.

If the field symbol is typed generically, then you can perform an explicit casting by specifying the data type in the `ASSIGN` statement as follows:

```
ASSIGN dobj TO <fs> CASTING [TYPE data_type|LIKE dobj].
```

After the `CASTING` addition, you can specify the data type or a data object. The casting will be performed as per the specified type. Your specified type should be compatible with the generic type of the field symbol, and you shouldn't perform an explicit typing for a fully typed field symbol. Casting allows you to interpret data differently per type conversions.

In this section, we discussed the use of field symbols in dynamic programming. In the next section, we'll look at using data references to point to a data object in memory.

# 16.2 Data References

Similar to object references, a *data reference* points to a data object in memory. Data references can be used as alternate access references to existing data objects, similarly to field symbols. However, with data references, it's possible to define