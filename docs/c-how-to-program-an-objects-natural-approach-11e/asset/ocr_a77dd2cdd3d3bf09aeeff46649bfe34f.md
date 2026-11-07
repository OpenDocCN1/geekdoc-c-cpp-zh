Generally, each program that uses random numbers creates one random-number generator engine, seeds it, then uses it throughout the program. In this program, only function rollDice needs access to the random-number generator, so lines 57–59 define the objects random_device, default_random_engine and uniform_int_distribution as static local variables. Declaring the objects in lines 57–59 static ensures they are created only the first time rollDice is called. They are then reused in subsequent rollDice calls. Unlike other local variables, which exist only until a function call terminates, static local retain their values between function calls. The expression rd() in line 58 gets a nondeterministic random integer from the random_device object and uses it to seed the default_random_engine, enabling the program to produce different results each time we execute it.

# Additional Notes Regarding Scoped enums

Qualifying an enum class's constant with its type name and :: explicitly identifies the constant as being in that type's scope. If another enum class contains the same identifier, it's always clear which constant is being used because the type name and :: are required. In general, use unique enum constant values to help prevent hard-to-find logic errors.

The following scoped enumeration creates the user-defined enum class type Month with enumeration constants representing the months of the year:

```
    enum class Month { jan = 1, feb, mar, apr, may, jun, jul, aug,
        sep, oct, nov, dec};
```

Any constant can be assigned an integer value in the enum class definition. Subsequent constants have a value 1 higher than the preceding constant until the next explicit setting. The first value in the preceding enumeration is explicitly set to 1, so the remaining values increment from 1, resulting in the values 1 through 12. You may assign the same value to multiple constants.

# C++20: using enum Declaration

If the type of an enum class's constants is obvious based on the context in which they're used—such as in our craps example—C++20's using enum declaration^16 allows you to reference an enum class's constants without the type name and scope-resolution operator (::). For example, adding the following statement after the enum class declaration

```
    using enum Status;
```

would allow the rest of the program to use keepRolling, won and lost, rather than Status::keepRolling, Status::won and Status::lost, respectively. You also may use an individual enum class constant with a declaration of the form

```
    using Status::keepRolling;
```

This would allow your code to use keepRolling without the Status:: qualifier. Generally, such using declarations should be placed inside the block that uses them.

16. Gasper Ažman and Jonathan Müller, “Using Enum,” July 16, 2019. Accessed April 14, 2023. http://wg21.link/p1099r5.