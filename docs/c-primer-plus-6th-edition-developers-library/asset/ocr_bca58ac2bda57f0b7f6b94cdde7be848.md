# box.us_view

the box union seen as an integer

bit 15

bit 0

# box.st_view

the box union seen as a structure

num_prtrs

gameio

num_comcds

num_drives

vid_setup

mother_bd

has_drive

Figure 15.3 A union as an integer and as a structure.

# Listing 15.4 The dualview.c Program

```
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
```