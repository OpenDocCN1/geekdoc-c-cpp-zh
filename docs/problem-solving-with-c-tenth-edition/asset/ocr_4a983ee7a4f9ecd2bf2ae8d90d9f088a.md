# Testing inputData

Every function should be tested in a program in which it is the only untested function. The function inputData includes a call to the function getTotal. Therefore, we should test getTotal in a driver program of its own. Once getTotal has been completely tested, we can use it in a program, like the one in Display 7.6, to test the function inputData.

When testing the function inputData, we should include tests with all possible kinds of production figures for a plant. We should include a plant that has no production figures (as we did for plant 4 in Display 7.6); we should include a test for a plant with only one production figure (as we did for plant 3 in Display 7.6); and we should include a test for a plant with more than one production figure (as we did for plants 1 and 2 in Display 7.6). We should test for both nonzero and zero production figures, which is why we included a 0 in the input list for plant 2 in Display 7.6.

# Algorithm Design for scale

The function scale changes the value of each indexed variable in the array production so that it shows the number of asterisks to print out. Since there should be one asterisk for every 1000 units of production, the value of each indexed variable must be divided by 1000.0. Then to get a whole number of asterisks, this number is rounded to the nearest integer. This method can be used to scale the values in any array a of any size, so the function declaration for scale, shown in Display 7.5 and repeated here, is stated in terms of an arbitrary array a of some arbitrary size:

```
void scale(int a[], int size);
//Precondition: a[0] through a[size - 1] each has a
//nonnegative value.
//Postcondition: a[i] has been changed to the number of 1000s
//(rounded to an integer) that were originally in a[i], for
//all i such that 0 <= i <= size - 1.
```

When the function scale is called, the array parameter a will be replaced by the array production, and the formal parameter size will be replaced by NUMBER_OF_PLANTS so that the function call looks like the following:

```
scale(production, NUMBER_OF_PLANTS);
```

The algorithm for the function scale is as follows:

```
for (int index = 0; index < size; index++)
```

Divide the value of a[index] by 1000 and round the result to the nearest whole number; the result is the new value of a[index].

# Coding for scale

The algorithm for scale translates into the C++ code given next, where round is a function we still need to define. The function round takes one argument of type double and returns a type int value that is the integer nearest to its argument; that is, the function round will round its argument to the nearest whole number.