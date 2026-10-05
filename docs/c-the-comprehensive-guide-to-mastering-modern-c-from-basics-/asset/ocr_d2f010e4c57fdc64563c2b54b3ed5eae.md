# 12.11 Using Custom Data Types

You now know how to create custom data types, how to initialize them, and how to equip them with methods. I will now show you a detailed example of how to use such custom types. Here you will see the following, among other things:

+   - How to pass and return a custom data type as a parameter
- How the type can be automatically converted
- How to output it and use it for calculations
- How it protects you from errors by providing type safety

Consider a date calculation. When dealing with a date with year, month, and day, there is always the risk of swapping the month and day, and so on. The ISO date 2024-02-05 is written in the US as 2/5/24, while it's 5.2.24 in Germany, for example. If you have a void printDate(int y, int m, int d); function and call it somewhere with printDate(28, 2, 2024), then that is obviously wrong.

This happens if you longer remember the exact meaning of the parameters. Then the program will probably not do what you intended, because you should have written printDate(2024, 2, 28). And nothing but the names of the parameters can help you use the function correctly.