
+   9. Write some C++ code that will fill an array with 20 values of type `int` read in from the keyboard. You need not write a full program, just the code to do this, but do give the declarations for the array and for all variables.

+   10. Suppose you have the following array declaration in your program:
+   
+   ```cpp
+   int yourArray[7];
+   ```
+   
+   Also, suppose that in your implementation of C++, variables of type `int` use two bytes of memory. When you run your program, how much memory will this array consume? Suppose that when you run your program, the system assigns the memory address 1000 to the indexed variable `yourArray[0]`. What will be the address of the indexed variable `yourArray[3]`?

## 5.2 Arrays in Functions

You can use both array indexed variables and entire arrays as arguments to functions. We first discuss array indexed variables as arguments to functions.

### INDEXED VARIABLES AS FUNCTION ARGUMENTS

An indexed variable can be an argument to a function in exactly the same way that any variable of the array base type can be an argument. For example, suppose a program contains the following declarations:

```
```cpp
double i, n, a[10];
```
```

If `myFunction` takes one argument of type `double`, then the following is legal:

```
```cpp
myFunction(n);
```
```

Since an indexed variable of the array `a` is also a variable of type `double`, just like `n`, the following is equally legal:

```
```cpp
myFunction(a[3]);
```
```

An indexed variable can be a call-by-value argument or a call-by-reference argument.

One subtlety applies to indexed variables used as arguments, however. For example, consider the following function call:

```
```cpp
myFunction(a[i]);
```
```

If the value of i is 3, then the argument is a[3]. On the other hand, if the value of i is 0, then this call is equivalent to the following:

```
myFunction(a[0]);
```

The indexed expression is evaluated in order to determine exactly which indexed variable is given as the argument.

### Self-Test Exercises

+   11. Consider the following function definition:

```
void tripler(int& n)
{
    n = 3*n;
}
```

Which of the following are acceptable function calls?

```
int a[3] = {4, 5, 6}, number = 2;
tripler(a[2]);
tripler(a[3]);
tripler(a[number]);
tripler(a);
tripler(number);
```

+   12. What (if anything) is wrong with the following code? The definition of tripler is given in Self-Test Exercise 11.

```
int b[5] = {1, 2, 3, 4, 5};
for (int i = 1; i <= 5; i++)
    tripler(b[i]);
```

### ENTIRE ARRAYS AS FUNCTION ARGUMENTS

A function can have a formal parameter for an entire array so that when the function is called, the argument that is plugged in for this formal parameter is an entire array. However, a formal parameter for an entire array is neither a call-by-value parameter nor a call-by-reference parameter; it is a new kind of formal parameter referred to as an array parameter. Let’s start with an example.

### Display 5.3 Function with an Array Parameter

### FUNCTION DECLARATION

```
void fillUp(int a[], int size);
//Precondition: size is the declared size of the array a.
//The user will type in size integers.
//Postcondition: The array a is filled with size integers
//from the keyboard.
```

### FUNCTION DEFINITION

```
void fillUp(int a[], int size)
{
    cout << "Enter " << size << " numbers:\n";
    for (int i = 0; i < size; i++)
        cin >> a[i];
    cout << "The last array index used is " << (size - 1) << endl;
}
```

with values typed in from the keyboard; the function then outputs a message to the screen telling the index of the last array index used.

The formal parameter int a[] is an array parameter. The square brackets, with no index expression inside, are what C++ uses to indicate an array parameter. An array parameter is not quite a call-by-reference parameter, but for most practical purposes it behaves very much like a call-by-reference parameter. Let's go through this example in detail to see how an array argument works in this case. (An array argument is, of course, an array that is plugged in for an array parameter, such as a[].)

When the function fillUp is called, it must have two arguments: The first gives an array of integers, and the second should give the declared size of the array. For example, the following is an acceptable function call:

```
int score[5], numberOfScores = 5;
fillUp(score, numberOfScores);
```

This call to fillUp will fill the array score with five integers typed in at the keyboard. Notice that the formal parameter a[] (which is used in the function declaration and the heading of the function definition) is given with square brackets but no index expression. (You may insert a number inside the square brackets for an array parameter, but the compiler will simply ignore the number, so we will not use such numbers in this book.) On the other hand, the argument given in the function call (score, in this example) is given without any square brackets or any index expression.

