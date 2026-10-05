
# PITFALL: Array Index out of Range

The most common programming error made when using arrays is attempting to reference a nonexistent array index. For example, consider the following array declaration:

```
int a[6];
```

When using the array a, every index expression must evaluate to one of the integers 0 through 5. For example, if your program contains the indexed variable a[1], the i must evaluate to one of the six integers 0, 1, 2, 3, 4, or 5. If i evaluates to anything else, that is an error. When an index expression evaluates to some value than those allowed by the array declaration, the index is said to be out of range or simply illegal. In most systems, the result of an illegal array index is that your program will simply do something wrong, disastrously wrong, and will do without giving you any warning.

For example, suppose your system is typical, the array a is declared as shown, and your program contains the following:

```
a[i] = 238;
```

Now, suppose the value of i, unfortunately, happens to be 7. The computer proceeds as if a[7] were a legal variable. The computer calculates the address where a[7] would be (if there were only one a[7]) and places the value 238 in that location in memory. However, there is no indexed variable a[7] and the memory that receives this 238 probably belongs to some other variable, a variable named moreStuff. The value of moreStuff might have been unintentionally changed. This situation is illustrated in Figure 5.2.

Array indexes may come out of range at the first or last iteration of a loop that processes the array. Thus, it pays to carefully check all array processing loops to be certain that they begin and end with legal array indexes.

# Initializing Arrays

An array can be initialized when it is declared. When initializing the array, the values for the indexed variables are enclosed in braces and separated with commas. For example, consider the following:

```
int children[3] = {2, 12, 1};
```

The previous declaration is equivalent to the following code:

```
int children[3];
children[0] = 2;
children[1] = 12;
children[2] = 1;
```

If you list fewer values than are indexed variables, those values will be used to initialize the first few indexed variables, and the remaining variables will be initialized to a zero of the array base type. In this situation, indexed variables not provided with initializers are initialized to zero. However, arrays with no initializers and other variables declared within a function definition, including the main function of a program, may not be initialized. Although array indexed variables (and other variables) may sometimes be automatically initialized to zero, you cannot and should not count on it.

If you initialize an array when it is declared, you can omit the size of the array, and the array will automatically be declared to have the minimum size needed for the initialization value. For example, the following declaration

```
int b[] = {5, 12, 11};
```

is equivalent to

```
int b[3] = {5, 12, 11};
```

# Introduction to Arrays

# Self-Test Exercises

- 1. Describe the difference in the meaning of int a[5]; and the meaning of a[4]. What is the meaning of the [5] and [4] in each case?

- 2. In the array declaration
double score[5];
identify the following:
a. The array name
b. The base type
c. The declared size of the array
d. The range of values an index accessing this array can have
e. One of the indexed variables (or elements) of this array

- 3. Identify any errors in the following array declarations.
int x[4] = {8, 7, 6, 4, 3}; evenint x[] = {8, 7, 6, 4};
const int SIZE = 4;
 x[SIZE];

- 4. What is the output of the following code?
char symbol[3] = {'a', 'b', 'c'};
for(int index = 0; index < 3; index++)
cout << symbol[index];

# Self-Test Exercises (continued)

- 5. What is the output of the following code?

```
double a[3] = {1.1, 2.2, 3.3};
cout << a[0] << " " << a[1] << " " << a[2] << endl;
a[1] = a[2];
cout << a[0] << " " << a[1] << " " << a[2] << endl;
```

- 6. What is the output of the following code?

```
int i, temp[10];
for (i = 0; i < 10; i++)
    temp[i] = 2*i;
for (i = 0; i < 10; i++)
    cout << temp[i] << " ";
cout << endl;
for (i = 0; i < 10; i = i + 2)
    cout << temp[i] << " ";
```

- 7. What is wrong with the following piece of code?

```
int sampleArray[10];
for (int index = 1; index <= 10; index++)
    sampleArray[index] = 3*index;
```

- 8. Suppose we expect the elements of the array to be ordered so that
a[0] <= a[1] <= a[2] <= ...

However, to be safe we want to program the array and issue a warning
in case it turns are out of order. The following code is
supposed to output such a warning, but it contains a bug. What is it?

```
double a[10];
<Some code to fill the array goes here.>
for (int index = 0; index < 10; index++)
    if (a[index] > a(index + 1))
        cout << "Array elements " << index << " and "
             << (index + 1) << " are out of order.";
```

- 9. Write some C++ code that will fill an array with 20 values of type int read
from the keyboard. You do not need a full program, just the code to do this,
but give the declarations for the array and for all variables.

# Self-Test Exercises (continued)

- 10. Suppose you have the following array declaration in your program:

```
int yourArray[7];
```

Suppose that in your program, how much memory will this consume?

# 5.2 Arrays in Functions

You can use both indexed variables and entire arrays as arguments. We first discuss indexed variables as arguments.

## Indexed Variables as Arguments

An indexed variable can be an argument, just like any variable. For example, consider the following:

```
double i, n, a[10];
```

If myFunction takes one argument of double, then the following is legal:

```
myFunction(n);
```

Since an indexed variable of the array is also a variable, the following is legal:

```
myFunction(a[3]);
```

If the value of i is 3, then the argument is a[3]. On the other hand, if the value of i is 0, then this call is equivalent to the following:

```
myFunction(a[0]);
```

## Self-Test Exercises

- 11. Consider the following function:

```
void tripler(int& n)
{
    n = 3 * n;
}
```

Which of the following are acceptable function calls?

```
int a[3] = {4, 5, 6}, number = 2;
tripler(a[2]);
tripler(a[3]);
tripler(number);
tripler(a);
tripler(number);
```

- 12. What (if anything) is wrong with the following code? The definition of tripler is given in Self-Test Exercise 11.

```
int b[5] = {1, 2, 3, 4, 5};
for (int i = 1; i <= 5; i++)
    tripler(b[i]);
```

## Entire Arrays as Function Arguments

A function can have a formal parameter for an entire array so that the function is called, the argument that is plugged in for this formal parameter is an array. However, a formal parameter for an entire array is neither a call-by-value parameter nor a call-by-reference parameter; it is a new kind of formal parameter referred to as an array parameter. Let's start with an example.

The defined in Display 5 has one array parameter, a, which will be replaced by an entire array when the function is called. It also has one call-by-value parameter (size) that is assumed to be an integer value equal to the size of the array. This function fills its argument (that is, fills the array's indexed variables) with values typed from the keyboard; the function then outputs a message to the screen telling the last of array index used.

The formal parameter int[] is an array parameter. The square brackets, or C++ syntax, to indicate an array parameter is not quite a call-by-reference, but for most practical purposes it behaves very much like a call-by-reference parameter. Let us go through this example in detail to see how an array argument works in this case. (An array argument is, of course, an array that is plugged in for an array parameter, such as a(size)).
