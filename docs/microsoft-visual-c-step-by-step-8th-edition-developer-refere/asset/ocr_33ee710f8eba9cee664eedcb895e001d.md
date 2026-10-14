```
parameters to the first item
    int currentMin = paramList[0];

    // Iterate through the list of parameters, searching to see whether any of them
    // are smaller than the value held in currentMin
    foreach (int i in paramList)
    {
        // If the loop finds an item that is smaller than the value held in
        // currentMin, then set currentMin to this value
        if (i < currentMin)
        {
            currentMin = i;
        }
    }

    // At the end of the loop, currentMin holds the value of the smallest
    // item in the list of parameters, so return this value.
    return currentMin;
}
```

# Note

The ArgumentException class is specifically designed to be thrown by a method if the arguments supplied do not meet the requirements of the method.

To use the Min method to find the minimum of two int variables named first and second, you can write this:

```
int[] array = new int[2];
array[0] = first;
array[1] = second;
int min = Util.Min(array);
```

And to use the Min method to find the minimum of three int variables (named first, second, and third), you can write this:

```
int[] array = new int[3];
array[0] = first;
array[1] = second;
array[2] = third;
int min = Util.Min(array);
```

You can see that this solution avoids the need for a large number of overloads, but it does so at a price: you have to write additional code to populate the array that you pass in. You can, of course, use an anonymous array if you prefer, like this: