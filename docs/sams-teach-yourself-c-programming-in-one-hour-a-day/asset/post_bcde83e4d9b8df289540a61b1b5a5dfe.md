
## Working with Pointers and Arrays of Structures

You've seen that arrays of structures can be a powerful programming tool, as can pointers to structures. You can combine the two, using pointers to access structures that are array elements.

To illustrate, here is a structure definition from an earlier example:

```
struct part
{
    short number;
    char name[10];
}
```

After the part structure is defined, you can declare an array of type part:

```
struct part data[100];
```

Next, you can declare a pointer to type part and initialize it to point to the first structure in the array data:

```
struct part *p_part;
p_part = &data[0];
```

Recall that the name of an array without brackets is a pointer to the first array element, so the second line could also have been written as

```
p_part = data;
```

You now have an array of structures of type part and a pointer to the first array element (that is, the first structure in the array). For example, you could print the contents of the first element using the

```
printf("%d %s", p_part->number, p_part->name);
```

What if you want to print all the array elements? You would probably use a for loop, printing every element with each iteration of the loop. To access the members using pointer notation, you must change the pointer p_part so that with each iteration of the loop it points to the next array element (that is, the next structure in the array). How do you do this?

C's pointer arithmetic comes to your aid. The unary increment operator (++) has a special meaning when applied to a pointer: It means "increment the pointer by the size of the object it points to." Put another way, if you have a pointer ptr that points to a data object of type obj, the statement

```
ptr++;
```

## Structures and Pointers

has the same effect as

ptr += sizeof(obj);

This aspect of pointer arithmetic is particularly relevant to arrays because array elements are stored sequentially in memory. If a pointer points to array element n, incrementing the pointer with the (++) operator causes it to point to element n+1. This is illustrated in Figure 11.6, which shows an array named x[] of 4-byte elements (for example, a structure containing two type short members, each 2 bytes long). The pointer was initialized to point to x[0]; each time ptr is incremented, it points to the next array element.

## FIGURE 11.6

![](img/d572877e6f876c745d39250550bf01c5_285_0.png)

What this means is that your program can step through an array of structures (or any other data type, for that matter) by incrementing a pointer. This sort of notation is usually easier to use and more concise than using array subscripts to perform the same task. Listing 11.5 shows how you do this.

## Input

**LISTING 11.5** pointerstep.c: Accessing Successive Array Elements by Incrementing a Pointer

```
1: /* pointerstep.c--Demonstrates stepping through an array */
2: /* array of structures using pointer notation. */
3:
4: #include <stdio.h>
5:
6: #define MAX 4
7:
8: /* Define a structure, then declare and initialize */
9: /* an array of 4 structures. */
10:
11: struct part {
12:     short number;
13:     char name[12];
14: } data[MAX] = { {1, "Thomas"},
15:     {2, "Christopher"};
```
16:     {3, "Andrew"},
17:     {4, "Benjamin"}
18:     };
19:
20:  /* Declare a pointer to type part, and a counter variable. */
21:
22:  struct part *p_part;
23:  int count;
24:
25: int main( void )
26: {
27:     /* Initialize the pointer to the first array element. */
28:
29:     p_part = data;
30:
31:     /* Loop through the array, incrementing the pointer */
32:     /* with each iteration. */
33:
34:     for (count = 0; count < MAX; count++)
35:     {
36:         printf("At address %p: %d %s\n", p_part, p_part->number);
37:
38:         p_part->name);
39:     }
40:
41:     return 0;
42: }

# Output

At address 0x2496: 1 Thomas
At address 0x2510: 2 Christopher
At address 0x2524: 3 Andrew
At address 0x2538: 4 Benjamin

# Analysis

First, on lines 1 through 18, this program declares and initializes an array of structures called data. A pointer called p_part is then defined on line 22 to be used to point to the data structure. The main() function's task on line 29 is to set the pointer, p_part, to point to the structure that was declared. All the elements are then printed using a for loop on lines 34 through 39 that increments the pointer with each iteration. The program also displays the address of each element.

