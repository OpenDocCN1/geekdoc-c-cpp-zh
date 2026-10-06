# ONE-DIMENSIONAL ARRAYS

# Declaring Arrays

To declare an array in C, a programmer specifies the type of the elements and the number of elements required by an array as follows:

```
typearrayName[arraySize];
```

This is called a single-dimensional array. The ArraySize must be an integer greater than zero and can be any valid C data type. For example, to declare a 10-element array called balance of type double, use this statement:

```
doublebalance[10];
```

Here, balance is a variable array which is sufficient to hold up to 10 double numbers.

# Initializing Arrays

You can initialize an array in C either by one or using a single statement as follows:

```
doublebalance[5]={1000.0,2.0,3.4,7.0,50.0};
```

The number of values between braces { } cannot be larger than the number of elements that we declare for the array between square brackets [ ].

If you omit the size of the array, an array just big enough to hold the initialization is created. If, you write:

```
doublebalance[]={1000.0,2.0,3.4,7.0,50.0};
```

You will create exactly the same array as you did in the previous example. Following is an example to assign a single element of the array:

```
balance[4]=50.0;
```

The above statement assigns the 5th element in the array with a value of 50.0. All arrays have 0 as the index of their first element which is also called the base index and the last index of an array will be total size of the array minus 1. Shown below is the pictorial representation of the array we discussed above:

| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|--|
| balance | 1000.0 | 2.0 | 3.4 | 7.0 | 50.0 |

# Accessing Array Elements

An element is accessed by indexing the array name. This is done by placing the index of the element within square brackets after the name of the array. For example: