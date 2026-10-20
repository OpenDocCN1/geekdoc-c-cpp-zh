
## A statement that creates a null array

```csharp
string[] initials = null;
```

## A statement that will throw a NullReferenceException

```csharp
string firstInitial = initials[0].ToUpper();
```

## Code that uses if statements to prevent a NullReferenceException

```csharp
if (initials != null)
{
    if (initials[0] != null)
    {
        string firstInitial = initials[0].ToUpper();
    }
}
```

## A statement that uses null-conditional operators to prevent a NullReferenceException

```csharp
string firstInitial = initials?[0]?.ToUpper();
```

## A statement that uses a nullable type

```csharp
int? length = initials?.Length;
```

## Description

- If you try to access a member or element of an object that contains a null value, a NullReferenceException will occur. That’s the case with the second example above, since the array it accesses contains a null value.
- One way to prevent a NullReferenceException is to use an if statement to check for a null value before accessing a member or element of the object.
- An easier way to prevent a NullReferenceException is to use the *null-conditional operator (?)* that became available with C# 6.0. This operator checks the object or element that precedes it for a null value. If it finds a null value, no further operations take place and a null value is returned.
- Because the null-conditional operator can cause a null value to be returned, the variable that the return value is assigned to must provide for nulls. If the variable is a value type, that means it must be defined as a nullable type.
- You can use the null-conditional operator with any object and any element. That includes collection objects and elements like the ones you’ll learn about later in this chapter, as well as custom objects and elements like the ones you’ll learn about in section 3.

## More ways to refer to array elements

Figure 8-13 presents some additional skills for referring to the elements of an array that were introduced with C# 8.0. To start, you can refer to an element by its index from the end of the array by coding the ^ operator before the index. To illustrate how this works, the first example presents an array of eight decimals that’s used by the other examples in this figure. Then, the second example shows how to retrieve the second element from the end of the array. Note that when you refer to an element from the end of an array, the index of the last element is 1, not 0 as you might expect.

You can also refer to a range of elements. To do that, you use the range operator (..) as illustrated by the statements in the third example. Here, the first statement refers to the elements in the range that starts with index 0 and ends with index 2. Note that the starting index is inclusive, so the element with that index is included in the range, but the ending index is exclusive, so the element with that index isn’t included in the range. Also note that the elements retrieved by this statement are stored in a variable that’s declared with the var keyword. That way, the range can be stored in a variable with the appropriate type, whether that’s an array or an individual variable.

When you refer to a range of elements, you can omit the starting index, the ending index, or both the starting and ending indexes. For instance, the second statement in this example doesn’t include a starting index, so it defaults to 0. Because of that, it gets the same range as the first statement.

The third statement doesn’t include an ending index, so it defaults to ^0. This refers to the element after the last element in the array. So the range in this example includes the element with index 6 through the last element in the array, which has index 7.

The fourth statement doesn’t include a starting or ending index. Because of that, the range includes all of the elements in the array. In most cases, you won’t use this technique unless you need to create a copy of the array. Instead, you can just refer to the original array.

The last statement in this example shows how to code a range that includes an index from the end of the array. Here, the starting index is 3 and the ending index is ^2. This is the same as coding 3..6, which is much easier to understand. Because of that, you won’t typically use indexes from the end of an array in a range unless it’s the index that refers to the element after the last element in the array (^0).

You can use a range to copy selected elements from one array to another instead of using the Array class. If you just need to process the elements without storing them in a separate array, though, you can use a foreach loop as shown in the fourth example. Here, instead of just naming the array as you saw earlier in this chapter, you include the range of elements you want to process.

The last example shows that you can store an index in a variable with the Index type, and you can store a range in a variable with the Range type. Then, you can use those variables to refer to the index and range.

### The array that’s used in the examples

```csharp
decimal[] sales = { 22125.67m, 25362.35m, 21478.93m, 27495.72m, 26405.61m, 19476.29m, 31837.56m, 28649.01m };
```

### How to refer to an element from the end of an array

```csharp
decimal previousMonthSales = sales[^2]; // 31837.56
```

### How to refer to a range of elements

**By including starting and ending indexes**

```csharp
var firstQtrSales = sales[0..3]; // indexes 0 through 2
```

**By including just an ending index**

```csharp
var firstQtrSales = sales[..3]; // indexes 0 through 2
```

**By including just a starting index**

```csharp
var secondHalfSales = sales[6..]; // indexes 6 through 7
```

**By including no starting or ending index**

```csharp
var YTDSales = sales[..]; // indexes 0 through 7
```

**By including an index from the end of the array**

```csharp
var secondQtrSales = sales[3..^2]; // indexes 3 through 5
```

### How to use a range in a foreach loop

```csharp
totalSales = 0.0m;
foreach (decimal sale in sales[3..6]) // indexes 3 through 5
{
    totalSales += sale;
}
```

### How to use the Index and Range types (.NET Core 3.0 and later only)

```csharp
Index previousMonthIndex = ^2;
decimal previousMonthSales = sales[previousMonthIndex]; // 31837.56
```

```csharp
Range secondQtrRange = 3..6;
var secondQtrSales = sales[secondQtrRange]; // indexes 3 through 5
```

### Description

- With C# 8.0 and later, you can refer to an element from the end of an array by coding the ^ operator before the index. The element indexes start with ^1 for the last element, ^2 for the next to last element, and so on.
- With C# 8.0 and later, you can also refer to a range of elements in an array. To do that, you code the first index, the range operator (..), and one past the last index.
- To refer to one element past the last element in an array, you code ^0.
- If you omit the first index in a range, it defaults to 0. If you omit the last index in a range, it defaults to ^0.
- You can also store an index in a variable with the Index type, and you can store a range in a variable with the Range type. Then, you can use these variables in place of an index or range.

## How to work with collections

Like an array, a *collection* can hold one or more elements. Unlike arrays, collections don’t have a fixed size. Instead, the size of a collection is increased automatically when elements are added to it. In addition, most types of collections provide methods you can use to change the capacity of a collection. In other words, collections are *mutable*. As a result, collections are usually more appropriate and can usually manage system resources better than arrays when you need to work with a varying number of elements.

In the topics that follow, you’ll learn how to use five types of collections: lists, sorted lists, queues, stacks, and array lists. Although the .NET Framework provides for other collections, these are the ones you’ll use most often.

### Commonly used collection classes

.NET Core provides two types of collection classes. First, it includes collection classes that can store any type of object. As a result, the collections created from these classes are sometimes referred to as *untyped collections*. In fact, you can store different types of objects in the same collection, even though that’s usually not a good idea. However, if you accidentally write code that adds the wrong type of object to an untyped collection, it will result in an error that won’t be discovered until you run the application.

The second type of collection classes prevents errors like this by using a feature known as *generics* to allow you to create *typed collections*. With a typed collection, you specify the data type in angle brackets (`<>`) after the name of the collection class. Then, you can only store objects of the specified data type in that collection, and any errors will be discovered when you attempt to compile the application.

Figure 8-14 shows four of the most commonly used typed and untyped collections. The classes for the typed collections are stored in the System.Collections.Generic namespace. And the classes for the untyped collections are stored in the System.Collections namespace.

As you’ll see in the next figure, typed collections have several advantages over untyped collections. As a result, you’ll typically want to use typed collections for most new development. However, you may need to use untyped collections when working with legacy applications.
