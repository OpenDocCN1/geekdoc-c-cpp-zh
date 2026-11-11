This type of data stores a number from 0 to 255 in an 8-bit system of binary numbers. For example, B10010 is the number 18, because this uses a base 2 system.

# ***Int***

Integers are how you will store numbers for the most part. Because most Arduinos have a 16-bit system, the minimum value is -32,768 and the maximum value of an integer is 32,767. The Arduino Due and a few other boards work on a 32-bit system, and thus can carry integers ranging from -2,147,483,648 to 2,147,483,647. Remember these numbers when you are attempting arithmetic with your program, as any numbers higher or lower than these values will cause errors in your code.

# ***Unsigned Int***

This yields the ability to store numbers from 0 to 65,535 on the 8-bit boards with which you will likely be working. If you have higher values than the signed integers will allow, you can switch to unsigned integers and achieve the same amount of range but all in the positive realm, such that you have a higher absolute value of the range.

# ***Word***

A word stores a 16-bit unsigned number on the Uno and on other boards with which you will likely be working. In using the Due and the Zero, you will be storing 32-bit numbers using words. Word is essentially the means by which integers and numbers are stored.

# ***Long***

If you need to store longer numbers, you can access 4-byte storage, or 32-bit storage in other words, using the long variable. You simply follow an integer in your coded math with the capital letter *L*. This will achieve numbers from -2,147,483,648 to 2,147,483,647.

# ***Unsigned Long***