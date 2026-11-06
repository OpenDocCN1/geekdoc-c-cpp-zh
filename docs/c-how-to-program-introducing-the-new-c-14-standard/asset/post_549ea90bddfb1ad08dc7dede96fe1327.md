
numbers `x` and `y` as parameters and does not return a value.

- B. Write the function prototype without parameter names for the function in part (a).

- C. Write two statements that each initialize the built-in array of `char`s named `vowel` with the string of vowels, `"AEIOU"`.

### 6. 8.6 Find the error in each of the following program segments.

Assume the following declarations and statements:

```cpp
int* zPtr; // zPtr will reference built-in array z
int number;
int z[5]{1, 2, 3, 4, 5};
```

- A.

```cpp
++zPtr;
```

- B.

```cpp
// use pointer to get first value of a built-in
// array
number = zPtr;
```

- C.

```cpp
// assign built-in array element 2 (the value 3) to
// number
number = *zPtr[2];
```

- D.

```cpp
// display entire built-in array z

for (size_t i(0); i <= 5; ++i) {
    cout << zPtr[i] << endl;
}
```

- E.

```cpp
++z;
```

## Exercises

### 1. 8.7 (True or False)

State whether the following are *true* or *false*. If false, explain why.

- A. Two pointers that point to different built-in arrays cannot be compared meaningfully.
- B. Because the name of a built-in array is implicitly convertible to a pointer to the first element of the built-in array, built-in array names can be manipulated in the same manner as pointers.

### 2. 8.8 (Write C++ Statements)

For each of the following, write C++ statements that perform the specified task. Assume that unsigned integers are stored in four bytes and that the starting address of the built-in array is at location 1002500 in memory.

- A. Declare an `unsigned int` built-in array `values` with five elements initialized to the even integers from 2 to 10. Assume that the constant `size` has been defined as `5`.
- B. Declare a pointer `vPtr` that points to an object of type `unsigned int`.
- C. Use a `for` statement to display the elements of built-in array `values` using array subscript notation.
- D. Write two separate statements that assign the starting address of built-in array `values` to pointer variable `vPtr`.
- E. Use a `for` statement to display the elements of built-in array `values` using pointer/offset notation.
- F. Use a `for` statement to display the elements of built-in array `values` using pointer/offset notation with the built-in array’s name as the pointer.
- G. Use a `for` statement to display the elements of built-in array `values` by subscripting the pointer to the built-in array.
- H. Refer to the fifth element of `values` using array subscript notation, pointer/offset notation with the built-in array name’s as the pointer, pointer subscript notation and pointer/offset notation.
- I. What address is referenced by `vPtr + 3`? What value is stored at that location?
- J. Assuming that `vPtr` points to `values[4]`, what address is referenced by `vPtr -= 4`? What value is stored at that location?

### 3. 8.9 (Write C++ Statements)

For each of the following, write a single statement that performs the specified task. Assume that `long` variables `value1` and `value2` have been declared and `value1` has been initialized to `200000`.

- A. Declare the variable `longPtr` to be a pointer to an object of type `long`.
- B. Assign the address of variable `value1` to pointer variable `longPtr`.
- C. Display the value of the object pointed to by `longPtr`.
- D. Assign the value of the object pointed to by `longPtr` to variable `value2`.
- E. Display the value of `value2`.
- F. Display the address of `value1`.
- G. Display the address stored in `longPtr`. Is the address displayed the same as `value1`’s?

### 4. 8.10 (Function Headers and Prototypes)

Perform the task in each of the following:

- A. Write the function header for function `zero` that takes a long integer built-in array parameter `bigIntegers` and a second parameter representing the array’s size and does not return a value.
- B. Write the function prototype for the function in part (a).
- C. Write the function header for function `add1AndSum` that takes an integer built-in array parameter `oneTooSmall` and a second parameter representing the array’s size and returns an integer.
- D. Write the function prototype for the function described in part (c).

### 5. 8.11 (Find the Code Errors)

Find the error in each of the following segments. If the error can be corrected, explain how.

- A.

```cpp
int* number;
cout << number << endl;
```

- B.

```cpp
double* realPtr;
long* integerPtr;
integerPtr = realPtr;
```

- C.

```cpp
int* x, Y;
x = Y;
```

- D.

```cpp
char s[]={"this is a character array"};
for (; *s != '\0'; ++s) {
    cout << *s << ' ';
}
```

- E.

```cpp
short* numPtr, result;
void* genericPtr(numPtr);
result = *genericPtr + 7;
```

- F.

```cpp
double x = 19.34;
double xPtr{&x};
cout << xPtr << endl;
```

### 6. 8.12 (Simulation: The Tortoise and the Hare)

In this exercise, you’ll re-create the classic race of the tortoise and the hare. You’ll use random-number generation to develop a simulation of this memorable event.

Our contenders begin the race at “square 1” of 70 squares. Each square represents a possible position along the race course. The finish line is at square 70. The first contender to reach or pass square 70 is rewarded with a pail of fresh carrots and lettuce. The course weaves its way up the side of a slippery mountain, so occasionally the contenders lose ground. There is a clock that ticks once per second. With each tick of the clock, your program should use function `moveTortoise` and `moveHare` to adjust the position of the animals according to the rules in **Fig. 8.18**. These functions should use pointer-based pass-by-reference to modify the position of the tortoise and the hare.

**Fig. 8.18 Rules for moving the tortoise and the hare.**

| Animal | Move type | Percentage of the time | Actual move |
|---|---|---:|---|
| Tortoise | Fast plod | 50% | 3 squares to the right |
| Tortoise | Slip | 20% | 6 squares to the left |
| Tortoise | Slow plod | 30% | 1 square to the right |
| Hare | Sleep | 20% | No move at all |
| Hare | Big hop | 20% | 9 squares to the right |
| Hare | Big slip | 10% | 12 squares to the left |
| Hare | Small hop | 30% | 1 square to the right |
| Hare | Small slip | 20% | 2 squares to the left |

Use variables to keep track of the positions of the animals (i.e., position numbers are 1–70). Start each animal at position 1 (i.e., the “starting gate”). If an animal slips left before square 1, move the animal back to square 1. Generate the percentages in **Fig. 8.18** by producing a random integer *i* in the range 1 ≤ *i* ≤ 10. For the tortoise, perform a “fast plod” when 1 ≤ *i* ≤ 5, a “slip” when 6 ≤ *i* ≤ 7 or a “slow plod” when 8 ≤ *i* ≤ 10. Use a similar technique to move the hare. Begin the race by displaying

```text
BANG !!!!!
AND THEY'RE OFF !!!!!
```

For each tick of the clock (i.e., each iteration of a loop), display a 70-position line showing the letter `T` in the tortoise’s position and the letter `H` in the hare’s position. Occasionally, the contenders land on the same square. In this case, the tortoise bites the hare and your program should display `OUCH!!!` beginning at that position. All positions other than the `T`, the `H` or the `OUCH!!!` (in case of a tie) should be blank.

After displaying each line, test whether either animal has reached or passed square 70. If so, display the winner and terminate the simulation. If the tortoise wins, display `TORTOISE WINS!!! YAY!!!` If the hare wins, display `Hare wins. Yuch.` If both animals win on the same clock tick, you may want to favor the tortoise (the “underdog”), or you may want to display `It’s a tie.` If neither animal wins, perform the loop again to simulate the next tick of the clock.

### 7. 8.13 (What Does This Code Do?)

What does this program do?