Look closely at the addresses. The precise values might differ on your system, but they are in equal sized increments—just the size of the structure. This clearly illustrates that incrementing a pointer increases it by an amount equal to the size of the object it points to.

## Passing Structures as Functions

Like other data types, a structure can be passed as an argument to a function. Listing 11.6 shows how to do this. This program is a modification of the program shown in 11.3. It uses a function to display information on the screen that is passed in, whereas Listing 11.3 uses statements in main().

# Input

**LISTING 11.6** struct.c: Passing a Structure as a Argument

```
1: // struct.c--Demonstrates passing a structure to a function.
2:
3: #include <stdio.h>
4:
5: /* Declare and define a structure to hold the data. */
6:
7: struct data {
8:     float amount;
9:     char fname[30];
10:    char lname[30];
11: } rec;
12:
13: /* The function prototype. The function has no return value, */
14: /* and it takes a structure of data type as its argument. */
15:
16: void print_rec(struct data display);
17:
18: int main( void )
19: {
20:     /* Input the data from the keyboard. */
21:
22:     printf("Enter the donor's first and last names,\n");
23:     printf("separated by a space: ");
```

# Output

Enter the donor's first and last names, separated by a space: Jayne Hatton
Enter donation amount: 450

Donor Jayne Hatton gave $450.00.

# Analysis

Looking at line 16, you see the function prototype for the function that is to receive the structure. As you would with any other data type that was going to be passed, you must include the proper arguments. In this case, it is a structure of type data. This is repeated in the header for the function in line 3. When calling the function, you have to pass only the structure instance name—in this case, rec (line 10). That's all there is to it. Passing a structure to a function isn't very different from passing a simple variable.

You can also pass a structure to a function by passing the structure's address (that is, a pointer to the structure). In fact, in older versions of C, this was the only way to pass a structure as an argument. It's not necessary, but you might see older programs that still use this method. If you use a pointer to a structure as an argument, remember that you must use the indirect membership operator (->) to access members in the function. You can also use the dot operator if you format the reference as (*ptr).member.

| DO | DON'T |
|---|---|
| take advantage of a pointer to a structure—especially when using arrays of structures. | DON'T confuse arrays with structures. |
| use the indirect membership operator (->) when working with a pointer to a structure. | DON'T forget that when you increment a pointer, it moves a distance equivalent to the size of the data to which it points. In the case of a pointer to a structure, this is the size of the structure. |

## Understanding Unions

Unions are similar to structures. A union is declared and used in the same ways that a structure is. A union differs from a structure in that only one of its members can be used at a time. The reason for this is simple. All the members of a union occupy the same area of memory—they are laid on top of one another.

## Defining, Declaring, and Initializing Unions

Unions are defined and declared in the same fashion as structures. The only difference in the declarations is that the keyword union is used instead of struct. To define a simple union of a char variable and an integer variable, you would write the following:

```
union shared
{
    char c;
    int i;
}
```

This union, shared, can be used to create instances of a union that can hold either a character value or an integer value i. This is an OR condition. Unlike a structure that would hold both values, the union can hold only one value at a time. Figure 11.7 illustrates how the shared union would appear in memory.

## FIGURE 11.7 shared.i The union can hold only one value at a time.

![](img/d572877e6f876c745d39250550bf01c5_289_0.png)

A union can be initialized on its declaration. Because only one member can be used at a time, only one member can be initialized. To avoid confusion, only the first member of the union can be initialized. The following code shows an instance of the shared union being declared and initialized:

```
union shared generic_variable = {'@'};
```

Notice that the generic_variable union was initialized just as the first member of a structure would be initialized.

## Accessing Union Members

Individual unions can be used in the same way that structure members can be used—by using the member operator (.). However, there is an important difference in accessing union members. Only one union member should be accessed at a time. Because union stores its members on top of each other, it's important to access only one member at a time. Listing 11.7 presents an example.
