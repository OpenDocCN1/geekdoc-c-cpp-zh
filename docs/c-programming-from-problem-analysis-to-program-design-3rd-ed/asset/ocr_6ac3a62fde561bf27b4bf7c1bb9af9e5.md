In previous chapters, you were introduced to the basics of programming. You learned about the three programming constructs of simple sequence, selection, and iteration. You learned to handle data and declare memory locations to store and access values using an identifier. In this chapter, you will discover how to work with collections of data that are referenced by a single identifier name. You will learn about one type of collection, called an array, which is similar to a vector in mathematics or cells in a spreadsheet in that each entry can be referenced by the location of the item in the collection. You will create arrays that can hold multiple data values. Using an index to reference the location of the item, you will learn how to access single values and iterate through collections to process all the values. You will learn about special properties and methods of the .NET Array class and learn how to define arrays of user-defined objects. You will learn how to pass arrays to methods and how methods can have arrays as their return type.

# ARRAY BASICS

It is not always efficient to have unique names for every memory location. Suppose, for example, you have 14 homework scores. A unique identifier could be associated with each one. The declaration would look something like the following:

```
int score1,
    score2,
    ...
    score14;
```

If you want to allow the user to input the values and compute the average, 14 separate prompts to input a score, 14 calls to the ReadLine() method, and 14 parse or convert method calls would need to be written. Another option you are probably considering would be to use a loop. You could write a loop body to input a value into a memory location and add that value to an accumulator. The loop body could read all 14 values. If you use the same memory location to store the second value, the second value replaces the first value. The third value replaces the second, and so on. This seems to be the most reasonable approach. Instead of having 14 distinct ReadLine() statements, you could place one method call inside a counter-controlled loop and have it execute 14 times.

If the only output needed is the average, a loop with a single variable is the most efficient way to write your algorithm. However, what if you want to determine and display how far each score is from the average of all scores? Or, what if you want to drop the lowest score? Or, what if you need all the values for additional processing later in the program? For these situations, using a single value presents a problem. The average cannot be calculated until you accumulate all the values. If all values are read into a single memory location, the first score is no longer available as soon as the second score is read. There is no way to determine how far the first value is from the average, until you calculate the average. For this type of problem, it would be best to retain the values in memory in addition