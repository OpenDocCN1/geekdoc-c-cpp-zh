
```c
/* room1 - the structure variable */
/* Called by: */
/*  main  */
/* Files used: */
/*  outfile.dat - output data file */
/* *************************************************** */
void funoutput(CUBICLE room1[])
{
    FILE *outptr;
    int i;
    outptr = fopen("outfile.dat", "w");

    for(i = 0; i < ENTRIES; i++) {
        fprintf(outptr, "Room: %d\n", i+1);
        fprintf(outptr,
            "length: %5.2f width: %5.2f height: %5.2f\n\n",
            room1[i].length, room1[i].width, room1[i].height);
        fprintf(outptr,"total wall area: %6.2f\n\n",
            room1[i].areewall);
        fprintf(outptr,"cost to paint walls: %6.2f\n\n",
            room1[i].paintcost);
    }
    fprintf(outptr, "\n\n");

    close(outptr);
    return;
}
```

# Input and Output

Input data file: "infile.dat"
20.5 16.5 10.0
30.6 25.4 8.0
45.5 30.0 9.5
16.5 12.8 8.0

Output data file: "outfile.dat"
Room: 1
length: 20.50 width: 16.50 height: 10.00
total wall area: 740.00
cost to paint walls: 1850.00

Room: 2
length: 30.60 width: 25.40 height: 8.00
total wall area: 896.00
cost to paint walls: 2240.00

Room: 3
length: 45.50 width: 30.00 height: 9.50
total wall area: 1434.50
cost to paint walls: 3586.25

Room: 4
length: 16.50 width: 12.80 height: 8.00
total wall area: 468.80
cost to paint walls: 1172.00

# Chapter Summary

A structure is a derived data type used to store and manipulate related data in the form of a heterogeneous record. A structure is declared with or without a tag to set up a template for storage to be allocated. The tag functions as a data type uniquely assigned to the structure. Once the structure is declared then the structure variables may be declared to allocate storage for the members of a structure variable. The general form of the structure declaration is as follows:

```c
struct tagname {
    structure data members;
};
```

The declaration of structure variables is as follows:

`struct tagname variable1,variable2,..., variableN;`

Once the structure variables are declared, the storage is allocated to them based on the structure declaration template.

Values for the data members of the structure variables may be defined by initialization, by assignment, through input, or through computation. The data members of the structure variables may be accessed using either a member operator, which is a dot (.) or by dereference and member operator (->) using a structure variable pointer. All arithmetic operations may be performed on the numeric members of the structure variables.

A synonym may be defined for a structure data type using the typedef construct. This is done as follows:

```c
typedef struct student_record
{
    structure members;
} STUDENT;
```

In this case STUDENT is the synonym for struct student_record. Structure variables may be declared using the synonym STUDENT instead of struct student_record. The following example shows such a declaration.

`struct student_record var1, var2;`

is equivalent to

`STUDENT var1, var2;`

Where var1 and var2 are structure variables.

The values of a structure variable may be assigned to another structure variable if the two structure variables have the same data type; otherwise the assignment must be member-by-member.

Structure variables may be passed to a function by value or by pointer. A structure variable may be returned from a function through the return statement or through argument and parameters.

A structure may be nested inside another structure. The nested structure must be declared first and the structure in which it is nested must be declared next.

A structure member may be a pointer to a variable of the same structure data type. Such structures are called self-referential structures. They are very useful for implementing linked lists.

A union is a construct used for optimizing the use of storage. In this construct only one member of the union is active and is allocated storage. Enumeration is used for data that can only have a small set of values, for example the name of each month, primary colors, etc.

# 732 Structures

# Exercises

1. Write a C program using the following structure to describe the axis of a cylinder, a circular cross-section, and the cylinder. Compute the area of the circular cross-section, the surface area of the cylinder, and the volume of the cylinder, given the length, and the radius.
```c
struct shape {
    float length;
    float radius;
    float area;
    float volume;
};
```

2. Write a C program using the following structure to hold compression load $p$ and diameter $d$ of a column of length $l$. Compute the compression stress and strain in the column. Output the load, diameter, stress, and strain with proper format.
```c
struct strength {
    float p;
    float d;
    float stress;
    float strain;
}
```
Use the following formulas to compute stress and strain:
$area = (\pi d^2)/4$
$stress = p/area$
where $E$ is the modulus of elasticity, which is $30 \times 10^6$ psi.

