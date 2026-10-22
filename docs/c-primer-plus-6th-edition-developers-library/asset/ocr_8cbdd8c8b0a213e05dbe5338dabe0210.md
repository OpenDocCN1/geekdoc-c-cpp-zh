You can use a value of 1 for the opaque member to indicate that the box is opaque and a 0 value to indicate transparency. You can do the same for the show_border member. For colors, you can use a simple RGB (red-green-blue) representation. These are the primary colors for mixing light. A monitor blends red, green, and blue pixels to reproduce different colors. In the early days of computer color, each pixel could be either on or off, so you could use one bit to represent the intensity of each of the three binary colors. The usual order is for the left bit to represent blue intensity, the middle bit green intensity, and the right bit red intensity. Table 15.3 shows the eight possible combinations. They can be used as values for the fill_color and border_color members. Finally, you can choose to let 0, 1, and 2 represent the solid, dotted, and dashed styles; they can be used as values for the border_style member.

# Table 15.3 Simple Color Representation

| Bit Pattern | Decimal | Color |
|---|---|---|
| 000 | 0 | Black |
| 001 | 1 | Red |
| 010 | 2 | Green |
| 011 | 3 | Yellow |
| 100 | 4 | Blue |
| 101 | 5 | Magenta |
| 110 | 6 | Cyan |
| 111 | 7 | White |

Listing 15.3 uses the box_props structure in a simple example. It uses #define to create symbolic constants for the possible member values. Note that the primary colors are represented by a single bit being on. The other colors can be represented by combinations of the primary colors. For example, magenta consists of the blue bit and the red bit being on, so it can be represented by the combination BLUE | RED.

# Listing 15.3 The fields.c Program

```
/* fields.c -- define and use fields */
#include <stdio.h>
#include <stdbool.h>   //C99, defines bool, true, false

/* line styles */
#define SOLID  0
#define DOTTED 1
#define DASHED 2
/* primary colors */
#define BLUE   4
```