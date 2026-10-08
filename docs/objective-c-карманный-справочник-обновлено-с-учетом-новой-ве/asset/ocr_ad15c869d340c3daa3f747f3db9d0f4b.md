binary floating-point, just as 0.1 in base three (one third) cannot be represented by any finite decimal sequence.

A binary number is the sum of a set of powers of two, just as a decimal number is a sum of powers of ten. With fractional values, the digits after the radix point indicate halves, quarters, eighths, and so on. If you try to create a value of 0.1 by adding powers of two, you never succeed, although you get progressively closer. Exactly the same thing happens when you try to create a third by adding powers of ten (a three tenths, plus three hundredths, plus three thousands, and so on).

One solution is to use fixed-point arithmetic. Rather than storing dollars, you might store hundredths of a cent. You must then remember to normalize your values, and you are limited by the range of an integer type. Objective-C provides another option: decimal floating-point types.

The NSDecimal type is a C structure that represents a decimal value. Somewhat strangely, there is no C API for creating these. You must create an NSNumber instance and then send it a -decimalValue message.

You then have two choices for arithmetic. NSNumber instances are immutable. You can create new ones as a result of arithmetic—for example, sending a decimalNumberByAdding: message to one.