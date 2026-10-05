
# Creating an array instance

Arrays are reference types, regardless of the type of the elements. This means that an array variable refers to a contiguous block of memory holding the array elements on the heap, as a class variable refers to an object on the heap. (For a description of values and references and the differences between the stack and the heap, see Chapter 8, “Understanding values and references.") This rule applies regardless of the type of the data items in the array. Even if the array contains a value type such as int, the memory will still be allocated on the heap; this is the one case where value types are not allocated on memory.

Remember that when you declare a class variable, memory is not allocated for the object until you declare the instance using the new keyword. Arrays follow the same pattern: When you declare an array variable, you don't declare its size, and no memory is allocated (other than to hold the reference on the stack). The array is given memory only when the instance is created; this is also the point at which you specify the size of the array.

To create an array instance, you use the new keyword followed by the element type, followed by the size of the array you're creating enclosed between square brackets. Creating an array also initializes its elements using the familiar default values (0, null, or false, depending on whether the type is numeric, a reference, or a Boolean, respectively). For example, to create and initialize a new array of four integers for the pins variable declared earlier, you write this:

```
pins = new int[4];
```

The following illustration shows what happens when you declare an array, and later when you create an instance of the array:

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_393_0.png)

Because the memory for the array instance is allocated dynamically, the size of the array does not have to be a constant; it can be calculated at runtime, as shown in this example:

Click here to view code image

```
int size = int.Parse(Console.ReadLine());
int[] pins = new int[size];
```

You can also create an array whose size is 0. This might sound bizarre, but it's useful for situations in which the size of the array is determined dynamically and could even be 0. An array of size 0 is not a null array; it's an array containing zero elements.

# Populating and using an array

When you create an array instance, all the elements of the array are initialized to a default value depending on your type. For example, all numeric values to 0, objects are initialized to null, DateTime values are set to the date and time "01/01/0001 00:00:00", and strings are initialized to null.

You can modify this behavior and initialize the elements of an array to specific values if you prefer. You can do this by providing a comma-separated list of values between a pair of braces. For example, to initialize pins to an array of four int variables whose values are 9, 3, 7, and 2, you write this:

Click here to view code image

```
int[] pins = new int[4]{ 9, 3, 7, 2 };
```

The values between the braces don't have to be constants; they can be values calculated at runtime, as shown in the following example, which populates the pins array with four random numbers:

Click here to view code image

```
Random r = new Random();
int[] pins = new int[4]{ r.Next() % 10, r.Next() % 10, r.Next() % 10, r.Next() % 10 };
```

> Note

The System.Random class is a pseudorandom number generator. The Next method returns a nonnegative random integer in the range 0 to Int32.MaxValue by default. The Next method is overloaded, and other versions enable you to specify the minimum value and maximum value of the range. The default constructor for the Random class seeds the random number generator with a time-dependent seed value, which reduces the possibility of the class duplicating a sequence of random numbers. Using an overloaded version of the constructor, you can provide your own seed value. That way, you can generate a repeatable sequence of random numbers for testing purposes.

The number of values between the braces must exactly match the size of the array instance being created:

Click here to view code image

```
int[] pins = new int[3]{ 9, 3, 7, 2 }; // error, size mismatch
int[] pins = new int[4]{ 9, 3, 7, 2 }; // OK
```

# Accessing an individual array element

To access an individual array element, you must provide an index indicating which element you require. Array indexes are zero-based; so, the initial element of an array lives at index 0 and not index 1. An index value of 1 accesses the second element. For example, you can read the contents of element 2 (the third element) of the pins array into an int variable by using the following code:

```
int myPin;
myPin = pins[2];
```

Similarly, you can change the contents of an array by assigning a value to an indexed element:

```
myPin = 1645;
pins[2] = myPin;
```

All array element access is bounds-checked. If you specify an index that is less than 0 or greater than equal to the length of the array, the compiler throws an IndexOutOfRangeException exception, as in this example:

Click here to view code image

```
try {
    int[] pins = { 9, 3, 7, 2 };
    Console.WriteLine(pins[4]); // error, the fourth and last element
    is at index 3
}
catch (IndexOutOfRangeException ex) {
    ...
}
```
