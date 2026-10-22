Here is some sample output:

```
How many pounds to a firkin of butter?
14
No luck, my friend. Try again.
56
You must have looked it up!
```

(We did.)

Note how the second value for units was read by the critic() function, yet main() also knew the new value when it finished the while loop. So both the main() function and the critic() function use the identifier units to access the same variable. In C terminology, we say that units has file scope, external linkage, and static storage duration.

We made units an external variable by defining it outside of (that is, external to) any function definition. That's all you need to do to make units available to all the subsequent functions in the file.

Let's look at some of the details. First, declaring units where it is declared makes it available to the functions below it without any further action taken. Therefore, critics() uses the units variable.

Similarly, nothing needed to be done to give main() access to units. However, main() does have the following declaration in it:

```
extern int units;
```

In the example, this declaration is mainly a matter of documentation. The storage class specifier extern tells the compiler that any mention of units in this particular function refers to a variable defined outside the function, perhaps even outside the file. Again, both main() and critic() use the externally defined units.

# External Names

The C99 and C11 standards require compilers to recognize the first 63 characters for local identifiers and the first 31 characters for external identifiers. This revises the previous requirement of recognizing the first 31 characters for local identifiers and the first six characters for external identifiers. It's possible that you may be working with the old rules. The reason the rules for names of external variables are more restrictive than for local variables is that external names need to comply with the rules of the local environment, which may be more limiting.

# Definitions and Declarations

Let's take a longer look at the difference between defining a variable and declaring it. Consider the following example:

```
int tern = 1;        /* tern defined */
main()
{
    external int tern; /* use a tern defined elsewhere */
```