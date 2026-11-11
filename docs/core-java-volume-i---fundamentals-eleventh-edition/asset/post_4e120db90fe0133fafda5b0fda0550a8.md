
A comma after the last value is allowed, which can be convenient for an array to which you keep adding values over time:

```
    String[] authors = {
       "James Gosling",
       "Bill Joy",
       "Guy Steele",
       // add more names here and put a comma after each name
    };
```

You can declare an *anonymous array*:

```
    new int[] { 17, 19, 23, 29, 31, 37 }
```

This expression allocates a new array and fills it with the values inside the braces. It counts the number of initial values and sets the array size accordingly. You can use this syntax to reinitialize an array without creating a new variable. For example,

```
    smallPrimes = new int[] { 17, 19, 23, 29, 31, 37 };
```

is shorthand for

```
    int[] anonymous = { 17, 19, 23, 29, 31, 37 };
    smallPrimes = anonymous;
```

> **NOTE:** It is legal to have arrays of length 0. Such an array can be useful if you write a method that computes an array result and the result happens to be empty. Construct an array of length 0 as
>
> `new elementType[0]`
>
> or
>
> `new elementType[] { }`
>
> Note that an array of length 0 is not the same as `null`.

### 3.10.2 Accessing Array Elements

The array elements are *numbered from 0 to 99* (and not 1 to 100). Once the array is created, you can fill the elements in an array, for example, by using a loop:

```
    int[] a = new int[100];
    for (int i = 0; i < 100; i++)
        a[i] = i; // fills the array with numbers 0 to 99
```

When you create an array of numbers, all elements are initialized with zero. Arrays of boolean are initialized with `false`. Arrays of objects are initialized with the special value null, which indicates that they do not (yet) hold any objects. This can be surprising for beginners. For example,

```java
String[] names = new String[10];
```

creates an array of ten strings, all of which are null. If you want the array to hold empty strings, you must supply them:

```java
for (int i = 0; i < 10; i++) names[i] = "";
```

> **CAUTION:** If you construct an array with 100 elements and then try to access the element a[100] (or any other index outside the range from 0 to 99), an "array index out of bounds" exception will occur.

To find the number of elements of an array, use `array.length`. For example:

```java
for (int i = 0; i < a.length; i++)
    System.out.println(a[i]);
```

### 3.10.3 The "for each" Loop

Java has a powerful looping construct that allows you to loop through each element in an array (or any other collection of elements) without having to fuss with index values.

The *enhanced for loop*

```java
for (variable : collection) statement
```

sets the given variable to each element of the collection and then executes the statement (which, of course, may be a block). The *collection expression* must be an array or an object of a class that implements the Iterable interface, such as ArrayList. We discuss array lists in Chapter 5 and the Iterable interface in Chapter 9.

For example,

```java
for (int element : a)
    System.out.println(element);
```

prints each element of the array a on a separate line.

You should read this loop as "for each element in a". The designers of the Java language considered using keywords, such as foreach and in. But this loop was a late addition to the Java language, and in the end nobody wanted to break the old code that already contained methods or variables with these names (such as System.in).

Of course, you could achieve the same effect with a traditional for loop:

```java
for (int i = 0; i < a.length; i++)
    System.out.println(a[i]);
```

However, the “for each” loop is more concise and less error-prone, as you don’t have to worry about those pesky start and end index values.

> **NOTE:** The loop variable of the “for each” loop traverses the elements of the array, not the index values.

The “for each” loop is a pleasant improvement over the traditional loop if you need to process all elements in a collection. However, there are still plenty of opportunities to use the traditional for loop. For example, you might not want to traverse the entire collection, or you may need the index value inside the loop.

> **TIP:** There is an even easier way to print all values of an array, using the toString method of the Arrays class. The call Arrays.toString(a) returns a string containing the array elements, enclosed in brackets and separated by commas, such as "[2, 3, 5, 7, 11, 13]". To print the array, simply call

```java
System.out.println(Arrays.toString(a));
```

### 3.10.4 Array Copying

You can copy one array variable into another, but then *both variables refer to the same array*:

```java
int[] luckyNumbers = smallPrimes;
luckyNumbers[5] = 12; // now smallPrimes[5] is also 12
```

Figure 3.14 shows the result. If you actually want to copy all values of one array into a new array, use the `copyOf` method in the `Arrays` class:

```java
int[] copiedLuckyNumbers = Arrays.copyOf(luckyNumbers, luckyNumbers.length);
```

The second parameter is the length of the new array. A common use of this method is to increase the size of an array:

```java
luckyNumbers = Arrays.copyOf(luckyNumbers, 2 * luckyNumbers.length);
```

The additional elements are filled with 0 if the array contains numbers, false if the array contains boolean values. Conversely, if the length is less than the length of the original array, only the initial values are copied.

```java
    else if (args[0].equals("-g"))
        System.out.println("Goodbye,");
    // print the other command-line arguments
    for (int i = 1; i < args.length; i++)
        System.out.println(" " + args[i]);
    System.out.println("!");
}
```

If the program is called as

```
java Message -g cruel world
```

then the args array has the following contents:

```
args[0]: "-g"
args[1]: "cruel"
args[2]: "world"
```

The program prints the message

```
Goodbye, cruel world!
```

> **C++ NOTE:** In the main method of a Java program, the name of the program is not stored in the args array. For example, when you start up a program as
>
>     java Message -h world
>
> from the command line, then args[0] will be "-h" and not "Message" or "java".

### 3.10.6 Array Sorting

To sort an array of numbers, you can use one of the sort methods in the Arrays class:

```java
int[] a = new int[10000];
. . .
Arrays.sort(a)
```

This method uses a tuned version of the QuickSort algorithm that is claimed to be very efficient on most data sets. The Arrays class provides several other convenience methods for arrays that are included in the API notes at the end of this section.

The program in Listing 3.7 puts arrays to work. This program draws a random combination of numbers for a lottery game. For example, if you play a "choose 6 numbers from 49" lottery, the program might print this:

Bet the following combination. It’ll make you rich!

+   4
+   7
+   8
+   19
+   30
+   44

To select such a random set of numbers, we first fill an array numbers with the values 1, 2, . . ., n:

```
int[] numbers = new int[n];
for (int i = 0; i < numbers.length; i++)
    numbers[i] = i + 1;
```

A second array holds the numbers to be drawn:

```
int[] result = new int[k];
```

Now we draw k numbers. The Math.random method returns a random floating-point number that is between 0 (inclusive) and 1 (exclusive). By multiplying the result with n, we obtain a random number between 0 and n − 1.

```
int r = (int) (Math.random() * n);
```

We set the result to be the number at that index. Initially, that is just r + 1, but as you’ll see presently, the contents of the numbers array are changed after each draw.

```
result[i] = numbers[r];
```

Now we must be sure never to draw that number again—all lottery numbers must be distinct. Therefore, we overwrite numbers[r] with the last number in the array and reduce n by 1.

```
numbers[r] = numbers[n - 1];
n--;
```

The point is that in each draw we pick an index, not the actual value. The index points into an array that contains the values that have not yet been drawn.

After drawing k lottery numbers, we sort the result array for a more pleasing output:

```
Arrays.sort(result);
for (int r : result)
    System.out.println(r);
```
