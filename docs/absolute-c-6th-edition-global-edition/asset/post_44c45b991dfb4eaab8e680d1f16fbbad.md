
## Self-Test Exercises

- 1. Describe the difference in the meaning of `int a[5];` and the meaning of `a[4]`. What is the meaning of the `[5]` and `[4]` in each case?

- 2. In the array declaration

  `double score[5];`

  identify the following:
  - a. The array name
  - b. The base type
  - c. The declared size of the array
  - d. The range of values an index accessing this array can have
  - e. One of the indexed variables (or elements) of this array

- 3. Identify any errors in the following array declarations.
  - a. `int x[4] = { 8, 7, 6, 4, 3 };`
  - b. `int x[] = { 8, 7, 6, 4 };`
  - c. `const int SIZE = 4;`
    `int x[SIZE];`

- 4. What is the output of the following code?

  ```
  char symbol[3] = {'a', 'b', 'c'};
  for (int index = 0; index < 3; index++)
      cout << symbol[index];
  ```

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

- 8. Suppose we expect the elements of the array a to be ordered so that

  ```
  a[0] <= a[1] <= a[2] <= ...
  ```

  However, to be safe we want our program to test the array and issue a warning in case it turns out that some elements are out of order. The following code is supposed to output such a warning, but it contains a bug. What is it?

  ```
  double a[10];
  <Same code to fill the array a goes here.>
  for (int index = 0; index < 10; index++)
      if (a[index] > a[index + 1])
          cout << "Array elements " << index << " and " << (index + 1) << " are out of order.";
  ```

- 9. Write some C++ code that will fill an array a with 20 values of type int read in from the keyboard. You need not write a full program, just the code to do this, but do give the declarations for the array and for all variables.

- 10. Suppose you have the following array declaration in your program:

  ```
  int yourArray[7];
  ```

  Also, suppose that in your implementation of C++, variables of type int use two bytes of memory. When you run your program, how much memory will this array consume? Suppose that, when you run your program, the system assigns the memory address 1000 to the indexed variable yourArray[0]. What will be the address of the indexed variable yourArray[3]?

## 5.2 Arrays in Functions

You can use both array indexed variables and entire arrays as arguments to functions. We first discuss array indexed variables as arguments to functions.

### Indexed Variables as Function Arguments

An indexed variable can be an argument to a function in exactly the same way that any variable of the array base type can be an argument. For example, suppose a program contains the following declarations:

```
double i, n, a[10];
```

If myFunction takes one argument of type double, then the following is legal:

```
myFunction(n);
```

Since an indexed variable of the array a is also a variable of type double, just like n, the following is equally legal:

```
myFunction(a[3]);
```

An indexed variable can be a call-by-value argument or a call-by-reference argument. One subtlety applies to indexed variables used as arguments, however. For example, consider the following function call:

```
myFunction(a[i]);
```

If the value of i is 3, then the argument is a[3]. On the other hand, if the value of i is 0, then this call is equivalent to the following:

```
myFunction(a[0]);
```

The indexed expression is evaluated in order to determine exactly which indexed variable is given as the argument.

### Self-Test Exercises

- 11. Consider the following function definition:

  ```c
  void tripler(int& n)
  {
      n = 3 * n;
  }
  ```

  Which of the following are acceptable function calls?

  ```c
  int a[3] = {4, 5, 6}, number = 2;
  tripler(a[2]);
  tripler(a[3]);
  tripler(a[number]);
  tripler(a);
  tripler(number);
  ```

- 12. What (if anything) is wrong with the following code? The definition of `tripler` is given in Self-Test Exercise 11.

  ```c
  int b[5] = {1, 2, 3, 4, 5};
  for (int i = 1; i <= 5; i++)
      tripler(b[i]);
  ```

### Entire Arrays as Function Arguments

A function can have a formal parameter for an entire array so that when the function is called, the argument that is plugged in for this formal parameter is an entire array. However, a formal parameter for an entire array is neither a call-by-value parameter nor a call-by-reference parameter; it is a new kind of formal parameter referred to as an array parameter. Let’s start with a simple example.

