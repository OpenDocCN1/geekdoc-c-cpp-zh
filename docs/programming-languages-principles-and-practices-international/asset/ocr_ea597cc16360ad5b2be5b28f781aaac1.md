A Modula-2 DEFINITION MODULE contains only definitions or declarations, and only the declarations that appear in the DEFINITION MODULE are **exported**, that is, are usable by other modules. The incomplete type specification of type Complex in the DEFINITION MODULE is called an opaque type; the details of its declaration are hidden in an implementation module and are not usable by other modules. These features are all similar to those of Ada and ML.

A corresponding IMPLEMENTATION MODULE in Modula-2 for the DEFINITION MODULE is as follows:

```
```modula-2
IMPLEMENTATION MODULE ComplexNumbers;

FROM Storage IMPORT ALLOCATE;

TYPE Complex = POINTER TO ComplexRecord
     ComplexRecord = RECORD
          re, im: REAL;
     END;

PROCEDURE add (x,y: Complex): Complex;
VAR t: Complex;
BEGIN
   NEW(t);
   t^.re := x^.re + y^.re
   t^.im := x^.im + y^.im;
   RETURN t;
END add;

   ...

PROCEDURE makeComplex (x,y: REAL): Complex;
VAR t: Complex;
BEGIN
   NEW(t);
   t^.re := x;
   t^.im := y;
   RETURN t;
END makeComplex;

PROCEDURE realPart (z: Complex) : REAL;
BEGIN
   RETURN z^.re;
END realPart;

PROCEDURE imaginaryPart (z: Complex) : REAL;
BEGIN
   RETURN z^.im;
END imaginaryPart;

END ComplexNumbers.
```
```