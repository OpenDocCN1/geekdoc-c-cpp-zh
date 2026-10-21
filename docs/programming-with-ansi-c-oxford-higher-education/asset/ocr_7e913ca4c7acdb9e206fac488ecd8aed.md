> This is testing of getline and then we have read t
> Now the read is being tested
> It requires ctrl-Z to end
> ^Z
> Now the read is being tested
> It requires ctrl-Z to end

# How the Program Works

The program has demonstrated the use of the three different functions, namely, cin.getline(), cin.read(), and cin.write(). When the user types characters, getline() or read() accepts only the maximum number of characters specified in the argument. The number of characters printed is taken from the characters read. This is why there is a mismatch between the characters input and the characters displayed as output.

# 12.7 FORMATING I/O

Formatting can be done using two different ways. The first method is to use built-in ios functions. Table 12.2 lists the various ios member functions.

Table 12.2 Use of ios functions

| ios member function | Use |
| width() | This specifies the width for display. The output will take up the width specified. It is used in aligning vertical columns of numeric items. |
| precision() | This specifies the precision of the floating-point number. The default precision is six digits after decimal point. |
| fill() | This specifies the character for filling up the unused portion of field. It is usually used with width member function. The remaining part of the field will be filled up with the char specified. Default char is space. |
| setf() | This specifies the format flags that control output display such as left or right justification, padding after sign symbol, scientific notation display, and displaying base of the number (such as hexadecimal, decimal, and octal). |
| unsetf() | This provides undo operation for the operations with setf(). |

# 12.7.1 Member Functions of ios

The prototype for all the following functions is:

```
All ios functions return old values of the stream while they are called to set them to new values.
<old value of stream> function_name(<specified new value>)
```

The functions set the new value to the stream and return the old value. The width() function sets the new width to the argument specified and returns the old width. The precision() function sets new precision and returns the old precision. Similarly, fill() returns old fill char and sets new fill char.

# width()

It specifies the minimum field width for display. The output following this statement will use the width specified. It resets itself after the first output after this statement. The output of the statements