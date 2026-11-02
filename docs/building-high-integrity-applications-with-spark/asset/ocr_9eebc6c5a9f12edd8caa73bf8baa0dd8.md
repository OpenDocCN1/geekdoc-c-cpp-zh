rules defined on page 30. Our Datebook example shows one of the few places where Ada allows use of as yet undeclared entities – assertions can reference names that are declared later in the same declarative part. We will make frequent use of this exception to Ada’s scope rules.

# ### 6.2.3 *Private Information*

Consider the type package Shapes on page 164. In many applications it would be more appropriate to keep the representation of circles hidden by making type Circle private. However, by moving the details of Circle into the private section, we find another problem – the precondition for function Inside_Circle no longer compiles. The precondition of a public subprogram cannot make use of hidden (private) information.

To work around this issue, we can introduce a public function, In_Bounds, that tests if a Circle is entirely inside the workspace. The following package Shapes2 shows these changes:

```
```ada
pragma SPARK_Mode(On);
package Shapes2 is
   subtype Coordinate_Type is Integer range -100 .. +100;
   subtype Radius_Type is Coordinate_Type range 0 .. 10;
   type Circle is private;

   -- Return True if X, Y are inside circle C.
   function Inside_Circle (X, Y : in Coordinate_Type;
                           C    : in Circle ) return Boolean
     with Pre => In_Bounds (C);

   -- Return True if C is entirely in the workspace.
   function In_Bounds (C : in Circle ) return Boolean;

private
   type Circle is
     record
        Center_X : Coordinate_Type;
        Center_Y : Coordinate_Type;
        Radius   : Radius_Type;
     end record;
end Shapes2;
```
```

The precondition on Inside_Circle has been rewritten to make use of the new function. The body of function In_Bounds is written in the package body