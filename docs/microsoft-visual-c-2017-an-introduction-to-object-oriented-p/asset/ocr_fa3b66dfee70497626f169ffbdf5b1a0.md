# Searching an Array Using a Loop

When you want to determine whether a variable holds one of many possible valid values, option is to use if statements to compare the variable to valid values. For example, suppose that company manages 10 items. When a customer places an order for an item, you need to determine whether the item number is valid. If valid item numbers are sequential, say 101 through 110, then the following simple if statement uses an AND operator to verify the order number and set a Boolean field to:

```
if(itemOrdered == 101 && itemOrdered <= 110)
isValidItem = true;
```

If the item numbers are nonsequential, however—for example, 101, 108, 201, 213, 266, 304, and so on—you must code the following deeply nested if statement or a lengthy OR comparison to determine the validity of an item number:

```
if(itemOrdered == 101)
isValidItem = true;
else if(itemOrdered == 108)
isValidItem = true;
else if(itemOrdered == 201)
isValidItem = true;
// and so on
```

Instead of creating a series of if statements, a more elegant solution to determining whether a value is valid is to compare it to a list of values in an array. For example, you can initialize an array with the valid values using the following statement:

```
int[] validValues = {101, 108, 201, 213, 266, 304, 311, 409, 412};
```

> You might prefer to declare the validValues array as a constant because, presumably, the valid numbers should not change during program execution. In C# you must use the keywords static and readonly prior to the constant declaration. To keep these examples simple, all arrays in this chapter are declared as variable arrays.

After the validValues array is declared, you can use either a for loop or a while loop to search whether the item variable matches any of the array entries.

![](bbox=[0.104, 0.616, 0.163, 0.663])