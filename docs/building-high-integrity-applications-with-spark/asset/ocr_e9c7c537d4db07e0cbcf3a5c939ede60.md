The range of each type is specified by a smallest and largest value, not by some storage unit size such as byte or word. Because they are different types, a comparison of Apples and Oranges is illegal. Of course, should you really want to combine apples and oranges in an expression, you can use explicit type conversions as in

```
```
Fruit := Big_Range (Apples) + Big_Range (Oranges);
```
```

Operations available for signed integers include +, -, *, /, **, abs, rem, and mod. The rem (remainder on division) and mod (mathematical modulo) operators return the same result when both of their operands are positive. Should one of your operands be negative, you should consult the formal definitions of these two similar operators given in section 4.5.5 of the ARM (2012). The attributes 'First, 'Last, 'Succ, 'Pred, and 'Image discussed for enumeration values are also available for signed integers.

To do input and output of our own integer types, we need to instantiate a package from the generic integer I/O package available in the Ada library. Here are the instantiations for the three integer types we defined:

```
```
package Pome.IO is new Ada.Text_IO.Integer_IO (Pome);
package Citrus.IO is new Ada.Text_IO.Integer_IO (Citrus);
package Big_IO is new Ada.Text_IO.Integer_IO (Big_Range);
```
```

**Modular Integers.** Modular integer types are unsigned integer types that use modular arithmetic. The value of a modular integer variable wraps around after reaching an upper limit. To define a modular integer type, we need only specify a modulus. Here are some modular integer type definitions and variable declaration:

```
```
type Digit   is mod 10;      -- range is from 0 to 9
type Byte    is mod 256;     -- range is from 0 to 255
type Nybble  is mod 16;      -- range is from 0 to 15
type Word    is mod 2**32;   -- range is from 0 to 4,294,967,295
```
```

```
```
Value : Nybble;
```
```

The following assignment statement illustrates the modular nature of this type:

```
```
Value := 12 + 8;    -- Value is assigned 4
```
```

In addition to the usual arithmetic operators, the logical operators and, or, xor, and not are available for modular integer types. These operators treat the values as bit patterns. The result of the not operator for a modular type is defined as the difference between the high bound of the type and the value of