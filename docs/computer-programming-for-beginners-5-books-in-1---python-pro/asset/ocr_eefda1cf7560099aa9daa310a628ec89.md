time going over all of the types so that you have a firm and solid idea of what these types are as well as how to use them effectively.

*Byte* - This represents an integer value anywhere from 0 to 255. This only takes up 1 byte of data and can be especially useful in Arduino programming since so many things in Arduino programming are on a sequence of 0 to 255 anyway.

*Int* - This represents an integer value of the average size, roughly four bytes. It can hold relatively large values but be careful because if you get into the two million area, you’re going to find yourself going far over the buffer limit for integer variables, which means that they’re going to be restarting from the very lowest number that an integer can hold.

*Float* - This represents a floating-point number or a decimal. These aren’t terribly common in Arduino programming, but they are more common than doubles. These can hold roughly up to 5 decimal places and be as large as about 32,000.

*Double* - This represents a double-precision floating point number. These are twice the size of floating-point numbers in terms of system memory, but they are far more accurate than normal floats and can have a larger non-decimal number than floating points do.

*Unsigned values* - These are the same size as their normal values, like unsigned ints and floats, but they don’t have the capacity for negative numbers. This means that they start at 0 and can store positive numbers twice as big as normal integers and floats can, but at the price of not being able to store any negative numbers. When you’re working with non-negative numbers, these are a great place to start.

*Short* - These are integer values that are half the size of integer values but twice the size of byte values. They can hold numbers into the 30,000s, but not any bigger than that. If you’re working with smaller numbers, you’ll probably want to use these over integers just because they use up less memory.

*Long* - These are integer values that are twice the size of normal integers, which means they can hold numbers well into the two billion areas, but there is no default value type large enough for any number bigger than that aside from unsigned longs which can be roughly four and a half billion.

*Char* - These represent ASCII character values. These are essentially any