
You can use a value of 1 for the opaque member to indicate that the box is opaque and a 0 value to indicate transparency. You can do the same for the show_border member. For colors, you can use a simple RGB (red-green-blue) representation. These are the primary colors for mixing light. A monitor blends red, green, and blue pixels to reproduce different colors. In the early days of computer color, each pixel could be either on or off, so you could use one bit to represent the intensity of each of the three binary colors. The usual order is for the left bit to represent blue intensity, the middle bit green intensity, and the right bit red intensity. Table 15.3 shows the eight possible combinations. They can be used as values for the fill_color and border_color members. Finally, you can choose to let 0, 1, and 2 represent the solid, dotted, and dashed styles; they can be used as values for the border_style member.

**Table 15.3 Simple Color Representation**

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

**Listing 15.3 The fields.c Program**

```c
/* fields.c -- define and use fields */
#include <stdio.h>
#include <stdbool.h>   // C99, defines bool, true, false

/* line styles */
#define SOLID  0
#define DOTTED 1
#define DASHED 2
/* primary colors */
#define BLUE   4
#define GREEN 2
#define RED 1
/* mixed colors */
#define BLACK 0
#define YELLOW (RED | GREEN)
#define MAGENTA (RED | BLUE)
#define CYAN (GREEN | BLUE)
#define WHITE (RED | GREEN | BLUE)

const char * colors[8] = {"black", "red", "green", "yellow",
"blue", "magenta", "cyan", "white"};

struct box_props {
    bool opaque : 1; // or unsigned int (pre C99)
    unsigned int fill_color : 4;
    unsigned int show_border : 1; // or unsigned int (pre C99)
    unsigned int border_color : 3;
    unsigned int border_style : 2;
    unsigned int : 2;
};

void show_settings(const struct box_props * pb);

int main(void)
{
    /* create and initialize box_props structure */
    struct box_props box = {true, YELLOW, true, GREEN, DASHED};
    printf("Original box settings:\n");
    show_settings(&box);
    box.opaque = false;
    box.fill_color = WHITE;
    box.border_color = MAGENTA;
    box.border_style = SOLID;
    printf("\nModified box settings:\n");
    show_settings(&box);
    return 0;
}

void show_settings(const struct box_props * pb)
{
    printf("Box is %s.\n",
    pb->opaque == true ? "opaque" : "transparent");
    printf("The fill color is %s.\n", colors[pb->fill_color]);
    printf("Border %s.\n", pb->show_border == true ? "shown" : "not shown");
    printf("The border color is %s.\n", colors[pb->border_color]);
    printf("The border style is ");
    switch(pb->border_style)
    {
        case SOLID  : printf("solid.\n"); break;
        case DOTTED : printf("dotted.\n"); break;
        case DASHED : printf("dashed.\n"); break;
        default     : printf("unknown type.\n");
    }
}
```

Here is the output:

```text
Original box settings:
Box is opaque.
The fill color is yellow.
Border shown.
The border color is green.
The border style is dashed.
```

```text
Modified box settings:
Box is transparent.
The fill color is white.
Border shown.
The border color is magenta.
The border style is solid.
```

There are some points to note. First, you can initialize a bit-field structure by using the same syntax regular structures use:

```c
struct box_props box = {true, YELLOW, true, GREEN, DASHED};
```

Similarly, you can assign to bit-field members:

```c
box.fill_color = WHITE;
```

Also, you can use a bit-field member as the value expression for a switch statement. You can even use a bit-field member as an array index:

```c
printf("The fill color is %s.\n", colors[pb->fill_color]);
```

Notice that the colors array was defined so that each index value corresponds to a string representing the name of the color having the index value as its numeric color value. For example, an index of 1 corresponds to the string "red", and the symbolic constant red has the value of 1.

### Bit Fields and Bitwise Operators

Bit fields and bitwise operators are two alternative approaches to the same type of programming problem. That is, often you could use either approach. For instance, the previous example used a structure the same size as unsigned int to hold information about a graphics box. Instead, you could use an unsigned int variable to hold the same information. Then, instead of using structure member notation to access different parts, you could use the bitwise operators for that purpose. Typically, this is a bit more awkward to do. Let's look at an example that takes both approaches to illustrate the differences, not to suggest that taking both approaches simultaneously is a good idea!

