Output 2.19 shows the results of Listing 2.30.

# OUTPUT 2.19

```
Enter a number: forty-two
The text entered was not a valid number.
```

The resultant value that the code parses from the input string is returned via an out parameter—in this case, number.

The key difference between Parse() and TryParse() is the fact that TryParse() won’t throw an exception if it fails. Frequently, the conversion from a string to a numeric type depends on a user entering the text. It is expected, in such scenarios, that the user will enter invalid data that will not parse successfully. By using TryParse() rather than Parse(), you can avoid throwing exceptions in expected situations. (The expected situation in this case is that the user will enter invalid data and we try to avoid throwing exceptions for expected scenarios.)

# Arrays

One particular aspect of variable declaration that Chapter 1 didn’t cover is array declaration. With array declaration, you can store multiple items of the same type using a single variable and still access them individually using the index when required. In C#, the array index starts at zero. Therefore, arrays in C# are zero based.

# BEGINNER TOPIC

# Arrays

Arrays provide a means of declaring a collection of data items that are of the same type using a single variable. Each item within the array is uniquely designated using an integer value called the index. The first item in a C# array is accessed using index 0. Programmers should be careful to specify an index value that is less than the array size. Since C# arrays are zero-based, the index for the last element in an array is one less than the total number of items in the array.