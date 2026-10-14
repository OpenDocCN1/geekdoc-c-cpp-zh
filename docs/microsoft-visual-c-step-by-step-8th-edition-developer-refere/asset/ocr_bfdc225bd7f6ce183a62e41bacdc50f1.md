pins array with four random numbers:

Click here to view code image

```
Random r = new Random();
int[] pins = new int[4]{ r.Next() % 10, r.Next() % 10,
    r.Next() % 10, r.Next() % 10 };
```

# Note

The System.Random class is a pseudorandom number generator. The Next method returns a nonnegative random integer in the range 0 to Int32.MaxValue by default. The Next method is overloaded, and other versions enable you to specify the minimum value and maximum value of the range. The default constructor for the Random class seeds the random number generator with a time-dependent seed value, which reduces the possibility of the class duplicating a sequence of random numbers. Using an overloaded version of the constructor, you can provide your own seed value. That way, you can generate a repeatable sequence of random numbers for testing purposes.

The number of values between the braces must exactly match the size of the array instance being created:

Click here to view code image

```
int[] pins = new int[3]{ 9, 3, 7, 2 }; // compile-time error
int[] pins = new int[4]{ 9, 3, 7 }; // compile-time error
int[] pins = new int[4]{ 9, 3, 7, 2 }; // OK
```

When you’re initializing an array variable in this way, you can actually omit the new expression and the size of the array. In this case, the compiler calculates the size from the number of initializers and generates code to create the array, such as in the following example:

```
int[] pins = { 9, 3, 7, 2 };
```

If you create an array of structures or objects, you can initialize each structure in the array by calling the structure or class constructor, as shown in this example:

Click here to view code image

```
Time[] schedule = { new Time(12,30), new Time(5,30) };
```

# Creating an implicitly typed array

The element type when you declare an array must match the type of elements that you attempt to store in the array. For example, if you declare pins to be an array of int, as shown in the preceding examples, you cannot store a double, string,