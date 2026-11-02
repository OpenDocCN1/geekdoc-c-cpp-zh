Swap was not defined in the package specification. It is not a basket operation but a local subprogram called by procedure Load.

# ### 3.4.1 Package Initialization

A program using our Bingo.Basket package should call the Load operation to initialize the global package variable The_Basket before drawing numbers from it. This explicit initialization is appropriate for this particular variable package as we will likely use this package to play multiple Bingo games. However, some situations require that initialization occur only once. For example, consider the following package that implements a serial number generator:

```
```ada
package Serial_Numbers is
    type Serial_Number is range 1000 .. Integer'Last;
    procedure Get_Next (Number : out Serial_Number);
end Serial_Numbers;
```
```

Calls to procedure Get_Next return the next available serial number. Because we do not want to repeat numbers, we have not included an operation to initialize the sequence. Instead, we set the initial serial number in the package body:

```
```ada
package body Serial_Numbers is

    Next_Number : Serial_Number := Serial_Number'First;

    procedure Get_Next (Number : out Serial_Number) is
    begin
        Number := Next_Number;
        Next_Number := Next_Number + 1;
    end Get_Next;

end Serial_Numbers;
```
```

The declaration of the global package variable Next_Number includes an assignment of an initial value. This value is assigned to the variable during elaboration of this package body. *Elaboration* is the runtime processing of declarations. Elaboration brings the item being declared into existence and then, if the declaration includes an initial value, assigns that value to the item.

When a variable package encapsulates a nontrivial data structure, initializing that data structure may require more than can be accomplished with assignments of initial values to its variables. We may, for example, need a loop to create an initial linked list. Package bodies may include an optional sequence of statements that are executed when the body is elaborated. This initialization