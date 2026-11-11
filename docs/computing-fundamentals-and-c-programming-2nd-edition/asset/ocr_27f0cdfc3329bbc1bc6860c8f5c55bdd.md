We can also use **scanf** to give the values through the keyboard.

```
```c
scanf("%s\n", book1.title);
scanf("%d\n", &book1.pages);
```
```

are valid input statements.

# ## WORKED-OUT PROBLEM 12.2

Define a structure type, **struct personal** that would contain person name, date of joining and salary. Using this structure, write a program to read this information for one person from the keyboard and print the same on the screen.

Structure definition along with the program is shown in Fig. 12.1. The **scanf** and **printf** functions illustrate how the member operator '.' is used to link the structure members to the structure variables. The variable name with a period and the member name is used like an ordinary variable.

```
```text
Program

struct personal
{
    char name[20];
    int day;
    char month[10];
    int year;
    float salary;
};
main()
{
    struct personal person;

    printf("Input Values\n");
    scanf("%s %d %s %d %f",
        person.name,
        &person.day,
        person.month,
        &person.year,
        &person.salary);
    printf("%s %d %s %d %f\n",
        person.name,
        person.day,
        person.month,
        person.year,
        person.salary);
}

Output

Input Values
M.L.Goel 10 January 1945 4500
M.L.Goel 10 January 1945 4500.00
```
```

*Fig. 12.1 Defining and accessing structure members*