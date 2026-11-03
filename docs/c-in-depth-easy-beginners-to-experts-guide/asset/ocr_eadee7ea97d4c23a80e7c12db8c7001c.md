definition (also called as template)

+   3. The tag name can be declared with the structure definition or even later in the main function.
+   4. The memory is allotted to the variables and not to the members of a structure.

# Using the members -

In an array we can access individual elements of the array using a subscript operator [ ].

Structures use a different scheme. It uses a dot or period operator (.). So to refer to marks in the above structure:

*s1.marks*

Here the variable name is given before the dot and the name of the member after that.

# Mind Wash Drill-

The elements of a structure are always stored in contiguous memory locations.

```
```c
struct student
{
    int roll;
    char grade;
    int marks;
};
    main()
{
    struct student s1={2, ‘A’, 89};
    printf(“Address of roll=%u”,&s1.roll);
    printf(“Address of grade=%u”,&s1.name);
    printf(“Address of marks=%u”,&s1.marks);
}
```
```