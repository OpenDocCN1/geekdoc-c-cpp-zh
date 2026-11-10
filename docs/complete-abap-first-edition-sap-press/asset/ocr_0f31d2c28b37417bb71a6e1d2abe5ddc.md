```
```text
flight type ty_sflight.
END OF ty_trip.

DATA : st_sflight TYPE ty_sflight,
       st_trip TYPE ty_trip.

*Addressing to the field of a structure type
DATA v_connid TYPE ty_sflight-connid.

*Accessing field of a structure data object
st_sflight-carrid = 'AA'.
st_sflight-connid = '04'.
WRITE st_sflight-connid.

*Accessing field of a nested structure
st_trip-flight-carrid = 'AB'.
```
```

**Listing 5-5** Accessing Fields of Structure

# 5.1.5 Use Cases

Structures should be used in the following cases:

+   - Use structures to process multiple fields of data. For example, when you want to process a record, you can define a structure with the fields of the record as components and process the record as a single entity.
+   - Group related fields into a structure if you need to perform certain actions on the fields together. It’s easy to clear the data in all the fields of a structure at once instead of individually clearing the data for each field.
+   
+     For example, if you have a structure `ST_SFLIGHT` with all the components of the ABAP Data Dictionary table `SFLIGHT`, you can clear a record easily by using the statement `CLEAR ST_SFLIGHT` rather than using the `CLEAR` statement for each individual field.
+   - Even though it’s possible to select data from a database table row into individual fields, it’s always recommended to use structures when processing data from database tables.
+   - Structure types also help you keep the parameter interface (signature) of a procedure (such as function module or method) simple by grouping relevant fields into one structure, as opposed to maintaining all fields individually in the interface.