The function defined in Display 5.3 has one array parameter, a, which will be replaced by an entire array when the function is called. It also has one ordinary call-by-value parameter (size) that is assumed to be an integer value equal to the size of the array. This function fills its array argument (that is, fills all the array’s indexed variables) with values typed in from the keyboard; the function then outputs a message to the screen telling the index of the last array index used.

The formal parameter int a[] is an array parameter. The square brackets, with no index expression inside, are what C++ uses to indicate an array parameter. An array parameter is not quite a call-by-reference parameter, but for most practical purposes it behaves very much like a call-by-reference parameter. Let us go through this example in detail to see how an array argument works in this case. (An array argument is, of course, an array that is plugged in for an array parameter, such as a[]).

array argument

### Display 5.3 Function with an Array Parameter

Function Declaration

```cpp
void fillUp(int a[], int size);
//Precondition: size is the declared size of the array a.
//The user will type in size integers.
//Postcondition: The array a is filled with size integers
//from the keyboard.
```

```cpp
void fillUp(int a[], int size)
{
    cout << "Enter " << size << " numbers:\n";
    for (int i = 0; i < size; i++)
        cin >> a[i];
    cout << "The last array index used is " << (size - 1) << endl;
}
```

When the function fillUp is called, it must have two arguments: the first gives an array of integers, and the second should give the declared size of the array. For example, the following is an acceptable function call:

```cpp
int score[5], numberOfScores = 5;
fillUp(score, numberOfScores);
```

when to use []

This call to fillUp will fill the array score with five integers typed in at the keyboard. Notice that the formal parameter a[] (which is used in the function declaration and the heading of the function definition) is given with square brackets but no index expression. (You may insert a number inside the square brackets for an array parameter, but the compiler will simply ignore the number, so we will not use such numbers in this book.) On the other hand, the argument given in the function call (score, in this example) is given without any square brackets or any index expression.

What happens to the array argument score in this function call? Very loosely speaking, the argument score is plugged in for the formal array parameter a in the body of the function, and then the function body is executed. Thus, the function call

```cpp
fillUp(score, numberOfScores);
```

is equivalent to the following code:

```
{
    size = 5;
    cout << "Enter " << size << " numbers:\n";
    for (int i = 0; i < size; i++)
        cin >> score[i];
    cout << "The last array index used is " << (size - 1) << endl;
}
```

5 is the value of numberOfScores.

The formal parameter a is a different kind of parameter from the ones we have seen before now. The formal parameter a is merely a placeholder for the argument score. When the function fillUp is called with score as the array argument, the computer behaves as if a were replaced with the corresponding argument score. When an array is used as an argument in a function call, any action that is performed on the array parameter is performed on the array argument, so the values of the indexed variables of the array argument can be changed by the function. If the formal parameter in the function body is changed (for example, with a cin statement), then the array argument will be changed.

So far it looks as if an array parameter is simply a call-by-reference parameter for an array. That is close to being true, but an array parameter is slightly different from a call-by-reference parameter. To help explain the difference, let us review some details about arrays.

arrays in memory

Recall that an array is stored as a contiguous chunk of memory. For example, consider the following declaration for the array score:

```cpp
int score[5];
```

When you declare this array, the computer reserves enough memory to hold five variables of type int, which are stored one after the other in the computer’s memory. The computer does not remember the addresses of each of these five indexed variables; it remembers only the address of indexed variable score[0]. The computer also remembers that score has a total of five indexed variables, all of type int. It does not remember the address in memory of any indexed variable other than score[0]. For example, when your program needs score[3], the computer calculates the address of score[3] from the address of score[0]. The computer knows that score[3] is located three int variables past score[0]. Thus, to obtain the address of score[3], the computer takes the address of score[0] and adds a number that represents the amount of memory used by three int variables; the result is the address of score[3].
