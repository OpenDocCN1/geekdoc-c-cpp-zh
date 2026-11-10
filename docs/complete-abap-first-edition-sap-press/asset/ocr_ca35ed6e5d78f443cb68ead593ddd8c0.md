```
WITH KEY (or WITH TABLE KEY) key_name COMPONENTS comp1...
```

To read an internal table using the secondary key, specify the name of the secondary key in the READ statement, as shown in Listing 5.10.

```
*Using the secondary key by_airline to read the internal table.
READ TABLE it_sflight INTO wa_sflight WITH TABLE KEY by_airline
COMPONENTS carrid = 'AA'.
```

# **Listing 5.10** Reading Internal Table Using Secondary Key

In Listing 5.10, assuming the internal table IT_SFLIGHT is defined with a secondary key BY_AIRLINE, we're using the READ statement and specifying the name of the secondary key to read the record of the table using the secondary key.

In Listing 5.11, we've defined an internal table IT_SFLIGHT as a sorted table using the pseudo-component table_line as the unique primary key. Two secondary keys, BY_AIRLINE and BY_FLIGHT, are also defined for the table. The secondary key BY_AIRLINE is defined as a non-unique sorted key, and the secondary key BY_FLIGHT is defined as a unique hashed key.

```
DATA it_sflight TYPE SORTED TABLE OF ty_sflight
      WITH UNIQUE KEY table_line
      WITH NON-UNIQUE SORTED KEY by_airline COMPONENTS carrid
      WITH UNIQUE HASHED KEY by_flight COMPONENTS carrid connid.
```

# **Listing 5.11** Secondary Keys for Sorted Table

Listing 5.12 shows an example to define secondary keys for hashed table.

```
DATA it_sflight TYPE HASHED TABLE OF ty_sflight
      WITH UNIQUE KEY table_line
      WITH NON-UNIQUE SORTED KEY by_airline COMPONENTS carrid
      WITH UNIQUE HASHED KEY by_flight COMPONENTS carrid connid.
```

# **Listing 5.12** Secondary Keys for Hashed Table

In Listing 5.12, we defined an internal table IT_SFLIGHT as a hashed table using the pseudo-component table_line as the unique primary key. Two secondary keys, BY_AIRLINE and BY_FLIGHT, are defined for the table. The secondary key BY_AIRLINE is defined as a non-unique sorted key, and the secondary key BY_FLIGHT is defined as a unique hashed key.

Before secondary keys were available, the only way to have the flexibility to read a table by any key while ensuring performance was to sort a standard table by the key and read it using the BINARY search addition.