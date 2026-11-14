![](bbox=[0.25, 0.08, 0.85, 0.26])

**EXAMPLE 6.5**
**ASCII**
**American Standard Code for Information- Interchange**

If one is using the ASCII code (ASCII is the acronym for American Standard Code for Information Interchange), then
`char x = 'A';`
`char y = 65;`

both of the above lines of code do the same thing, as the integer 65 is the decimal value of the ASCII character A.

**null character**

Note that there is a difference between the integer 0 and the character 0. Failure to notice the difference can result in a difficult to find program bug. The integer zero is written as 0. That is, all bits are 0. A char integer with a value of zero is often referred to as a *null character*. On the other hand "0" has a value of 48 in the ASCII character set. If the objective is to compare something to zero but we use "0", we are actually comparing to the integer 48. When working with integers and characters, always make certain which one is intended, the integer interpretation or the character interpretation.

# 6.4.3.1.4 SHORT INTEGER TYPE

**short** The short integral type, as the name suggests, is a short integer. It was commonly used in the early days of computing (when memory was expensive) to express small integer values. Typically, it is one-half the size of the integer. In embedded applications, memory is still expensive. Consequently, it is not unusual to use either chars or shorts to express integer numbers. In embedded applications, one typically selects the smallest type that will suffice for the task at hand.

# 6.4.3.1.5 LONG INTEGER TYPE

**long** The long integral type is the opposite of a short integral type and probably evolved in the same way. The long is used when an integral type is needed, but the size of the integer on the machine is too small to express the magnitude of the number and floating point numbers are either not available or not preferred. Typically, it is twice the size of the integer.

# 6.4.3.1.6 FLOATING POINT TYPES

**floating point type** We have seen how to use integral types to express information in a microprocessor. With integral types, the size of a number one can express is determined by the number of bits in an integer for the target machine. The microprocessor in the early PCs expressed integers as 16-bit words; therefore, the largest positive integer number that could be expressed was 65536. Although one seldom has to work with and manage the national debt, in an embedded application, there are times when it is necessary to represent larger numbers. To do so, one must use a different data type called the *floating point type*.