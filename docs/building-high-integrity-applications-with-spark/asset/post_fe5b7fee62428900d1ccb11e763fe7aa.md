
Write an instantiation of the generic procedure Tally given on page 63 that tallies up the number of floating point numbers in an array that are nearly equal to a given number. Make use of the function Nearly_Equal you wrote for Exercise 2.19.

2.26 Given the following array types that define an unconstrained array of Cartesian points (defined on page 58) indexed by Natural integers, an array variable that holds 100 points, and a variable that holds a count of points:

```ada
    type    Point_Array is array (Natural range <>) of Point;
    subtype Point_List  is Point_Array (101 .. 200);
```

```ada
    My_Points  : Point_List ;
    Point_Tally : Natural;
```

- a. Write an instantiation of the generic procedure Tally given on page 63 that tallies up the number of points in an array that are not further from the origin than a given point. You may use the function "<=" defined on page 58.
- b. Write a call to the procedure you instantiated to tally the number of points in the array My_Points that are on or inside a circle of radius 1.0. Put the result into the variable Point_Tally. You may either declare a variable to hold a pattern point or use a record aggregate in your procedure call.

## 3 Programming in the Large

DeRemer and Kron (1975) distinguished the activities of writing large programs from that of writing small programs. They considered large programs to be systems built from many small programs (modules), usually written by different people. It is common today to separate the features of a programming language along the same lines. In Chapter 2, we presented the aspects of Ada required to write the most basic programs. In this chapter, we discuss some of Ada's features that support the development of large programs.

To facilitate the construction of large programs, Ada makes use of programming units. An Ada program consists of a main subprogram that uses services provided by library units. A *library unit* is a unit of Ada code that we may compile separately. Library units are often called *compilation units*. We have already made use of many predefined library units in our examples. The *with clause* provides access to a library unit. The *use clause* provides direct visibility to the public declarations within a library unit so we do not have to prefix them with the name of the library unit.

A library unit is a subprogram (a procedure or function), package, or generic unit. The main subprogram is itself a library unit. Subprograms, packages, and generic units that are nested within another programming unit are not library units; they must be compiled with the programming unit in which they are nested. Generally, we use a compiler and linker to create an executable from a collection of library units. Library units also play a role in mixing SPARK and non-SPARK code in a single program – a topic we discuss in Chapter 7. In the following sections, we will introduce you to the package and to generic units.

Encapsulation and information hiding are the cornerstones of programming in the large. Both concepts deal with handling complexity. There are two aspects of encapsulation: the combining of related resources and the separation of specification from implementation. In object-oriented design and programming, we use encapsulation to combine data and methods into a single entity called a *class*. Encapsulation also allows us to separate what methods a class supplies for manipulating the data without revealing how those methods are implemented.

The *package* is Ada's construct for encapsulation. The package supports abstract data types, separate compilation, and reuse. We write packages in two parts: the package declaration and the package body. The declaration specifies the resources the package can supply to the rest of the program. These resources may include types, subtypes, constants, variables, and subprograms. The package body provides the implementation of the subprograms defined in the package declaration.

Information hiding is related to but different than encapsulation. Encapsulation puts things into a box. Whether that box is opaque or clear determines whether the information is hidden or not.

Information hiding is what we do in the design process when we hide the decisions that are most likely to change. We hide information to protect the other portions of our design from changes to that decision. Modern programming languages provide mechanisms to ensure that details of a design are not accessible to portions of our program that do not need those details.

Information hiding ensures that the users of a class are not affected when we make a change to the implementation of that class. Suppose, for example, our program makes use of a sorted list. If we were to change the implementation of that list from one based on linked lists to one based on arrays, information hiding ensures that this change has no effect on the parts of our program that use a sorted list.

The major Ada construct for information hiding is the *private type*, which is introduced in Section 3.3.2. Private subprograms and private child packages are additional Ada constructs for restricting access to design details.

Although there are many different ways to define and use packages, we can usually place packages into one of four categories: definition packages, utility packages, type packages, and variable packages. This classification scheme is neither strict nor inclusive. In the following sections we will look at an example from each category.

### 3.1 Definition Packages

A definition package groups together related constants and types. Such packages are useful when the same types must be used in several different programs or by different programmers working on different parts of one large program.

Here is an example of a definition package:

```ada
with Ada.Numerics;
package Common_Units is

   type Degrees is digits 18 range 0.0 .. 360.0;
   type Radians is digits 18 range 0.0 .. 2.0 * Ada.Numerics.Pi;

   type Volts is delta 1.0 / 2.0**12 range -45_000.0 .. 45_000.0;
   type Amps is delta 1.0 / 2.0**16 range -1_000.0 .. 1_000.0;
   type Ohms is delta 0.125 range 0.0 .. 1.0E8;

   type Light_Years is digits 12 range 0.0 .. 20.0E9;

   subtype Percent is Integer range 0 .. 100;
end Common_Units;
```

This package defines six types and one subtype. It uses the value of π from the Ada library definition package Ada.Numerics. Because definition packages have no subprograms, there is nothing to implement. In fact, the compiler will give us an error should we try to compile a body for it.

Here is a short program that uses our definition package:

```ada
with Common_Units; use type Common_Units.Ohms;
with Ada.Text_IO;  use Ada.Text_IO;
procedure Ohms_Law is

   package Ohm_IO is new Fixed_IO (Common_Units.Ohms);
   package Amp_IO is new Fixed_IO (Common_Units.Amps);
   package Volt_IO is new Fixed_IO (Common_Units.Volts);

   A  : Common_Units.Amps;
   R1 : Common_Units.Ohms;
   R2 : Common_Units.Ohms;
   V  : Common_Units.Volts;
begin
   Put_Line ("Enter current and two resistances ");
   Amp_IO.Get (A);
   Ohm_IO.Get (R1);
   Ohm_IO.Get (R2);
   V := A * (R1 + R2);
   Put ("The voltage drop over the two resistors is ");
   Volt_IO.Put (Item => V,
                Fore => 1,
                Aft  => 2,
                Exp  => 0);
   Put_Line (" volts ");
end Ohms_Law;
```

This program also illustrates the *use type clause*. When we declare a type, we define its domain and a set of operations. As type Ohms is a fixed point type, the operations include all of the standard arithmetic operators. To add two resistance values, we use the plus operator. However, because this operator is defined in package Common_Units, we must either prefix the plus operator with the package name or include a use clause to access the operator directly. A use clause makes all of the resources in the named package available without prefixing. A use type clause is more specific; it allows us to use operators¹ of the given type without prefixing.

### 3.2 Utility Packages

A utility package groups together the constants, types, subtypes, and subprograms necessary to provide some particular service. The library package Ada.Numerics.Elementary_Functions is a utility package that includes twenty-nine mathematical functions such as square root, trigonometric functions, and logarithms for Float values. There is also a generic version of this mathematical package that may be instantiated for any floating point type.

Here is the declaration of a utility package that provides three operations for control over output displayed on a screen:

```ada
package Display_Control is

   procedure Bold_On;
   -- Everything sent to the screen after this procedure
   -- is called will be displayed in bold characters

   procedure Blink_On;
   -- Everything sent to the screen after this procedure
   -- is called will be blinking

   procedure Normal;
   -- Everything sent to the screen after this procedure
   -- is called will be displayed normally

end Display_Control;
```
