num: 10
num after turning off bit zero: 10

The value 0xFFFE used in the AND statement is the hexadecimal representation of 1111 1111 1111 1110. Therefore, the AND operation leaves all bits in num unchanged except for bit zero, which is set to zero. Thus, even numbers are unchanged, but odd numbers are made even by reducing their value by 1.

The AND operator is also useful when you want to determine whether a bit is on or off. For example, this program determines if a number is odd:

```
// Use bitwise AND to determine if a number is odd.

using System;

class IsOdd {
  static void Main() {
    ushort num;

    num = 10;

    if((num & 1) == 1)
      Console.WriteLine("This won't display.");

    num = 11;

    if((num & 1) == 1)
      Console.WriteLine(num + " is odd.");
  }
}
```

The output is shown here:

11 is odd.

In the if statements, the value of num is ANDed with 1. If bit zero in num is set, the result of num & 1 is 1; otherwise, the result is zero. Therefore, the if statement can succeed only when the number is odd.

You can use the bit-testing capability of the bitwise & to create a program that uses the bitwise & to show the bits of a byte value in binary format. Here is one approach:

```
// Display the bits within a byte.

using System;

class ShowBits {
  static void Main() {
    int t;
    byte val;

    val = 123;
    for(t=128; t > 0; t = t/2) {
      if((val & t) != 0) Console.Write("1 ");
```