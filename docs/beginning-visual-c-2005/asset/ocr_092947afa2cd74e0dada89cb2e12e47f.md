You could use a for loop here if you also wanted to record the index position of the maximum element as well as its value(for example:

```
double max = 0;
int index = 0;
for (int i = 0 ; i < sample->Length ; i++)
    if(max < samples[i])
    {
        max = samples[i];
        index = i;
    }
```

# Sorting One-Dimensional Arrays

The Array class in the System namespace defines a Sort() function that sorts the elements of a one-dimensional array so that they are in ascending order. To sort an array you just pass the array handle to the Sort() function. Here’s an example:

```
array<int>^ samples = { 27, 3, 54, 11, 18, 2, 16};
Array::Sort(samples);                         // Sort the array elements

for each(int value in samples)                 // Output the array elements
    Console::Write(L"{0, 8}", value);
Console::WriteLine();
```

The call to the Sort() function rearranges the values of the elements in the samples array so they are in ascending sequence. The result of executing this code fragment is:

2      3      11     16     18     27     54

You can also sort a range of elements in an array by supplying two more arguments to the Sort() function specifying the index for the first element of those to be sorted and the number of elements to be sorted. For example:

```
array<int>^ samples = { 27, 3, 54, 11, 18, 2, 16};
Array::Sort(samples, 2, 3);                   // Sort elements 2 to 4
```

This statement sorts the three elements in the samples array that begin at index position 2. After executing these statements, the elements in the array will have the values:

27     3      11     18     54     2      16

The are several other versions of the Sort() function that you can find if you consult the documentation but I’ll introduce one other that is particularly useful. This version presumes you have two arrays that are associated so that the elements in the first array represent keys to the corresponding elements in the second array. For example, you might store names of people in one array and the weights of the individuals in a second array. The Sort() function sorts the array of names in ascending sequence and also rearrange the elements of the weights array so the weights still match the appropriate person. Let’s try it in an example.