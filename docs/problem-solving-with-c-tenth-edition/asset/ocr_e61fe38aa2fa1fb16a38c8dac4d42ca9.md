for the array and hope that size is large enough. There are two problems with this. First, you may estimate too low, and then your program will not work in all situations. Second, since the array might have many unused positions, this can waste computer memory. Dynamic arrays avoid these problems. If your program uses a dynamic array for student identification numbers, then the size of the class can be entered as input to the program and the dynamic array can be created to be exactly that size.

Dynamic arrays are created using the new operator. The creation and use of dynamic arrays is surprisingly simple. Since array variables are pointer variables, you can use the new operator to create dynamic variables that are arrays and treat these dynamic array variables as if they were ordinary arrays. For example, the following creates a dynamic array variable with ten array elements of type double:

```
typedef double* DoublePtr;
DoublePtr p;
p = new double[10];
```

To obtain a dynamic array of elements of any other type, simply replace double with the desired type. To obtain a dynamic array variable of any other size, simply replace 10 with the desired size.

There are also a number of less obvious things to notice about this example. First, the pointer type that you use for a pointer to a dynamic array is the same as the pointer type you would use for a single element of the array. For instance, the pointer type for an array of elements of type double is the same as the pointer type you would use for a simple variable of type double. The pointer to the array is actually a pointer to the first indexed variable of the array. In the previous example, an entire array with ten indexed variables is created and the pointer p is left pointing to the first of these ten indexed variables.

Also notice that when you call new, the size of the dynamic array is given in square brackets after the type, which in this example is the type double. This tells the computer how much storage to reserve for the dynamic array. If you omit the square brackets and the 10, the computer will allocate enough storage for only one variable of type double, rather than for an array of ten indexed variables of type double. As illustrated in Display 9.6, you can use an int variable in place of the constant 10 so that the size of the dynamic array can be read into the program.

The program in Display 9.6 sorts a list of numbers. This program works for lists of any size because it uses a dynamic array to hold the numbers. The size of the array is determined when the program is run. The user is asked how many numbers there will be, and then the new operator creates a dynamic array of that size. The size of the dynamic array is given by the variable array_size.

Notice the delete statement, which destroys the dynamic array variable a in Display 9.6. Since the program is about to end anyway, we did not really need this delete statement; however, if the program went on to do other

# Creating a dynamic array