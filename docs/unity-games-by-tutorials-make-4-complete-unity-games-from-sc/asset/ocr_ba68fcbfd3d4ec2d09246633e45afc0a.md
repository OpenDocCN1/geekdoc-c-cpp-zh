Add the following:

```
Console.WriteLine(writers[2]);
```

Click the Run it button and you will see Eric's name printed to the console.

![](bbox=[0.423, 0.187, 0.576, 0.237])

C# starts counting with zero, so the second element of the array is accessed by 1. You can replace a value in the array.

Add the following:

```
writers[0] = "Ray";
```

This replaces the first string in the array with another string. Now, when you access the first element, it will read: Ray instead of Anthony.

Unfortunately, you cannot remove indexes. Once you define an array with four elements, it will always contain four elements. If you want to copy the array to another array, you'll need to create a new array and copy all the values.

# Control flow

When writing your programs, you'll need to control how the code flows based on certain values. If your if statement will get started. Add the following underneath the previous code:

```
if (likesPizza == false)
{
    Console.WriteLine("You monster!");
}
```

Like other languages, the statement is evaluated and the code is run between the braces. When assigning variables, C# also contains a ternary operator. Add the following:

```
bool isMonster = (likesPizza == true) ? false : true;
```

This is just a shorthand for assigning a value. You can think of it as a condensed statement.

Like other languages, you also have a bevy of loops at your disposal. The first loop is the traditional for loop.