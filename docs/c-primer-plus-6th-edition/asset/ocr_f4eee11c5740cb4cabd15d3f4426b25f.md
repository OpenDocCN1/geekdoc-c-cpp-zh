# Chapter 17 Input, Output, and Files

+   - float &
- double &\n- long double &

These are referred to as formatted input functions because they convert the input data to the format indicated by the target.
A typical operator function has a prototype like the following:

```
istream & operator>>(int &);
```

Both the argument and the return value are references.With a reference argument (see Chapter 8,"Adventures in Functions"), a statement such as following causes the operator->() function to work with the variable staff_size itself rather than with a copy, as would be the case with a regular argument:

```
cin >> staff_size;
```

Because the argument is a reference, cin is able to directly modify the value of a variable used as an argument. The preceding statement, for example, directly modifies the value of the staff_size variable.We'll get to the significance of a reference return value in a moment. First, let's examine the type conversion aspect of the extraction operator. For arguments of each type in the preceding list of types, the extraction operator converts the character input to the indicated type of value. For example, suppose staff_size is type int. In this case, the compiler matches

```
cin >> staff_size;
```

to the following prototype:

```
istream & operator>>(int &);
```

The function corresponding to that prototype then reads the stream of characters being sent to the program—say, characters 2, 3, 1, 8, and for a system using a 2-byte int, the function converts these to the 2-byte binary representation of the integer 23184. If, on the other hand, staff_size were double, cin would use operator>>(double &) to convert the same input into the 8-byte floating-point representation of the value 23184.

Incidentally, you may use the hex, oct, and dec manipulators with cin to specify that integer input is to be interpreted as hexadecimal, octal, or decimal format. For example, the statement causes an input of 12 or 0x12 to be read as hexadecimal 12, or decimal 18, and it causes ff or FF to be read as decimal 255:

```
cin >> hex;
```

The istream class overloads the >> extraction operator for character pointer types:

+   - signed char *
- char *
- unsigned char *