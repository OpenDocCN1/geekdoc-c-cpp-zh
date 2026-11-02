It is not necessary to use 'Old here because in this case N is an in parameter that the function cannot change.

# Package Initial Conditions

As we describe in Section 3.4.1, when a package is elaborated, certain initialization activities can occur. Global variables in the package specification or body that have initialization expressions are given their initial values. Also, the package body can have a sequence of statements used to perform more complex package-wide initializations. The Initial_Condition aspect can be used on a package specification to assert a condition that is true after the package has been fully elaborated. Conceptually the aspect is like a kind of package-wide postcondition.

Typically, Initial_Condition makes sense in cases where a variable package has an abstract state that it initializes, as described in Section 4.3. The initial condition can then capture information about the result of that initialization. The SPARK tools generate a verification condition to show that the package's elaboration does indeed initialize the internal state as specified.

As an example, consider again the Datebook package discussed in Section 4.3. Here we show an abbreviated specification that includes a function returning the number of events in the datebook. For brevity, the other subprograms in the package are not shown.

```
with Dates;
package Datebook
    with
        Abstract_State     => State,
        Initializes         => State,
        Initial_Condition  => Number_Of_Events = 0
is
    function Number_Of_Events return Natural
        with
            Global => (Input => State);
end Datebook;
```

If the Initial_Condition aspect is used, it must appear after the Abstract_State and Initializes aspects, if they are present. It can also only use visible variables and subprograms. In the preceding example, the package initial condition asserts that after elaboration, the number of events in the datebook is zero. This is an intuitive expectation, now formally specified and checked by the SPARK tools.

Notice that function Number_Of_Events is declared after it is used in the Initial_Condition aspect of package Datebook. This order violates the scope