3. Write a C program to compute weekly pay for 10 machine workers with an ID, name, the hours worked, and hourly rate. Compute the gross pay with 25% deductions from the gross pay for the net pay. Output the ID, name, hourly rate, gross pay, deductions, and net pay. The overtime pay over 40 hours is 1.5 times the hourly rate. Organize the data by employee.

4. Write a C program to compute inventory for three different models. Each model has a certain number of cars and price for each car. Compute the total cost of all cars of each model. Output the model name, number of cars, and total cost of all cars of the models. Organize the data by model.

# APPENDIX A

**Nonprintable Characters**

| Dec | Hex | Oct | Bin | Character |
|---|---|---|---|---|
| 0 | 0 | 0 | 000000 | NUL—Binary Zero |
| 1 | 1 | 1 | 000001 | SOH—Start of Header |
| 2 | 2 | 2 | 000010 | STX—Start of Text |
| 3 | 3 | 3 | 000011 | ETX—End of Text |
| 4 | 4 | 4 | 000100 | EOT—End Of Transmission |
| 5 | 5 | 5 | 000101 | ENQ—Enquiry |
| 6 | 6 | 6 | 000110 | ACK—Acknowledge |
| 7 | 7 | 7 | 000111 | BELL—Bell |
| 8 | 8 | 10 | 001000 | BS—Backspace |
| 9 | 9 | 11 | 001001 | HT—Horizontal Tab |
| 10 | a | 12 | 001010 | LF—Line Feed or Newline |
| 11 | b | 13 | 001011 | VT—Vertical Tabulation |
| 12 | c | 14 | 001100 | FF—Form Feed |
| 13 | d | 15 | 001101 | CR—Carriage Return |
| 14 | e | 16 | 001110 | SO—Shift Out |
| 15 | f | 17 | 001111 | SI—Shift In |
| 16 | 10 | 20 | 010000 | DLE—Data Link Escape |
| 17 | 11 | 21 | 010001 | DC1—Device Control 1 |
| 18 | 12 | 22 | 010010 | DC2—Device Control 2 |
| 19 | 13 | 23 | 0010011 | DC3—Device Control 3 |
| 20 | 14 | 24 | 0010100 | DC4—Device Control 4 |
| 21 | 15 | 25 | 0010101 | NAC—Negative Acknowledgment |
| 22 | 16 | 26 | 0010110 | SYN—Synchronization |
| 23 | 17 | 27 | 0010111 | ETB—End of Text Block |
| 24 | 18 | 30 | 0011000 | CAN—Cancel |
| 25 | 19 | 31 | 0011001 | EM—End of Medium |
| 26 | la | 32 | 0011010 | SUB—Substitute |
| 27 | 1b | 33 | 0011011 | ESC—Escape |
| 28 | 1c | 34 | 0011100 | FS—File Separator |
| 29 | 1d | 35 | 0011101 | GS—Group Separator |
| 30 | 1e | 36 | 0011110 | RS—Record Separator |
| 31 | 1f | 37 | 0011111 | US—Unit Separator |
| 127 | 7f | 177 | 1111111 | DEL—Delete |

# ASCII Characters

| Dec | Hex | Oct | Bin | Character |
|---|---|---|---|---|
| 32 | 20 | 40 | 010000 | SP—Space |
| 33 | 21 | 41 | 010001 | ! |
| 34 | 22 | 42 | 010010 | " |
| 35 | 23 | 43 | 010011 | # |
| 36 | 24 | 44 | 010100 | $ |
| 37 | 25 | 45 | 010101 | % |
| 38 | 26 | 46 | 010110 | & |
| 39 | 27 | 47 | 010111 | . |
| 40 | 28 | 50 | 010100 | ( |
| 41 | 29 | 51 | 010101 | ) |
| 42 | 2a | 52 | 010110 | * |
| 43 | 2b | 53 | 010111 | + |
| 44 | 2c | 54 | 011100 | , |
| 45 | 2d | 55 | 011101 | - |
