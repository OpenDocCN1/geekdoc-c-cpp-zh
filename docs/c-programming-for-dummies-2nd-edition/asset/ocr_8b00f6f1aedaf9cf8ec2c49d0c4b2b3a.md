```
printf("%s was born on %d/%d/%d\n", president.name, president.birthday.month, president.birthday.day, president.birthday.year);

return(0);
}
```

Listing 14-4 declares two structure types: date at Line 6 and human at Line 12. Within the human structure's declaration, at Line 15 you see the date structure variable birthday declared. That's effectively how one structure is born inside another.

Line 17 creates a human structure variable, president. The rest of the code fills this structure's members with data. The method for accessing a nested structure's members is shown in Lines 20 through 22.

Exercise 14-8: Type the source code from Listing 14-4 into your editor. Build and run the program.

Exercise 14-9: From your solution for Exercise 14-8, replace the name member in the human structure with a nested structure. Name that structure id and have it contain two char array members for storing an individual's first and last names: first and last. If you do everything correctly, the reference to the president's name will be the variables president.name.first and president.name.last. Be sure to assign values to these variables in your code and display the results.

# Passing a structure to a function

As a type of variable, it's entirely possible for a function to accept a structure as an argument and return it as a value. However, this process requires that the structure be declared externally, as a global variable. The reason is that the structure's definition must be available to all functions in the source code.

The topic of global variables is avoided until Chapter 16. It's not that complex, but learning about passing and returning structures can be delayed until then.