# 5.2　Internal Tables

Internal tables are dynamic data objects that can store multiple rows of data with a common row type. In fact, internal tables are the only data objects that can store multiple rows of data at a time. We use internal tables when we need to work with mass data. Internal tables can be compared to two-dimensional arrays.

Working with internal tables is a bit different from other data objects. In this section, we'll look at how to define, store, and access data with internal tables. We'll discuss how to define internal types and the different types of internal tables available. We'll then provide steps for working with internal tables before discussing the use of control break statements.

# 5.2.1　Defining Internal Tables

Listing 5.6 shows the basic syntax for declaring an internal table. Here, the data object `IT_SFLIGHT` is declared as an internal table with the line type as `TY_SFLIGHT`. The line type of a table specifies the fields that make up a row. The `TABLE OF` addition to the type specification defines an internal table.

```
TYPES : BEGIN OF ty_s_flight.
        CARRID TYPE S_CARR_ID,
        CONNID TYPE S_CONN_ID,
        FLDATE TYPE S_DATE,
       END OF ty_s_flight.
DATA : it_sflight TYPE TABLE OF ty_sflight.
```

**Listing 5.6** Declaring Internal Table

Because an internal table consists of multiple rows, you can't work with the data of an individual row directly. To process the data from an internal table, you need a structure data object, called the work area. The *work area* of an internal table is a structure that can store one record at a time and has the same line type as the internal table. This allows you to read an individual row from an internal table into the work area and process it.

Listing 5.7 shows the work area `wa_sflight` declaration, referring to the same line type as the internal table `IT_SFLIGHT`.

```
TYPES : BEGIN OF ty_s_flight.
        CARRID TYPE S_CARR_ID,
        CONNID TYPE S_CONN_ID,
```