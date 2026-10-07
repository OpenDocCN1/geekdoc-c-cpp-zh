
```
struct rectangle {
    struct coord toleft;
    struct coord bottomrt;
};
```

This statement defines a structure of type rectangle that contains two structures of type coord. These two type coord structures are named toleft and bottomrt.

The preceding statement defines only the type rectangle structure. To declare a structure, you must include a statement such as

```
struct rectangle mybox;
```

You could have combined the definition and declaration, as you did before for the type coord:

```
struct rectangle {
    struct coord toleft;
    struct coord bottomrt;
} mybox;
```

To access the actual locations (the type int members), you must apply the member operator (.) twice. Thus, the expression
mybox.toleft.x

refers to the x member of the toleft member of the type rectangle structure named mybox. To define a rectangle with coordinates (0,10), (100,200), you would write

```
mybox.toleft.x = 0;
mybox.toleft.y = 10;
mybox.bottomrt.x = 100;
mybox.bottomrt.y = 200;
```

Maybe this is a bit confusing. You can understand better if you look at Figure 11.1, which shows the relationship between the type rectangle structure, the two type coord structures it contains, and the two type int variables each type coord structure contains. These structures are named as in the preceding example.

# LESSON 11 Implementing Structures, Unions, and TypeDefs

FIGURE 11.1

| A type int variable (x) | mybox.topleft.x | A type coord structure (topleft) |
|---|---|---|
| A type int variable (y) | mybox.topleft.y | A type rectangle structure (mybox) |
| A type int variable (x) | mybox.bottomrt.x | A type coord structure (bottomrt) |
| A type int variable (y) | mybox.bottomrt.y | |

The relationship between a structure, structures within a structure, and the structure members.

Listing 11.2 presents an example of using structures that contain other structures. This listing takes input for the coordinates of a rectangle and calculates and displays the rectangle's area. Note the program's assumptions, given in comments near the start of the program (lines 3 through 8).

# Input

# LISTING 11.2 struct c: A Demonstration of Structures that Contain Other Structures

```
/* Demonstrates structures that contain other structures. */
/* Receives input for corner coordinates of a rectangle and
calculates the area. Assumes that the y coordinate of the
lower-right corner is greater than the y coordinate of the
upper-left corner
```

# Using Structures That Are More Complex

```
30:    scanf("%d", &mybox.topleft.x);
31:
32:    printf("\nEnter the top left y coordinate: %d");
33:    scanf("%d", &mybox.topleft.y);
34:
35:    printf("\nenter the bottom right x coordinate: %d");
36:    scanf("%d", &mybox.bottomrt.x);
37:
38:    printf("\nenter the bottom right y coordinate: %d");
39:    scanf("%d", &mybox.bottomrt.y);
40:
41:    /* Calculate the length and width */
42:
43:    width = mybox.bottomrt.x - mybox.topleft.x;
44:    length = mybox.topleft.y - mybox.bottomrt.y;
45:
46:    /* Calculate and display the area */
47:
48:    area = width * length;
49:    printf("\nThe area is %ld units.\n", area);
50:
51:    return 0;
52: }
```

# Output

Enter the top left x coordinate: 0

Enter the top left y coordinate: 6

Enter the bottom right x coordinate: 9

Enter the bottom right y coordinate: 1

The area is 45 units.

# Analysis

The coord structure is defined on lines 15 through 18 with its two members, x and y. Lines 20 through 23 declare and define an instance, called mybox. The two members of the rectangle structure are toleft and bottomrt, both of type coord. Lines 29 through 39 fill the values in the mybox structure. At first, it might seem that there are only two values fill because mybox has only two members. However, each of mybox's members has its own members. toleft and bottomrt have two members each, x and y from the coord structure. This gives a total of four members to be filled. After the members are filled with values, the area is calculated using the structure and member names. When using the x and y values, you must include the instance name. Because x and y are in a structure within a structure, you must use the names of both structures—mybox.bottomrt.x, mybox.bottomrt.y, mybox.topleft.x, and mybox.topleft.y—in the calculations. The C programming language does not have a limit on the number of structures that can be nested; however, compliance to ANSI standard guarantees support for only 63 levels. With memory allows, you can define structures that contain structures—well, you get the idea! Of course, rarely are more than three levels of nesting using any C program.

# Structures That Contain Arrays

You can define a structure that contains one or more arrays as members. The array can be of any data type (int, char, and so on). For example, the statements

```
struct data {
  short x[4];
  char y[10];
};
```

define a structure of type data that contains a 4-element array member x and a 10-element array member y. You can declare a structure named record of type data as follows:

```
struct data record;
```

The organization of this structure is shown in Figure 11.2. Note that, in this figure, the elements of array x are shown to take up twice much space as the elements of array y. This is because a short typically carries 2 bytes, whereas a char usually carries only 1 byte (as learned in Lesson 3, “Storing Information: Variables and Constants”).

FIGURE 11.2
The organization of a structure that contains arrays as members.

img/d57287e6f87c745d39250550bf01c270_0.png

# Using Structures That Are More Complex

You access individual elements of arrays that structure members using a combination of the member operator and array subscripts:
record.x[2] = 100;
record.y[1] = 'x';

You probably remember that character arrays are most frequently used to store strings. You should remember (from Lesson 9, “Pointers”) that the name of an array, without brackets, is a pointer to the array. Because this holds true for arrays that structure members, the expression
record.y

is a pointer to the first element of array y[] in the structure record. Therefore, you could print the contents of y[] onscreen using the statement
puts(record.y);

Now look at another example. Listing 11.3 uses a structure that contains a float variable and two char arrays.

# LISTING 11.3 array.c: A Structure That Contains Array Members

```
1: /* Demonstrates a structure that has array members. */
2:
3: #include <stdio.h>
4: #define NAMESIZE 30
5: /* Define and declare a structure to hold the data. */
6: /* It contains one float variable and two char arrays. */
7:
8: struct data{
9: float amount;
10: char fname[NAMESIZE];
11: char lname[NAMESIZE];
12: } rec;
13:
14: int main( void )
15: {
16:
17: /* Input the data from the keyboard. */
18: printf("Enter the donor's first and last name,\n");
19: printf("separated by a space: ");\n
20: scanf("%s %s", rec.fname, rec.lname);
21:
22: printf("\nenter the donation amount: ");\n
23: scanf("%f", &rec.amount);
24:
```
25: /* Display the information. */
26: /* Note: %.2f specifies a floating-point value *
27: /* to be displayed with two digits to the right */
28: /* of the decimal point. */
29:
30: /* Display the data on the screen. */
31:
32: printf("%s %s $%.2f.\n", rec.fname, rec.lname,
33: rec.amount);
34:
35:
36: }
```

# Output ▼

Enter the donor's first and last names, separated by a space: Jayne Hatton

Enter the donation amount: 450

Donor Jayne Hatton gave $450.00.

# Analysis ▼

This program includes a structure that contains array members named fname [NAMESIZE] and lname [NAMESIZE]. Both are arrays of characters that hold a person’s first name and last name, respectively. By using a constant to define the maximum length of names, it is easier to go back and make a change if you discover the need to allow for longer names. The structure declared on lines 8 through 12 is called data. It contains the fname and lname characters with a float variable called amount. This structure is ideal for holding a person's name (in two parts, first name and last name) and a value, such as the amount donated to a charitable organization.

# Arrays of Structures

If you can have structures that contain arrays, can you also have arrays of structures? You bet you can! In fact, arrays of structures are powerful programming tools. Here’s how it’s done.

You’ve seen how a structure definition can be tailored to fit the data your program has to work with. Usually a program has to work with more than one instance of the data. For