array argument

when to use []

What happens to the array argument score in this function call? Very loosely speaking, the argument score is plugged in for the formal array parameter a in the body of the function, and then the function body is executed. Thus, the function call

```
fillUp(score, numberOfScores);
```

is equivalent to the following code:

```
{ size = 5; cout << "Enter " << size << " numbers:\n"; for (int i = 0; i < size; i++) cin >> score[i]; cout << "The last array index used is " << (size - 1) << endl; }
```

5 is the value of numberOfScores

The formal parameter a is a different kind of parameter from the ones we have seen before now. The formal parameter a is merely a placeholder for the argument score. When the function fillUp is called with score as the array argument, the computer behaves as if were replaced with the corresponding argument score. When an array is used as an argument in a function call, any action that is performed on the array parameter is performed on the array argument, so the values of the indexed variables of the array argument can be changed by the function. If the formal parameter in the function body is changed (for example, with a cin statement), then the array argument will be changed.

So far it looks as if an array parameter is simply a call-by-reference parameter for an array. That is close to being true, but an array parameter is slightly different from a call-by-reference parameter. To help explain the difference, let's review some details about arrays.

Recall that an array is stored as a contiguous chunk of memory. For example, consider the following declaration for the array score:

```
int score[5];
```

When you declare this array, the computer reserves enough memory to hold five variables of type int, which are stored one after the other in the computer's memory. The computer does not remember the addresses of each of these five indexed variables; it remembers only the address of indexed variable score[0]. The computer also remembers that score has a total of five indexed variables, all of type int. It does not remember the address in memory of any indexed variable other than score[0]. For example, when your program needs score[3], the computer calculates the address of score[3] from the address of score[0]. The computer knows that score[3] is located three int variables past score[0]. Thus, to obtain the address of score[3], the computer takes the address of score[0] and adds a number that represents the amount of memory used by three int variables; the result is the address of score[3].

Viewed this way, an array has three parts: the address (location in memory) of the first indexed variable, the base type of the array (which determines how much memory

each indexed variable uses), and the size of the array (that is, the number of indexed variables). When an array is used as an array argument to a function, only the first of these three parts is given to the function. When an array argument is plugged in for its corresponding formal parameter, all that is plugged in is the address of the array's first indexed variable. The base type of the array argument must match the base type of the formal parameter, so the function also knows the base type of the array. However, the array argument does not tell the function the size of the array. When the code in the function body is executed, the computer knows where the array starts in memory and how much memory each indexed variable uses, but (unless you make special provisions) it does not know how many indexed variables the array has. That is why it is critical that you always have another int argument telling the function the size of the array. (That is also why an array parameter is not the same as a call-by-reference parameter. You can think of an array parameter as a weak form of call-by-reference parameter in which everything about the array is told to the function except for the size of the array).²

These array parameters may seem a little strange, but they have at least one very nice property as a direct result of their seemingly strange definition. This advantage is best illustrated by again looking at our example of the function fillUp given in Display 5.3. That same function can be used to fill an array of any size, as long as the base type of the array is int. For example, suppose you have the following array declarations:

```
int score[5], time[10];
```

The first of the following calls to fillUp fills the array score with five values, and the second fills the array time with ten values:

```
fillUp(score, 5);
fillUp(time, 10);
```

You can use the same function for array arguments of different sizes, because the size is a separate argument.

### THE const PARAMETER MODIFIER

When you use an array argument in a function call, the function can change the values stored in the array. This is usually fine. However, in a complicated function definition, you might write code that inadvertently changes one or more of the values stored in an array even though the array should not be changed at all. As a precaution, you can tell the compiler that you do not intend to change the array argument, and the computer will then check to make sure your code does not inadvertently change any of the values in the array. To tell the compiler that an array argument should not be changed by your function, insert the modifier const before the array parameter for that argument

² If you have heard of pointers, this will sound like pointers and indeed an array argument is passed by passing a pointer to its first (zeroth) index variable. We will discuss this in Chapter 10. If you have not yet learned about pointers, you can safely ignore this footnote.
