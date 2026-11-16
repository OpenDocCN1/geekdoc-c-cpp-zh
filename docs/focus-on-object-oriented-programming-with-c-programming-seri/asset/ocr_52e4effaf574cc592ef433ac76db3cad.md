• The `IntArray` class should also contain a private data member that will hold the name of the `IntArray` object when instantiated. This data member should be initialized with a call to a `setName()` member function.

I will supply a driver program, `iadrv.cpp`, that demonstrates the use of the `IntArray` class. The driver will demonstrate all operation and error condition features separately. Each test will note what feature is being demonstrated and output each array name, index, and corresponding element using the overloaded `<<` operator.

Note that for each array test data, the driver will simply multiply the array index by 10 immediately after each array is initialized or modified and output its contents. When your program encounters a run-time error, you should "simulate" a halt with appropriate diagnostics rather than actually halting the program. Be sure that all error messages sent to the terminal window are also sent to the `csis.txt` output file.

When elements of an array are output, the array name should be output, a left bracket, an index value, a right bracket, an equal sign, and finally a value. For example:

```
a[3] = 30
```

Note that the driver program outputs array elements vertically down the page. This behavior should not be changed. Be sure that you include a destructor for the `IntArray` class. The driver program will include the following tests:

+   1. Test array declared with single integer:

```
IntArray a(10);
```

+   2. Test array declared with two integers, one of which is negative:

```
IntArray b(-3, 6);
```

+   3. Test array declared with two non-negative integers:

```
IntArray c(6, 8);
```

+   4. Test array declared with two identical integers:

```
IntArray d(5, 5);
```