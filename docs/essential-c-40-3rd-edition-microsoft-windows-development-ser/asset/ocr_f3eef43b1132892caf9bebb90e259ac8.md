# BEGINNER TOPIC

# Choosing between for and while Loops

Although you can use the two statements interchangeably, generally you would use the for loop whenever there is some type of counter, and the total number of iterations is known when the loop is initialized. In contrast, you would typically use the while loop when iterations are not based on a count or when the number of iterations is indeterminate when iterating commences.

# The foreach Loop

The last loop statement within the C# language is foreach. foreach is designed to iterate through a collection of items, setting a variable to represent each item in turn. During the loop, operations may be performed on the item. One feature of the foreach loop is that it is not possible to accidentally miscount and iterate over the end of the collection.

The general form of the foreach statement is as follows:

```
foreach(type variable in collection)
statement;
```

Here is a breakdown of the foreach statement.

+   - type is used to declare the data type of the variable for each item within the collection.
+   - variable is a read-only variable into which the foreach construct will automatically assign the next item within the collection. The scope of the variable is limited to the foreach loop.
+   - collection is an expression, such as an array, representing multiple items.
+   - statement is the code that executes for each iteration within the foreach loop.

Consider the foreach loop in the context of the simple example shown in Listing 3.45.