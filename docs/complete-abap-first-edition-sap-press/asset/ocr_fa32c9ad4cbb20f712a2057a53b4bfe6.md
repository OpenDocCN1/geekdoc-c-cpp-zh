When you define a table with a non-unique key, you can have multiple records with the same values for the key and no restrictions apply. You should choose the key carefully based on the data being processed to avoid data inconsistency.

When using the TABLE KEY addition with the READ statement, the system performs a binary search to identify the matching row.

The syntax for declaring a sorted table is as follows:

```
DATA internaltable_name TYPE SORTED TABLE OF structure_\nreference WITH UNIQUE [or NON-UNIQUE] KEY key_fields.
```

To define a sorted table, use the SORTED TABLE OF addition. It's mandatory to define the key of the table during a declaration. The key is defined using the WITH UNIQUE KEY or WITH NON-UNIQUE KEY addition to define a unique or non-unique key, respectively. The key of the sorted table can consist of a single field or multiple fields. If the key contains multiple fields, each field is listed after the WITH UNIQUE (or NON-UNIQUE) KEY addition, separated by a space.

For example, the following statement defines a sorted table IT_SFLIGHT with line type TY_SFLIGHT consisting of unique key CARRID and CONNID (assuming CARRID and CONNID are components of structure type TY_SFLIGHT):

```
DATA it_sflight TYPE SORTED TABLE OF ty_\nsflight WITH UNIQUE KEY carrid connid.
```

In addition, the following statement defines a sorted table IT_SFLIGHT with non-unique key CARRID and CONNID:

```
DATA it_sflight TYPE SORTED TABLE OF ty_sflight WITH NON-\nUNIQUE KEY carrid connid.
```

# Hashed Tables

Unlike standard and sorted tables, hashed tables do not have a row index. They are managed using a hash algorithm. Because there is no row index, you can’t perform any index operations and can only read the individual rows by the key. Hashed tables support only unique keys, and defining the key is mandatory while declaring the internal table.

When using the TABLE KEY addition with the READ statement, the system doesn’t compare the contents of the key fields manually to identify the matching row. Instead, the system uses hash functions to identify the matching row.