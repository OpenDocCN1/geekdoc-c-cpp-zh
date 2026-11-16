The structure can be depicted as follows:

| name | gpa | year |
|---|---|---|
| Sammie | 3.85 | 2016 |

# Referencing elements of a struct .

We now have the same problem with structs as we had with arrays. How do we reference individual elements (called components or fields) of a struct? With arrays we used subscripts. With structs we use a period, also known as a direct component selection operator (or, more simply, the selection operator, for short).

For example, we can give values to each of the fields of the `struct` as follows:

```
```c
// struct2.c
s1.gpa = 3.85;
s1.year = 2016;
strcpy(s1.name, "Sammie");
```
```

# Example: Date structure.

Suppose that we have a need to keep track of various dates. We can define a Date data type as follows:

```
```c
// struct3.c
typedef struct {
    int month;
    int day;
    int year;
} Date;
```
```