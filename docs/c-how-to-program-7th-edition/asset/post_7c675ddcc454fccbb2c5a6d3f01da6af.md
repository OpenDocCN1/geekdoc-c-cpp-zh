
## Section 8.11 Arrays of Pointers

- Arrays may contain pointers.
- Such a data structure can be used to form an array of pointer-based strings, referred to as a string array. Each entry in the array is a string, but in C++ a string is essentially a pointer to its first character, so each entry in an array of strings is simply a pointer to the first character of a string.
- String arrays are commonly used with command-line arguments that are passed to `main` when a program begins execution.

## Section 8.12 Function Pointers

- A pointer to a function is the address where the code for the function resides.
- Pointers to functions can be used to call the functions they point to, passed to functions, returned from functions, stored in arrays, assigned to other pointers.

## Terminology

| Term | Page | Term | Page |
|---|---:|---|---:|
| `*` (pointer dereference or indirection operator) | 348 | nonconstant pointer to nonconstant data | 355 |
| address operator (`&`) | 348 | null character (`'\0'`) | 370 |
| character constant | 370 | null pointer | 347 |
| command-line arguments | 373 | offset to a pointer | 368 |
| constant pointer to constant data | 358 | pass-by-reference with pointer arguments | 350 |
| constant pointer to nonconstant data | 357 | pass-by-reference with reference arguments | 350 |
| dereferencing a pointer | 348 | pointer arithmetic | 365 |
| dereferencing operator (`*`) | 348 | pointer/offset notation | 368 |
| directly references a value | 346 | pointer/subscript notation | 368 |
| function pointer | 374 | pointer to a function | 374 |
| `getline` function of `cin` | 372 | selection sort algorithm | 358 |
| indirection | 346 | `sizeof` operator | 362 |
| indirection (`*`) operator | 348 | special character | 370 |
| indirectly references a value | 346 | string array | 373 |
| nonconstant pointer to constant data | 355 | string constant | 370 |
|  |  | string literals | 370 |

## Self-Review Exercises

- 8.1 Answer each of the following:
  - a) A pointer is a variable that contains as its value the ______ of another variable.
  - b) The three values that can be used to initialize a pointer are ______, ______, and ______.
  - c) The only integer that can be assigned directly to a pointer is ______.
  - f) Use a `for` statement to print the elements of array `values` using pointer/offset notation with the array name as the pointer.
  - g) Use a `for` statement to print the elements of array `values` by subscripting the pointer to the array.
  - h) Refer to the fifth element of `values` using array subscript notation, pointer/offset notation with the array name as the pointer, pointer subscript notation and pointer/offset notation.
  - i) What address is referenced by `vPtr + 3`? What value is stored at that location?
  - j) Assuming that `vPtr` points to `values[4]`, what address is referenced by `vPtr - 4`? What value is stored at that location?

**8.9** For each of the following, write a single statement that performs the specified task. Assume that long variables `value1` and `value2` have been declared and `value1` has been initialized to 200000.

- a) Declare the variable `longPtr` to be a pointer to an object of type `long`.
- b) Assign the address of variable `value1` to pointer variable `longPtr`.
- c) Print the value of the object pointed to by `longPtr`.
- d) Assign the value of the object pointed to by `longPtr` to variable `value2`.
- e) Print the value of `value2`.
- f) Print the address of `value1`.
- g) Print the address stored in `longPtr`. Is the value printed the same as `value1`’s address?

**8.10** Perform the task specified by each of the following statements:

- a) Write the function header for function `zero` that takes a long integer array parameter `bigIntegers` and does not return a value.
- b) Write the function prototype for the function in part (a).
- c) Write the function header for function `add1AndSum` that takes an integer array parameter `oneToSmall` and returns an integer.
- d) Write the function prototype for the function described in part (c).

**8.11** Find the error in each of the following segments. If the error can be corrected, explain how.

- a)
  ```cpp
  int *number;
  cout << number << endl;
  ```
- b)
  ```cpp
  double *realPtr;
  long *integerPtr;
  integerPtr = realPtr;
  ```
- c)
  ```cpp
  int *x, y;
  x = y;
  ```
- d)
  ```cpp
  char s[] = "this is a character array";
  for ( ; *s != '\0'; s++)
      cout << *s << ' ';
  ```
- e)
  ```cpp
  short *numPtr, result;
  void *genericPtr = numPtr;
  result = *genericPtr + 7;
  ```
- f)
  ```cpp
  double x = 19.34;
  double *xPtr = &x;
  cout << *xPtr << endl;
  ```

**8.12** *(Simulation: The Tortoise and the Hare)* In this exercise, you’ll re-create the classic race of the tortoise and the hare. You’ll use random number generation to develop a simulation of this memorable event.

Our contenders begin the race at “square 1” of 70 squares. Each square represents a possible position along the racecourse. The finish line is at square 70. The first contender to reach or pass square 70 is rewarded with a pail of fresh carrots and lettuce. The course weaves its way up the side of a slippery mountain, so occasionally the contenders lose ground.

There is a clock that ticks once per second. With each tick of the clock, your program should use function moveTortoise and moveHare to adjust the positions of the animals according to the rules in Fig. 8.21. These functions should use pointer-based pass-by-reference to modify the position of the tortoise and the hare.

| Animal | Move type | Percentage of the time | Actual move |
|---|---|---|---|
| Tortoise | Fast plod | 50% | 3 squares to the right |
|  | Slip | 20% | 6 squares to the left |
|  | Slow plod | 30% | 1 square to the right |
| Hare | Sleep | 20% | No move at all |
|  | Big hop | 20% | 9 squares to the right |
|  | Big slip | 10% | 12 squares to the left |
|  | Small hop | 30% | 1 square to the right |
|  | Small slip | 20% | 2 squares to the left |

**Fig. 8.21** | Rules for moving the tortoise and the hare.

Use variables to keep track of the positions of the animals (i.e., position numbers are 1–70). Start each animal at position 1 (i.e., the "starting gate"). If an animal slips left before square 1, move the animal back to square 1.

Generate the percentages in the preceding table by producing a random integer i in the range 1 ≤ i ≤ 10. For the tortoise, perform a "fast plod" when 1 ≤ i ≤ 5, a "slip" when 6 ≤ i ≤ 7 or a "slow plod" when 8 ≤ i ≤ 10. Use a similar technique to move the hare.

Begin the race by printing

```
BANG !!!!!
AND THEY'RE OFF !!!!!
```

For each tick of the clock (i.e., each repetition of a loop), print a 70-position line showing the letter T in the tortoise's position and the letter H in the hare's position. Occasionally, the contenders land on the same square. In this case, the tortoise bites the hare and your program should print OUCH!!! beginning at that position. All print positions other than the T, the H or the OUCH!!! (in case of a tie) should be blank.

After printing each line, test whether either animal has reached or passed square 70. If so, print the winner and terminate the simulation. If the tortoise wins, print TORTOISE WINS!!! YAY!!! If the hare wins, print Hare wins. Yuch. If both animals win on the same clock tick, you may want to favor the tortoise (the "underdog"), or you may want to print It's a tie. If neither animal wins, perform the loop again to simulate the next tick of the clock.

### 8.13 What does this program do?

```cpp
1  // Ex. 8.13: ex08_13.cpp
2  // What does this program do?
3  #include <iostream>
4  using namespace std;
5
6  void mystery1( char *, const char * ); // prototype
7
```
