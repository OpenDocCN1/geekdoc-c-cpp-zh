![](bbox=[0.1, 0.1, 0.25, 0.28])

students.Length contains the number of elements in the array.

C# provides another loop, named foreach, designed specifically for iterating through collections such as the array. It works this way:

```
```csharp
// Now average the students that you have.
double sum = 0.0;
foreach (Student student in students)
{
    sum += student.gpa; // This extracts the current student's GPA.
}
double avg = sum / students.Length;
```
```

The first time through the loop, foreach fetches the first Student object in the array and stores it in the variable student. On each subsequent pass, foreach retrieves the next element. Control passes out of the foreach loop when all elements in the array have been processed.

Notice that no index appears in the foreach statement. The lack of an index greatly reduces the chance of error and is simpler to write than the for statement, although sometimes that index is handy and you prefer a for loop.

![](bbox=[0.1, 0.65, 0.25, 0.78])

The foreach loop is even more powerful than it would seem from the example. This statement works on other collection types in addition to arrays. In addition, foreach handles multidimensional arrays (arrays of arrays, in effect), a topic I don't describe in this book. To find out all about multidimensional arrays, look up multidimensional arrays in the C# Help system.

# Sorting Arrays of Data

A common programming challenge is the need to sort the elements within an array. Just because an array cannot grow or shrink doesn't mean that the elements within it cannot be moved, removed, or added. For example, the following code snippet swaps the location of two string elements within the array strings:

```
```csharp
string temp = strings[i]; // Save the i'th string.
strings[i] = strings[k]; // Replace it with the kth.
strings[k] = temp;       // Replace kth with temp.
```
```

In this example, the object reference in the ith location in the strings array is saved so that it isn't lost when the second statement replaces it with another element. Finally, the temp variable is saved back into the kth location. Pictorially, this process looks like Figure 6-1.

![](bbox=[0.1, 0.88, 0.25, 0.98])

The data collections discussed in the rest of this chapter are more versatile than the array for adding and removing elements.