You can use a union as a means of combining the structure approach with the bitwise approach. Given the existing declaration of the struct box_props type, you can declare the following union:

```c
union Views /* look at data as struct or as unsigned short */
{
    struct box_props st_view;
    unsigned short us_view;
};
```

On some systems, an unsigned int and a box_props structure both occupy 16 bits of memory. On others, such as ours, unsigned int and box_props are 32 bits. In either case, with this union, you can use the st_view member to look at that memory as a structure or use the us_view member to look at the same block of memory as an unsigned short. Which bit fields of the structure correspond to which bits in the unsigned short? That depends on the implementation and the hardware. The following example assumes that structures are loaded into memory from the low-bit end to the high-bit end of a byte. That is, first bit field in the structure goes into bit 0 of the word. (For simplicity, Figure 15.3 illustrates this idea with a 16-bit unit.)

Listing 15.4 uses the Views union to let you compare the bit field and bitwise approaches. In it, box is a Views union, so box.st_view is a box_props structure using bit fields, and box.us_view is the same data viewed as an unsigned short. Recall that a union can have its first member initialized, so the initialization values match the structure view. The program displays box properties using a function based on the structure view and also with a function based on the unsigned short view. Either approach lets you access the data, but the techniques differ. The program also uses the itobs() function defined earlier in this chapter to display the data as a binary string so that you can see which bits are on and which are off.

```text
box.us_view
the box union seen as an integer
bit 15
bit 0

box.st_view
the box union seen as a structure
num_prtrs
gameio
num_comcds
num_drives
vid_setup
mother_bd
has_drive
```

**Figure 15.3 A union as an integer and as a structure.**

**Listing 15.4 The dualview.c Program**

```c
/* dualview.c -- bit fields and bitwise operators */
#include <stdio.h>
#include <stdbool.h>
#include <limits.h>
/* BIT-FIELD CONSTANTS */
/* line styles */
#define SOLID 0
#define DOTTED 1
#define DASHED 2
/* primary colors */
#define BLUE 4
#define GREEN 2
#define RED 1
/* mixed colors */
#define BLACK 0
#define YELLOW (RED | GREEN)
#define MAGENTA (RED | BLUE)
#define CYAN (GREEN | BLUE)
#define WHITE (RED | GREEN | BLUE)

/* BITWISE CONSTANTS */
#define OPAQUE 0x1
#define FILL_BLUE 0x8
#define FILL_GREEN 0x4
#define FILL_RED 0x2
#define FILL_MASK    0xE
#define BORDER       0x100
#define BORDER_BLUE  0x800
#define BORDER_GREEN 0x400
#define BORDER_RED   0x200
#define BORDER_MASK  0xE00
#define B_SOLID      0
#define B_DOTTED     0x1000
#define B_DASHED     0x2000
#define STYLE_MASK   0x3000

const char * colors[8] = {"black", "red", "green", "yellow",
    "blue", "magenta", "cyan", "white"};
struct box_props {
    bool opaque           : 1;
    unsigned int fill_color : 3;
    unsigned int           : 4;
    bool show_border      : 1;
    unsigned int border_color : 3;
    unsigned int border_style : 2;
    unsigned int           : 2;
};

union Views    /* look at data as struct or as unsigned short */
{
    struct box_props st_view;
    unsigned short us_view;
};

void show_settings(const struct box_props * pb);
void show_settings1(unsigned short);
char * itobs(int n, char * ps);

int main(void)
{
    /* create Views object, initialize struct box view */
    union Views box = {{true, YELLOW, true, GREEN, DASHED}};
    char bin_str[8 * sizeof(unsigned int) + 1];

    printf("Original box settings:\n");
    show_settings(&box.st_view);
    printf("\nBox settings using unsigned int view:\n");
    show_settings1(box.us_view);

    printf("bits are %s\n",
        itobs(box.us_view, bin_str));
    box.us_view &= ~FILL_MASK;      /* clear fill bits */
```
