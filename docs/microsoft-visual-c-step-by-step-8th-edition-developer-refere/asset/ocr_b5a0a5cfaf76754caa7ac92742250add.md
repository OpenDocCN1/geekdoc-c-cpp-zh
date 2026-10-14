references to the same array instance, as demonstrated in the following example:

Click here to view code image

```
int[] pins = { 9, 3, 7, 2 };
int[] alias = pins; // alias and pins refer to the same array
instance
```

In this example, if you modify the value at pins[1], the change will also be visible by reading alias[1].

If you want to make a copy of the array instance (the data on the heap) that an array variable refers to, you have to do two things. First, you create a new array instance of the same type and the same length as the array you are copying. Second, you copy the data from the original array element by element to the new array, as in this example:

Click here to view code image

```
int[] pins = { 9, 3, 7, 2 };
int[] copy = new int[pins.Length];
for (int i = 0; i < pins.Length; i++)
{
    copy[i] = pins[i];
}
```

Note that this code uses the Length property of the original array to specify the size of the new array.

Copying an array is actually a common requirement of many applications—so much so that the System.Array class provides some useful methods that you can employ to copy an array. For example, the CopyTo method copies the contents of one array into another array given a specified starting index. The following example copies all the elements from the pins array to the copy array starting at element zero:

Click here to view code image

```
int[] pins = { 9, 3, 7, 2 };
int[] copy = new int[pins.Length];
pins.CopyTo(copy, 0);
```

Another way to copy the values is to use the System.Array static method named Copy. As with CopyTo, you must initialize the target array before calling Copy:

Click here to view code image

```
int[] pins = { 9, 3, 7, 2 };
int[] copy = new int[pins.Length];
Array.Copy(pins, copy, copy.Length);
```