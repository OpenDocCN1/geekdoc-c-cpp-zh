# PITFALL: (continued)

template (Display 16.1) with the type parameter replaced by a type for which the assignment operator does not work at all, or does not work "correctly." As a more concrete example, suppose that your program defines the template function swapValues as in Display 16.1. You cannot add the following to your program:

```
int a[10], b[10];
<Some code to fill arrays>
swapValues(a, b);
```

This code will not work because assignment does not work with array types.

# Self-Test Exercises

5. Display 5.6 shows a function called search, which sequentially searches an array for a specified integer. Give a function template version of search that can be used to search an array of elements of any type. Give both the function declaration and the function definition for the template. (Hint: It is almost identical to the function given in Display 5.6.)

6. Compare and contrast overloading of a function name with the definition of a function template for the function name.

7. (This exercise is only for those who have already read at least Chapter 6 on structures and classes and preferably also read Chapter 8 on overloading operators.) Can you use the sort template function (Display 16.3) to sort an array with base type DayOfYear defined in Display 6.4?

8. (This exercise is only for those who have already read Chapter 10 on pointers and dynamic arrays.)

Although the assignment operator does not work with ordinary array variables, it does work with pointer variables that are used to name dynamic arrays. Suppose that your program defines the template function swapValues (as in Display 16.1) and contains the following code. What is the output produced by this code?

```
typedef int* ArrayPointer;
ArrayPointer a, b, c;
a = new int [3];
b = new int [3];

int i;
for (i = 0; i < 3; i++)
{
    a[i] = i;
    b[i] = i * 100;
}
c = a;
```