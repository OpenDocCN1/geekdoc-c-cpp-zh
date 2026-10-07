246 LESSON 11 Implementing Structures, Unions, and TypeDefs

```
int first_three;
char dash1;
int second_two;
char dash2;
int last_four;
};
```

/* Use the structure template */
struct SSN customer_ssn;

# Example 2

```
/* Declare a structure and instance together */
struct date {
char month[2];
char day[2];
char year[4];
} current_date;
```

# Example 3

```
/* Declare and initialize a structure */
struct time {
int hours;
int minutes;
int seconds;
time of_birth = { 8, 45, 0 };
```

# Using Structures That Are More Complex

Now that you have been introduced to simple structures, you can go on to the interesting and complex types of structures. These are structures that contain other structures as members and structures that contain arrays as members.

# Including Structures Within Other Structures

As mentioned earlier, a C structure can contain any of C’s data types. The preceding example can be extended to illustrate this.

Assume that your graphics program has to deal with rectangles. A rectangle can be defined by the coordinates of two diagonally opposite corners. You've already seen how to define a structure that can hold the two coordinates required for a single point. You need two such structures to define a rectangle. You can define a structure as follows (assuming, of course, that you have already defined the coord structure):