# # 10.9 TABLE OF STRINGS

LO 10.4

We often use lists of character strings, such as a list of the names of students in a class, list of the names of employees in an organization, list of places, etc. A list of names can be treated as a table of strings and a two-dimensional character array can be used to store the entire list. For example, a character array `student[30][15]` may be used to store a list of 30 names, each of length not more than 15 characters. Shown below is a table of five cities:

<table><tr><td>C</td><td>h</td><td>a</td><td>n</td><td>d</td><td>i</td><td>g</td><td>a</td><td>r</td><td>h</td></tr><tr><td>M</td><td>a</td><td>d</td><td>r</td><td>a</td><td>s</td><td></td><td></td><td></td><td></td></tr><tr><td>A</td><td>h</td><td>m</td><td>e</td><td>d</td><td>a</td><td>b</td><td>a</td><td>d</td><td></td></tr><tr><td>H</td><td>y</td><td>d</td><td>e</td><td>r</td><td>a</td><td>b</td><td>a</td><td>d</td><td></td></tr><tr><td>B</td><td>o</td><td>m</td><td>b</td><td>a</td><td>y</td><td></td><td></td><td></td><td></td></tr></table>

This table can be conveniently stored in a character array `city` by using the following declaration:

```
```c
char city[ ][ ]
{
    "Chandigarh",
    "Madras",
    "Ahmedabad",
    "Hyderabad",
    "Bombay"
} ;
```
```

To access the name of the ith city in the list, we write

```
```
city[i-1]
```
```

and therefore, `city[0]` denotes “Chandigarh”, `city[1]` denotes “Madras” and so on. This shows that once an array is declared as two-dimensional, it can be used like a one-dimensional array in further manipulations. That is, the table can be treated as a column of strings.

# ## WORKED-OUT PROBLEM 10.11

H

Write a program that would sort a list of names in alphabetical order.

A program to sort the list of strings in alphabetical order is given in Fig. 10.12. It employs the method of bubble sorting described in Case Study 1 in Chapter 9.

Program

```
```c
#define ITEMS 5
#define MAXCHAR 20
main( )
{
    char string[ITEMS][MAXCHAR], dummy[MAXCHAR];
    int i = 0, j = 0;
```
```