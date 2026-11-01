Just as with the array's declaration, you use parentheses in VB.NET and square brackets in C# to address the elements in the array. Note that (0) and [0] refer to the first element in the array and (1) and [1] refer to the second.

By design, arrays have a fixed size. So, given the previous example that defines an array with room for two elements, the following code will throw an error:

```
VB.NET
roles(2) = "Members"  ' Throws an error
```

```
C#
roles[2] = "Members";  // Throws an error
```

This code tries to squeeze a third role into an array that has room for only two. Obviously, that doesn't fit and you'll get an error stating that the "Index was outside the bounds of the array." But what if you need to create more room in the array at a later stage in your code at run time? In VB.NET this is pretty easy. You can use the ReDim statement:

```
ReDim Preserve roles(2)
roles(2) = "Members"  ' Works fine now
```

This line of code re-dimensions the array to its new size: an upper bound of two, thus creating room for a third element. The Preserve keyword is necessary to leave the current items in the array intact. Without it, the resized array will be empty.

C# has no direct keyword to re-dimension an array. However, you can leverage the Array class of the .NET Framework to resize the array as follows:

```
Array.Resize(ref roles, 3);  // Resize the array so it can
                              // hold three elements

roles[2] = "Members";       // Works fine now
```

Don't worry about this odd-looking syntax right now; you probably won't need it very often, because the .NET Framework offers alternatives to fixed-size arrays. Since Array.Resize is available to VB.NET as well, you have two options to choose from if you're using that language.

When you start working with arrays, you find that they are quick to use at run time, but lack some useful functionality. For example, it's not so easy to add new elements or to remove existing items from the array. Fortunately, the .NET Framework offers a range of useful collections that do give you the feature set you need.

# Defining and Working with Collections

Collections are similar to arrays in that they enable you to store more than one object in a single variable. The same bag analogy works for collections: You can simply drop a number of items in a bag, and it will hold them for you. What's different with collections is how they enable you to work with the data in the bag. Instead of simply accessing each item by its index, most collections expose an Add method that enables you to add an item to the collection. Similarly, they have Remove and