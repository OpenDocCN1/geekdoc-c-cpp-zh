# 5.6. Arithmetic Challenges on Microcontrollers

```
printf("Value after decrement: %d\n", c);

return 0;
}
```

Listing 5.2: https://onecompiler.com/c/426u2cbgs

Output:

Value before increment: 127
Value after increment: -128

Value before decrement: -128
Value after decrement: 127

+   - char is an 8-bit signed type, ranging from -128 to 127
- Incrementing 127 overflows to -128 (wraps around)
- Decrementing -128 underflows to 127 (wraps around other way)

This code demonstrates a common scenario, but might not always produce the same results on different platforms. The programmer must use appropriate data types to avoid getting unexpected values.

# 5.6 Arithmetic Challenges on Microcontrollers

Arithmetic operations on microcontroller-based embedded systems are more challenging than on personal computers. Things that we usually don't think about computers, like data types and operators, become more important and require special attention.

# 5.6.1 Integer Data Types and Operations

In embedded systems programming, integer data types are essential, but they come with some challenges. Some of the issues with C integer data types in embedded systems include:

+   - Limited Memory and Processing Power: Embedded systems often have limited memory and processing power, restricting the size and precision of integer values.
- Hardware-specific Limitations: Some embedded systems have specific limitations, as limited support for supposedly common operations like multiplication and division. For instance, some microcontrollers may not have a hardware multiplier, making multiplication slower.
- Integer Promotions and Conversions: C integer promotions and conversions can sometimes behave unexpectedly in embedded systems. For example, assigning a signed integer to an unsigned integer may result in unexpected values.