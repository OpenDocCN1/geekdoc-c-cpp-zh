
One annoying aspect of enum types is that they are not recognized by C input-output statements. For example:

```
enum direction { north, south, east, west };
direction d1 = south;
printf("%d\n", south);
```

The value 1 gets output.

If it is desired to have a specific integer value associated with an enumerated value, then the integer can be assigned to the value when the data type is defined. Enumerated values that subsequently appear in the list will be assigned sequential values beginning with the specified integer value plus 1.

For example:

```
enum direction { up, down, left = 10, right };
```

| Enumerated Value | Numeric Value |
|---|---|
| up | 0 |
| down | 1 |
| left | 10 |
| right | 11 |

The name of the data type can be omitted when defining an enumerated data type. Variables can also be declared to be of the particular enumerated data type when the data type is defined:

```
enum { east, west, south, north } location;
```

Note that defining an enumerated data type within a function restricts the usage of that definition to variables defined within the function. Defining an enumerated data type at the beginning of the program, outside any function, makes the type definition global to the file.

## Typedef Statement

The `typedef` statement enables a programmer to assign an alternate name to a data type. For example:

```
typedef int COUNTER;
```

defines the name COUNTER to be equivalent to the C data type `int`. Variables can now be declared to be of type COUNTER:

```
COUNTER a, b, c;
```

This provides added readability to the program. Here's another example:

```
typedef char *STRING_PTR;
```

defines a name `STRING_PTR` to be a `char` pointer. We can now define variables to be of type `STRING_PTR`:

```
STRING_PTR buffer;
```

will be treated as a character pointer by the C compiler.

Another example:

```
typedef char STRING[81];
```

defines a type called `STRING` which is an array of 81 characters. We can now define variables to of type `STRING` as in:

```
STRING text;
```

This has the effect of defining the variable text to be a character array containing 81 characters and is equivalent to:

```
char text[81];
```

## Procedure to Define a New Type Name

- 1. Write the statement as if a variable of the desired type were being defined.
- 2. Where the name of the defined variable would normally appear, substitute the new type name.
- 3. In front of everything, place the keyword typedef.

```
#define Bool unsigned char
typedef unsigned char Bool
Bool a;
```

## Enumerations & Typedef Homework

1. a) Declare a tag for an enumeration whose values represent the seven days of the week.

```
enum Day { Sun, Mon, Tue, Wed, Thus, Fri, Sat };
```

b) Use typedef to define a name for the enumeration.

```
typedef enum Day THEWEEK
typedef enum {Sun, Mon, Tue, Wed, Thus, Fri, Sat} Day;
```

2. Which of the following statements about enumeration constants are true?

a) An enumeration constant may represent any integer specified by the programmer.

b) Enumeration constants have exactly the same properties as constants created using #define. False

c) Enumeration constants have the values 0, 1, 2, ... by default.

d) All constants in an enumeration must have different values. False

e) Enumeration constants may be used as integers in expressions.

3. Suppose that b and i are declared as follows:

```
enum { FALSE, TRUE } b;
int i;
```

Which of the following statements are legal? Which ones are "safe" (always yield a meaningful result)?

- a) b = FALSE; legal/safe
- b) b = i;
- c) b++; legal / safe (valid?)
- d) i = b; legal safe -> value one
- e) i = 2 * b + 1; safe -> value = 2*0+1 ... 1

All the statements are legal, since C allows integers and enumeration values to be mixed w/o restriction. However, only (a)(d)(e) are safe.

(b) not meaningful if b has a value other than 0 or 1 (c) will not yield a meaningful result if b ...

4. Suppose that the direction variable is declared as follows:

```
enum { NORTH, SOUTH, EAST, WEST } direction;
```

Let x and y be int variables. Write a switch statement that tests the value of direction, incrementing x if direction is EAST, decrementing x if direction is WEST, incrementing y if direction is SOUTH, and decrementing y if direction is NORTH.

5. What are the integer values of the enumeration constants in each of the following declarations?

- a) enum { NORTH, EAST, SOUTH, WEST };
  0   1   2   3
