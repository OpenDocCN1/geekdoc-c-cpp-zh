```
procedure Display_Digit ( Digit : in Digit_Type)
  with
    Global => (Output => LED_State);

end LED_Display;
```

The Abstract_State aspect defining the abstract state LED_State has more options than those you saw in Section 4.3.8 Procedure Display_Digit references this abstract state in its Global aspect.

The declaration of LED_State includes the option External, which tells us that the actual state is maintained in hardware devices and/or other software subsystems that are external to our SPARK program. Finally, the two external properties Async_Readers and Effective_Writes are given for this external state object. These are the same properties we used with volatile variables in the previous section. Like a volatile variable, if none of the four properties is specified, all four properties are assumed to be true. And, as is the case here, if one or more properties are defined, the undefined properties are assumed to be false.

Here is the body of package LED_Display where we refine the abstract state LED_State, define the external variable that connects us to the hardware, and implement the procedure Display_Digit :

```
with System.Storage_Elements;
package body Led_Display
  with SPARK_Mode => On,
    Refined_State => (LED_State => Value)
is
  type Octet is mod 2 ** 8;

  Value : Octet
    with
    Size => 8, -- Use exactly 8 bits for this variable
    Volatile => True,
    Async_Readers => True,
    Effective_Writes => True,
    Address => System.Storage_Elements.To_Address(16#FFFF0000#);

  -- Segments 'a' through 'g' are in order from least to most significant bit .
  -- Active high.
  Patterns : constant array (Digit_Type) of Octet :=
    (2#0011.1111#, 2#0000.0110#, 2#0101.1011#, 2#0100.1111#,
     2#0110.0110#, 2#0110.1101#, 2#0111.1101#, 2#0000.0111#,
     2#0111.1111#, 2#0110.0111#);
```