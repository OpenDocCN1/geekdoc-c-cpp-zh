# Class constructor

The *class constructor* is special method called just once for the whole class in one internal mode. A class constructor can have a maximum of one instance and one static constructor. A static constructor can't have any parameters, whereas the instance constructor can have only importing parameters.

By defining importing parameters for the instance constructor, we can ensure that the object is always initialized before any of its attributes or methods are accessed.

[Listing 8.6](#) shows the implementation of the constructor.

```
CLASS PRINTER_WITH_COUNTER DEFINITION INHERITING FROM PRINTER.
PUBLIC SECTION.
DATA counter TYPE I.
METHODS constructor IMPORTING count TYPE I.
METHODS print REDEFINITION.
ENDCLASS.

CLASS PRINTER_WITH_COUNTER IMPLEMENTATION.
METHOD constructor.
CALL METHOD super->constructor.
counter = count.
ENDMETHOD.
METHOD print.
counter = counter + 1.
CALL METHOD SUPER->PRINT.
ENDMETHOD.
ENDCLASS.

START-OF-SELECTION.
DATA oref TYPE REF TO PRINTER_WITH_COUNTER.
CREATE OBJECT oref
EXPORTING
count = 0.
```

**Listing 8.6** Class with Constructor

In Listing 8.6, the constructor method is defined in the definition part of the PRINTER_WITH_COUNTER class with one importing parameter, count. Because the PRINTER_WITH_COUNTER class is a subclass of the printer class, the superclass constructor must be called first in the implementation of the constructor method, even if there's no constructor defined in the superclass. This ensures that all of the superclass components in the inheritance tree are initialized properly. If a constructor is defined in the superclass, it won't be inherited by the subclass. This