- b) enum { DIAMONDS = 5, HEARTS, CLUBS, SPADES };
  5   6   7   8
- c) enum { MON = 8, TUES, WED, THURS = 14, FRI };
  8   9   10  14  15
- d) enum { RED = 5, BLUE, GREEN, YELLOW = 12, BROWN };
  5   6   7   12  13

```
int main(void)
enum direction: int x,y
for (direction: NORTH; direction <= WEST; ++direction)
switch (direction) {
    case NORTH: y--; break;
    case SOUTH: y++; break;
    case EAST: x++; break;
    case WEST: x--; break;
}
return 0;
}
```

- Introduction to Structures
- Manipulating Entire Structures
- Struct Example: Today's Date and Tomorrow's Date
- Arrays of Structures
- Nesting Structures
- Structures Homework
- Database Lab

free() -> freeing cleaning

![](img/7f36c52b5170b89b142dbb7b1ea4666b_410_0.png)

```
typedef struct {
 char f_name[20];
 char l_name[10];
 int ph;
 PHONE_BOOK_ENTRY + NEXT,
} PHONE_BOOK_ENTRY;
```

- Step 1: Using malloc() reserve space for phone_book_Entry structure
- 2: initialize record.
- 3: if first phone book quits to first rec.
- if not first rec. add to the end of the list
- 4: Assign NULL to (next) of last element (next field)
- Called 'Linked List'

![](img/7f36c52b5170b89b142dbb7b1ea4666b_410_1.png)

## Introduction to Structures

We have previously used arrays to store collections of data of the same type (and a specified size) using a single name:

```
int num[10];
```

![](img/7f36c52b5170b89b142dbb7b1ea4666b_411_0.png)

We learned to reference individual elements of an array using subscripts such as num[1] or num[1].

![](img/7f36c52b5170b89b142dbb7b1ea4666b_411_1.png)

Often, we have a need to create collections of related data of different types. For example, if I wanted to collect information about students, I might be interested in the following information:

- The student's name (string of characters)
- The student's gpa (double)
- The student's expected graduation year (integer)

We can model such a collection in C using the data type called a struct. A struct is an example of a user-defined data type, i.e., we can define our own struct to model whatever data we want.

For example:

```
typedef struct {
   char name[30];
   double gpa;
   int year;
} Student;
```

This serves as a blueprint or template for the creation of a new data type called Student. This new user-defined data type, Student, can be used to declare variables just like any built-in data type:

```
typedef struct {
   char name[30];
   double gpa;
   int year;
} Student;

int main(void) {
   Student s1, s2, s3;
   ...
   return 0;
}
```

Our declarations above create three variables of type Student: s1, s2, and s3. Each of these variables create now has storage in memory for a character string, a double, and an int. Note that the name of our new data type begins with a capital letter. While it's not required, it's a good rule to follow.

Also note that the struct is declared outside of main() in the global scope. This allows the struct to be visible to all parts of the program. If the struct were only declared within main(), then it would be local to main() and only visible within main().

The structure can be depicted as follows:

| | name | gpa | year |
|---|---|---|---|
| s1 | Sammie | 3.85 | 2016 |

## Referencing elements of a struct.

We now have the same problem with structs as we had with arrays. How do we reference individual elements (called components or fields) of a struct? With arrays we used subscripts. With structs we use a period, also known as a direct component selection operator (or, more simply, the selection operator, for short).

For example, we can give values to each of the fields of the struct as follows:

```
s1.gpa = 3.85;
s1.year = 2016;
strcpy(s1.name, "Sammy");
```

## Example: Date structure.

Suppose that we have a need to keep track of various dates. We can define a Date data type as follows:

```
typedef struct {
    int month;
    int day;
    int year;
} Date;
```

Once we have defined a Date data type, we can create Date variables as follows:

```
typedef struct {
    int month;
    int day;
    int year;
} Date;

int main(void) {
    Date yesterday, today, tomorrow, appointment, birthday;
    ...
    ...
    return 0;
}
```
