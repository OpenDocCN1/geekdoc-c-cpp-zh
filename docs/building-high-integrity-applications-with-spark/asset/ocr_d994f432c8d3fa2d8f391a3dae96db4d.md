in Section 6.1. However, unlike runtime errors, it is up to the programmers to explicitly include assertions in their programs. Furthermore, assertions can be used to check whatever conditions the programmers deem appropriate.

An assertion policy of Ignore causes the compiler to remove the assertion checks so they will not be tested at runtime. In that case, failures of the assertions are not detected, probably causing other, less well-behaved failures. One of the main goals of SPARK is to allow proof that all assertions never fail.^4 In that case, the program can be compiled with an assertion policy of Ignore without being concerned about unexpected failures. In addition to increasing the reliability of the program, SPARK can improve its performance because the assertions consume resources, such as processor time, to check.

In the following subsections we describe how to specify assertions and give some hints about their use. Our approach is to show examples of increasing complexity and realism to give a feeling for how SPARK assertions work in practice.

# 6.2.1 *Preconditions*

Ada allows subprograms to be decorated with preconditions. A *precondition* is a logical expression (an expression with Boolean type) that must hold (evaluate to True) whenever the subprogram is called. Preconditions are specified using the Pre aspect. Because the expression used to define the precondition is arbitrary, it can be used to encode conditions of any complexity.

As an example, consider a package, Shapes, that does some geometric computations on two-dimensional shapes. All coordinates used by the package are in Cartesian form and constrained to a workspace in the range of −100 to 100 pixels in each dimension. An abbreviated specification of the package follows:

```
```ada
pragma SPARK_Mode(On);
package Shapes is

   subtype Coordinate_Type is Integer range -100 .. +100;
   subtype Radius_Type    is Coordinate_Type range 0 .. 10;

   type Circle is
      record
         Center_X : Coordinate_Type;
         Center_Y : Coordinate_Type;
         Radius   : Radius_Type;
      end record;
```
```