only be validated at runtime, because the type of the source reference variable will be known only at runtime.

For this assignment, the syntax checker can't validate statically and will throw a syntax error if the `=` assignment operator or the `MOVE` statement is used for the assignment.

For such assignments, we have to use the `?=` casting operator or the `MOVE ?TO` statement. An upcast is performed if the source reference variable is of a generic type and the target reference variable is fully typed.

Listing 16.24 shows an example of a downcast.

```
```abap
TYPES: BEGIN OF ty_mara,
         matnr TYPE matnr,
         mtart TYPE mtart,
       END OF ty_mara.
DATA : s_mara TYPE ty_mara,
       dref TYPE REF TO ty_mara, " Fully Typed
       dref1 TYPE REF TO DATA. " Generic type
CREATE DATA dref.
GET REFERENCE OF s_mara INTO dref1.
TRY.
  dref ?= dref1. " Down Cast
CATCH cx_sy_move_cast_error.
ENDTRY.
```
```

**Listing 16.24** Downcast

# 16.3  Runtime Type Services

ABAP *Runtime Type Services* (RTTS) is an object-oriented framework that consists of the following elements:

+   - **Runtime Type Information (RTTI)**  
+     Using RTTI, we can determine the type information about data objects or instances of classes at runtime during program execution.
+   - **Runtime Type Creation (RTTC)**  
+     RTTC allows us to define new data types during the program execution.

The RTTS framework implements a hierarchy of classes, as shown in Figure 16.4, via which we can determine the type information of data objects and define new