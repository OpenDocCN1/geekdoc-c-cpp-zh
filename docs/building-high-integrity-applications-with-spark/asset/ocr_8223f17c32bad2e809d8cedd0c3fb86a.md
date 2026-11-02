the operand. For a modulus that is a power of two, this corresponds to a bit-wise complement of the binary representation of the value of the operand.

You may recall using the logical operators and bit masks in your assembly language, C, C++, or Java programs to clear, set, and toggle individual bits in a computer’s memory. Thus, you might think that Ada’s modular types provide the mechanism for Ada programs to manipulate individual bits. Ada provides a much higher level approach to bit manipulation. This topic is beyond the scope of this work. See McCormick, Singhoff, and Hugues (2011) for a full discussion of low level programming with Ada.

Again, we must instantiate packages to do input and output with the types we define. You can find the details on these packages and the get and put procedures in section A.10.8 of the ARM (2012). Here are the instantiations for our four modular types:

```
```ada
package Digit_IO  is new Ada.Text_IO.Modular_IO (Digit);
package Byte_IO   is new Ada.Text_IO.Modular_IO (Byte);
package Nibble_IO is new Ada.Text_IO.Modular_IO (Nibble);
package Word_IO   is new Ada.Text_IO.Modular_IO (Word);
```
```

# ### 2.3.3 Subtypes

By defining our own types, we make our programs easier to read and safer from type errors and allow range checking by the SPARK tools. In some cases, values with different constraints are related so closely that using them together in expressions is common and desired. Although explicit type conversion allows us to write such expressions, Ada provides a better solution – the subtype. Subtypes allow us to create a set of values that is a subset of the domain of some existing type. Subtypes inherit the operations from their base type. Subtypes are compatible with the type from which they were derived and all other subtypes derived from that type. A subset is defined by specifying an existing type and an optional constraint. Let us look at some examples:

```
```ada
subtype Uppercase is Character range 'A' .. 'Z';
subtype Negative  is Integer   range Integer'First .. -1;

type    Day_Type is (Monday, Tuesday, Wednesday, Thursday,
                     Friday, Saturday, Sunday);
subtype Weekday is Day_Type range Monday .. Friday;
subtype Weekend is Day_Type range Saturday .. Sunday;

type    Pounds      is digits 6 range 0.0 .. 1.0E+06;
subtype UPS_Weight  is Pounds  range 1.0 .. 100.0;
```
```