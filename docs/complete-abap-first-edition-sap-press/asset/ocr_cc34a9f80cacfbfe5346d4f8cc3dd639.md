```
flight TYPE ty_sflight,
END OF ty_trip.
```

# Listing 5.3  Nested Structure Type

In Listing 5.3, we've defined structure type `TY_SFLIGHT` referring to the transparent table `SFLIGHT`. We've also defined a nested structure type `TY_TRIP` that consists of the component `NAME` and the structure type `FLIGHT`.

Listing 5.4 shows an example of defining the structure as a data object using the `DATA` keyword. The syntax is similar to the `TYPES` keyword.

```
*To define a structure as a data object, simply use the
*DATA keyword instead of the TYPES keyword.
DATA : BEGIN OF st_sflight,
             CARRID TYPE S_CARR_ID,
             CONNID TYPE S_CONN_ID,
             FLDATE TYPE S_DATE,
         END OF st_sflight.
*You can also create a structure by referring to the
*database table to match the table row type.
DATA st_sflight1 TYPE sflight.
```

# Listing 5.4  Defining Data Object as Structure

In Listing 5.4, structure `ST_SFLIGHT` consists of three components, `CARRID`, `CONNID`, and `FLDATE`, whereas structure `ST_SFLIGHT1` contains all the fields of the ABAP Data Dictionary table `SFLIGHT`.

# 5.1.3  Global Structures

Structures types can be defined globally to have visibility across programs. Global structure types are also used to define the parameter interface for function modules or methods and also can be used to define screen elements for general screens. You'll learn more about function modules and methods in Chapter 7 and more about screen programming in Chapter 12.

Global structures types are created in ABAP Data Dictionary (Transaction SE11). Follow these steps to create a global structure:

+   1. Enter Transaction SE11.
+   2. Select the DATA TYPE radio button on the ABAP Data Dictionary initial screen. Enter the name of the structure. The name should be in a customer namespace, starting with Y or Z. Click the CREATE button (Figure 5.6).