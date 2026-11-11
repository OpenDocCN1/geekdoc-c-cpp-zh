Java provides the *conditional* ?: operator that selects a value, depending on a Boolean expression. The expression *condition* ? *expression1* : *expression2* evaluates to the first expression if the condition is true, to the second expression otherwise. For example,

```
```
x < y ? x : y
```
```

gives the smaller of x and y.

# ### 3.5.9 Switch Expressions

If you need to choose among more than two values, then you can use a switch expression (as of Java 14). It looks like this:

```
```
String seasonName = switch (seasonCode)
{
    case 0 -> "Spring";
    case 1 -> "Summer";
    case 2 -> "Fall";
    case 3 -> "Winter";
    default -> "???";
};
```
```

The case labels can also be strings or constants of an enumerated type.

> > **NOTE:**
> > The switch expression, like every expression, has a value. Note the -> arrow preceding the value in each branch.

> > **NOTE:**