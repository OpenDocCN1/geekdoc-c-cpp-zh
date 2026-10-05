
# How to work with one-dimensional arrays

You can use an array to store a set of related data. Since a one-dimensional array is the simplest type of array, you'll start by learning how to create and use one-dimensional arrays.

## How to create an array

To create a one-dimensional array, you use the syntax shown in figure 8-1. As you can see, you can create an array using either one or two statements. This is similar to the techniques you use to declare variables, except that you code square brackets after the data type to indicate that the variable refers to an array. Within the second set of brackets, you code a number that indicates the length, or size, of the array. This specifies the number of elements that the array can hold.

Notice that you also use the new keyword to create an array. That's because, as you'll learn later in this chapter, arrays are created from the Array class's by the .NET Framework. So when you create an array, you're creating an instance of this class.

When you create an array, each element in the array is initialized to a default value. This value depends on the data type of the array as indicated by the table in this figure. Specifically, numeric types are set to zero, char types are set to the null character, Boolean types are set to false, DateTime types are set to 12:00:00 AM on January 1, 0001, and reference types are set to null. In the next figure, you'll learn how to assign new values to the elements of an array.

In most cases, all of the elements in an array will contain the same type of data, and you'll declare the array with that data type. However, if you don't know what type of data an array will contain, you can declare it with the object data type. Then, each element can contain data of any type.

# Chapter 8 How to work with arrays and collections 215

## The syntax for creating a one-dimensional array

With two statements

```csharp
type[] arrayName;
// declaration statement
arrayName = new type[arrayLength];
// assignment statement
```

With one statement

```csharp
type[] arrayName = new type[arrayLength];
```

## How to create an array of decimal types

With two statements

```csharp
decimal[] totals;
totals = new decimal[4];
```

With one statement

```csharp
decimal[] totals = new decimal[4];
```

## Other examples

An array of strings

```csharp
string[] description = new string[3];
```

Two arrays in one statement

```csharp
const int MaxCount = 100;
decimal[] prices = new decimal[MaxCount];
discountPercentages = new decimal[MaxCount];
```

## Default values for array elements

| Data type | Default value |
|---|---|
| numeric | (zero) |
| char | '0' (the null character) |
| Boolean | false |
| DateTime | 01/01/0001 00:00:00 |
| reference types | null |

## Description

- An array can store one or more elements. The length, or size, of an array is the number of elements in the array.
- When you create an array, each element of the array is set to a default value. If the array contains value types, each element is set to the value shown above. If the array contains reference types, each element is set to null.

![](img/3148667e42d4db35b3d08576aaa1fa01_234_0.png)

## How to assign values to the elements of an array

8-2 shows how to assign values to the elements of an array. As the syntax at the top of this figure indicates, you refer to an element in an array by coding the array name followed by its index in brackets. The index that you specify must be 0, which refers to the first element in the array, to the upper bound of the array, which is one less than the length of the array.

To understand how this works, take a look at the first example in this figure. This example declares an array of decimals that contains four elements. Then, it uses indexes 0 through 3 to assign values to those four elements. Here, the length of the array is 4, and the upper bound of the array is 3. Note that if you use an index that's greater than the upper bound, an IndexRangeException will be thrown.

The syntax and examples at the bottom of this figure show how to declare an array and assign values to its elements in a single statement. Here, you start the array declaration as before, but you code a list of values after the declaration. Notice that when you use this technique, you can omit the keyword and the type specification. C# automatically sets the length of the array to the number of elements within the braces. If you include the data type and length specification, however, they must match the list of values you provide.

The next three statements show how this works. The first statement creates the same array as the first example in this figure. Notice that this statement specifies the data type and length of the array. The second statement creates the same array, but the data type and length are omitted. Finally, the third statement creates the same array of strings that was created by the second example in this figure. Like the second statement, the data type and length are omitted from this statement.

You may remember from chapter 4 that you can use the var keyword to declare a variable that infers its type from the value's assigned to it. You can also use the var keyword to declare an array when you initialize it with a list of values. However, you cannot use the var keyword when you declare an array without initializing it. This is because the compiler needs to know the type of the array, and it cannot determine it if there are no values provided.

If you use the var keyword, the compiler infers the type of the array from the values in the list. If the values are not all of the same type, the compiler will throw an error.

PAGE 236
# Chapter 8 How to work with arrays and collections

## The syntax for getting values from an array

To get a value from an array, you use the array name followed by the index in brackets. The index must be between 0 and the length of the array minus one. If you use an index that is out of range, an IndexRangeException will be thrown.

```csharp
type value = arrayName[index];
```

## Examples of getting values from an array

```csharp
decimal[] totals = { 10.5m, 20.0m, 30.2m, 40.0m };
decimal firstTotal = totals[0];
decimal secondTotal = totals[1];
decimal thirdTotal = totals[2];
decimal fourthTotal = totals[3];
```

```csharp
string[] names = { "Alice", "Bob", "Charlie", "David" };
string firstName = names[0];
string secondName = names[1];
string thirdName = names[2];
string fourthName = names[3];
```

## How to change values in an array

To change a value in an array, you use the array name followed by the index in brackets and then assign a new value to it.

```csharp
arrayName[index] = value;
```

## Examples of changing values in an array

```csharp
decimal[] totals = { 10.5m, 20.0m, 30.2m, 40.0m };
totals[0] = 15.0m;
totals[1] = 25.0m;
totals[2] = 35.0m;
totals[3] = 45.0m;
```

```csharp
string[] names = { "Alice", "Bob", "Charlie", "David" };
names[0] = "Eve";
names[1] = "Frank";
names[2] = "Grace";
names[3] = "Heidi";
```

## How to iterate through the elements of an array

There are several ways to iterate through the elements of an array. The most common way is to use a for loop.

```csharp
for (int i = 0; i < arrayName.Length; i++)
{
    // use arrayName[i]
}
```

Another way is using a foreach loop, which is simpler if you don't need the index.

```csharp
foreach (type element in arrayName)
{
    // use element
}
```

## Examples of iterating through an array

```csharp
decimal[] totals = { 10.5m, 20.0m, 30.2m, 40.0m };
decimal sum = 0;
for (int i = 0; i < totals.Length; i++)
{
    sum += totals[i];
}
foreach (decimal total in totals)
{
    sum += total;
}
```

```csharp
string[] names = { "Alice", "Bob", "Charlie", "David" };
foreach (string name in names)
{
    Console.WriteLine(name);
}
```
