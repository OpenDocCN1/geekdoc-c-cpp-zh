
More importantly—changes made to the object being referred to by the parameter will influence the object referred to by the argument since they are one and the same. Let's see why. Recall that when you make a variable of a class type, you are making a reference to an object, not the object itself. The object is allocated by means of new, and a reference to it is assigned to the reference variable. When you use a reference variable as an argument to a method, the parameter gets a reference to the same object as that referred to by the argument. Consequently, the argument and parameter will both refer to the same object. This means objects are passed to methods by use of what is effectively call-by-reference. Changes to the object inside the method do affect the object used as an argument. In C#, arrays can have one or more dimensions, although the one-dimensional array is the most common. Arrays are used for a variety of purposes because they offer a convenient means of grouping related variables. For example, you may use an array to hold a record of the daily high temperatures for a month, a list of clients signed onto a network, or your collection of programming books.

The chief advantage of an array is that it organizes information so that it can be easily manipulated. For example, if you have an array containing the salaries for a chosen group of families, it is easy to compute the average salary by looping through the array. Likewise, arrays organize information so that it can be easily sorted. Although arrays in C# can be used just like arrays in many other programming languages, they have one unique property: They are implemented as objects. This fact is one reason that a discussion of arrays was deferred until objects had been introduced. By implementing arrays as objects, several significant advantages are gained, not the least of which is that unused arrays can be garbage collected.

Since the compound assignment statements are shorter than their noncompound counterparts, the compound assignment operators are likewise sometimes called the shorthand assignment operators.

The compound assignment operators give two advantages. First, they are more compact than their "longhand" counterparts. Second, they can produce more efficient executable code (since the left-hand operand is evaluated just once). Therefore, you will frequently see the compound assignment operators used in expertly written C# programs. When compatible types are mixed in an assignment, the value of the right side is automatically converted to the type of the left side. Therefore, in the previous section, the value in `i` is converted into a float and then assigned to `f`. However, because of C#'s strict type checking, not all types are compatible, and accordingly, not all type conversions are implicitly permitted. For example, bool and int are not compatible.

When these two conditions are met, a widening conversion happens. For example, the int type is always large enough to hold all valid byte values, and both int and byte are integer types, so an implicit conversion can be applied. For widening conversions, the numeric kinds, including integer and floating-point types, are compatible with one another. For example, the following program is perfectly valid, since long to double is a widening conversion that is performed automatically:

Although the implicit type conversions are useful, they won't satisfy all programming needs since they apply only to widening conversions between compatible types. For all other cases, you should use a cast. A cast is an instruction to the compiler to convert an expression into a specified type. Hence, it demands an explicit type conversion. A cast has this general structure:

```
(target-type) expression
```

Here, target-type indicates the target type to convert the specified expression to. For example, suppose you want the type of the expression x/y to be int. In that case, although x and y are of type double, the cast converts the result of the expression to int. The parentheses around x/y are important. Otherwise, the cast to int would apply only to x, and not to the result of the division. The cast is vital here because there is no implicit conversion from double to int.

When a cast includes a narrowing conversion, data may be lost. For example, when casting a long into an int, data will be lost if the long's value is greater than the range of an int because its high-order bits are discarded. When a floating-point value is cast to an integer type, the fractional part will likewise be lost because of truncation. For example, if the value 1.23 is assigned to an integer, the resulting value will simply be 1. The 0.23 is lost. In the program, the cast of (x/y) to int brings about the truncation of the fractional part, and data is lost. Next, no loss of data happens when b is assigned the value 100 because a byte can hold the value 100. However, when an attempt is made to assign b the value 257, data loss happens because 257 exceeds a byte's range. This results in b having the value 1 because only the 1 bit is set in the low-order 8 bits of the binary representation of 257. Finally, no data is lost, yet a cast is required when assigning a byte value to a char.

A one-dimensional array is a list of related variables. Such arrays are common in programming. For example, you may use a one-dimensional array to store the ID numbers of the active clients on a network. Another array may be used to store the current batting averages for a baseball team. Since arrays in C# are implemented as objects, two steps are required to obtain one for use in your program. First, you should declare a variable that can refer to an array. Second, you should create an instance of the array by use of new. Thus, to declare a one-dimensional array, you will regularly use this general structure:

```
type[] arrayName = new type[size];
```

Here, type declares the element type of the array. The element type determines the data type of the elements that the array will contain. Notice the square brackets that follow type. They indicate that a reference to a one-dimensional array is being declared. The number of elements that the array will hold is determined by size. Here is an example. The following makes an int array of ten elements and connects it to an array reference variable named test:

```
int[] test = new int[10];
```

The test variable holds a reference to the memory allocated by new. This memory is large enough to hold ten elements of type int. In this situation, when test is first created, it refers to no physical object. It is only after the second statement executes that test refers to an array.

An individual element inside an array is accessed by use of an index. An index describes the position of an element inside an array. In C#, all arrays have zero as the index of their first element. Since test has ten elements, it has index values of 0 through 9. To index an array, specify the number of the element you want, enclosed by square brackets.

## Ref and Out Parameters

As just explained, by default, value types, such as int or char, are passed by value to a method. This means changes to the parameter that receives a value type won't affect the actual argument used in the call. You can, however, modify this behavior. Using the ref and out keywords, it is possible to pass any of the value types by reference. Doing so permits a method to modify the argument used in the call. Before going into the mechanics of using ref and out, it is helpful to understand why you should pass a value type by reference. As a rule, there are two reasons: to permit a method to modify the contents of its arguments or to enable a method to return more than one value. Let's look at each reason in detail.

Frequently, you will need a method to be able to work on the actual arguments that are passed to it. The quintessential example of this is a "swap" method that swaps the values of its two arguments. Since value types are passed by value, it is impossible to write such a method that swaps the values of two ints, for instance, using C#'s default call-by-value parameter-passing mechanism. The ref modifier takes care of this issue.

As you probably are aware, a return statement enables a method to return a value to its caller. However, a method can return only one value each time.
