the hardware could be designed so that data written to a specific memory address is sent instead as a command to a particular I/O device, while data read from that same address might provide information about the current status of the device.

A typical example of a memory-mapped I/O device is a display buffer in which each character position on the screen is assigned one or more unique memory addresses. In the PC, for example, the color-display buffer is mapped to memory starting at address B800016. Each character position is assigned two bytes; the first contains an ASCII character code followed by a second byte that specifies the foreground and background colors of the character. The address of the first byte assigned to a specific row and column is thus calculated as.

B800016 + 2 x (80 x row + col)

# 4.6.1 Accessing Data Using a Pointer

When using variables in C, you normally never worry about where in memory they are located. You merely create the variable (i.e., allocate memory for it) by declaring it, and then manipulate its content by referring to its identifier. To display text on the screen, however, we have to use a pointer.

A pointer in C is a variable that contains an address. There is no pointer data type name. Instead, we declare that a variable is a pointer by placing an asterisk ("*") in front of its identifier in the declaration:

```
uint8_t *p ; /* "p" is a pointer to a byte */
```

Note that the declaration makes explicit the type (and thus the size) of the object that is pointed to. Although the declaration allocates memory to hold the pointer, it must still be initialized before it can be used, as in

```
p = (uint8_t *) (0xB8000 + 2 * (80 * row + col)) ;
```

Of course, the initial value may be specified in the declaration if desired, as in

```
uint8_t *p = (uint8_t *) (0xB8000 + 2 * (80 * row + col)) ;
```

Without the cast, the last example represents an attempt to store data of type int in a variable intended to hold an address. Although an address and an int may use the same number of bits, if we do not use a cast the compiler will still issue a warning that we were mixing "apples and oranges".

Once a pointer has been initialized, we can access the data that it points to by using the asterisk as a de-reference operator:

```
*p = 'A' ; /* Display 'A' on the screen. */
```

The result of declaring and initializing such a pointer and then using it to store a character into the display buffer is depicted graphically in Figure 4-11.

Note that since p was declared as a pointer to a byte, the de-referenced pointer (*p) can be used in any context where you would normally use a variable of type uint8_t — that is, on either side of an assignment operator.