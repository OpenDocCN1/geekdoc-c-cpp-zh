Global variables used by a subprogram behave similarly to parameters where the actual argument is fixed. However, it is not necessary in the data dependency contract to specify the types of the global variables. To be used in the contract, the variables must be visible at that point in the program. Thus, their types are available from their declarations elsewhere. In the preceding example, the global variables are declared inside the specification of package Raster_Graphics.

One important rule is that the variables mentioned in the data dependency contract have to be entire objects. For example, it is not permitted to use a single array element or record component. The variable must be the entire array or record even if the subprogram accesses only one component of the composite entity.

SPARK also requires that functions only read from global data. Thus, the modes Output and In_Out are illegal for functions. This is consistent with SPARK's restriction that functions have only *in* parameters. It is necessary to ensure that the unspecified evaluation order of subexpressions remains deterministic.

Consider, for example, an assignment statement such as

```
```
X := F(A) + F(B);
```
```

If F were allowed to output to a global variable, the final result stored in that variable would depend on the order in which the operands to + are evaluated. However, that order is unspecified by the language. To ensure the program always produces well-defined, predictable results, outputs cannot be allowed to depend on such unspecified ordering. The concern is eliminated by forbidding functions from having side effects such as writing to global data. This problem does not arise in the case of procedures because each procedure is called in its own statement, and the order in which statements execute is specified.

Procedure Draw_Line described earlier has two ordinary parameters and makes use of three global variables. One might wonder why some or all of those global variables were not declared as parameters instead. Doing so would be considered better style in the eyes of many developers.

There are, however, at least two cases in which the use of global data is reasonable. Perhaps the most important use of global data is to hold the internal state of a variable package. We used this approach with the Bingo basket package in Section 3.4. We discuss the SPARK aspects for managing internal state in Section 4.3.

Global data is also useful when a nested subprogram accesses the local variables or parameters of an enclosing subprogram. To demonstrate this, consider the following abbreviated body of package Raster_Graphics. For now we will