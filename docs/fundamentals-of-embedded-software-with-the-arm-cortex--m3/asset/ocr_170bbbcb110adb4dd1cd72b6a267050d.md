![](bbox=[0.18, 0.09, 0.89, 0.23])

FIGURE 4-11 Relationship between a pointer and what it points to.

# ## 4.6.2 Arrays, Pointers, and the “Address of” Operator

When we declare an array of bytes called “a”, a corresponding sequence of bytes is allocated in memory. The element a[0] is stored in the first byte, and its address is known as the base address of the array. We can obtain this address by applying the “address of” operator to a[0], as in &a[0]. Since &a[0] is the address of data of type uint8_t, we think of it as an expression whose value is of type “pointer to uint8_t” (Figure 4-12).

![](bbox=[0.21, 0.41, 0.86, 0.57])

FIGURE 4-12 An array of chars and their corresponding memory addresses.

In C, the name of an array by itself with no subscript (e.g., “a”) is strictly equivalent to the address of its first element (e.g., &a[0]). Thus, the data type of a is also “pointer to uint8_t,” which means that we may substitute a pointer in place of the name of an array when subscripting (e.g., p[k]). This fact can be used to access our display buffer as an array by initializing a pointer to the base address of the display buffer and then applying subscripting:

```
uint8_t *color_display_buffer = (uint8_t *) 0x80000 ;
...
color_display_buffer[2*(80*row+col)] = 'A' ;
```

Of course, it would be nicer to use one subscript to select the row, a second subscript to select the column, and a third to differentiate between the ASCII and attribute bytes of the character cell. To do so requires that we first describe a row of 80 two-byte cells using a pair of typedefs:

```
typedef uint8_t ONE_CELL[2] ; // 1 cell of 2 bytes
typedef ONE_CELL ONE_ROW[80] ; // 1 row of 80 cells
```