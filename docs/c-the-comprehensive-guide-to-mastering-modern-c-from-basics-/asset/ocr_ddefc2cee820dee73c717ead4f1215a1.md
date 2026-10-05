```
notices
Person jack { .name = "Jack", .age = 23, .city = "Dallas" }; // okay
Person jimmi { .name = "Jimmy", .age = 48 }; // okay, not all
specified
Person carl { "Carl", .age = 53 }; // all designated or none
Person paul { .age = 34, .name = "Paul", .city = "Reno" }; // swapped
Person jim.name="Jim", .age=34, .city="NYC"}; // not with
parenthesis
```

# ### Listing 12.3 With designated initializers, you specify the elements to be set.

For paul, the designated initializers must be specified in the correct order. As with jimmi, you can also omit fields, which will then be value-initialized. However, you must not mix fields with and without designated names, as carl.

> Warning about Parentheses
nYou can also write the initialization elements in parentheses, like string name("x"). However, if you have no element for the list, then you must not use the parentheses: string() unfortunately means something else (a function declaration). Therefore, it is better to consistently initialize with curly brackets: string name{} is a correct initialization.

In few cases, initialization with curly brackets and parentheses means something different; std::vector is one such exception.