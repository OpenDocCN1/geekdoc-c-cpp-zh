allows each class in the inheritance tree to have its own constructor in order to initialize its attributes per requirements.

In the example in Listing 8.6, the `count` parameter of the constructor is assigned a value when instantiating the reference object `oref`. The syntax checker will give an error if the constructor's mandatory parameters aren't passed while instantiating the reference object. This ensures that the object is always instantiated properly.

Now, say we have a more advanced printer model that can print multiple copies along with the basic features provided so far. To create this printer, we'll inherit the `PRINTER_WITH_COUNTER` class and add additional functionality, as shown in Listing 8.7.

```
CLASS MULTI_COPY_PRINTER DEFINITION INHERITING FROM PRINTER_WITH_COUNTER.
PUBLIC SECTION.
DATA copies TYPE I.
METHODS set_copies IMPORTING copies TYPE I.
METHODS print REDEFINITION.
ENDCLASS.

CLASS MULTI_COPY_PRINTER IMPLEMENTATION.
METHOD set_copies.
Me->copies = copies.
ENDMETHOD.
METHOD print.
Do copies TIMES.
CALL METHOD SUPER->Print.
ENDDO.
ENDMETHOD.
ENDCLASS.

START-OF-SELECTION.
DATA oref TYPE REF TO MULTI_COPY_PRINTER.
CREATE OBJECT oref
EXPORTING
count = 0.
oref->set_copies( 5 ).
oref->print( ).
```

**Listing 8.7** Class Extended to Print Multiple Copies

In Listing 8.7, we defined the `MULTI_COPY_PRINTER` class, inheriting from `PRINTER_WITH_COUNTER`. In the `MULTI_COPY_PRINTER` class, we defined a method called