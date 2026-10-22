loop instead. The for loop is good with arrays as well, for instance if you need to count each item, like this:

```
for(int i = 0; i < names.Length; i++)
Console.WriteLine("Item number " + i + ": "
+ names[i]);
```

We use the above Length property of the array to see how many times the loop should iterate, and then we use the counter (i) to output where we are in the process, as well as get the item from the array. Just like we used a number, a so called indexer, to put items into the array, we can use it to get a specific item out again.

You could use an array to sort a range of values, and it’s very straightforward. The array class holds a bunch of smart methods for working with arrays. This example uses numbers instead of strings, just to try something else, but it could just as easily have been strings. I wish to show you another way of populating an array, which is much easier if you have a small, predefined set of items that you wish to put into your array. Take a look:

```
int[] numbers = new int[5] { 4, 3, 8, 0, 5 };
```

With one line, we have created an array with a size of 5, and filled it with 5 integers. By filling the array like this, you get an extra advantage, since the compiler will check and make sure that you don’t insert too many items into the array. Try adding a number more—you will see the compiler notify about the potential error.

The arrays we have used so far have only had one dimension. However, C# arrays can also be multidimensional,