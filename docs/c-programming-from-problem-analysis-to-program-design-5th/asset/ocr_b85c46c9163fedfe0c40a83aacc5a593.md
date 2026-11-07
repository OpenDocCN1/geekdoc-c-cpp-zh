![](bbox=[0.182, 0.107, 0.912, 0.333])

**FIGURE 11-1**  `structs newStudent and student`

> > **NOTE** You can also declare `struct` variables when you define the `struct`. For example, consider the following statements:

```
struct studentType
{
    string firstName;
    string lastName;
    char courseGrade;
    int testScore;
    int programmingScore;
    double GPA;
} tempStudent;
```

These statements define the `struct` `studentType` and also declare `tempStudent` to be a variable of type `studentType`.

Typically, in a program, a `struct` is defined before the definitions of all of the functions in the program so that the `struct` can be used throughout the program. Therefore, if you define a `struct` and also simultaneously declare a `struct` variable (as in the preceding statements), then that `struct` variable becomes a global variable and thus can be accessed anywhere in the program. Keeping in mind the side effects of global variables, you first should only define a `struct` and then declare the `struct` variables.

# Accessing `struct` Members

In arrays, you access a component by using the array name together with the relative position (index) of the component. The array name and index are separated using square brackets. To access a structure member (component), you use the structure variable name together with the member name; these names are separated by a dot (period). The syntax for accessing a `struct` member is:

```
structVariableName.memberName
```