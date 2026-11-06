
- c. Two-dimensional arrays always have the same number of rows and columns.
- d. Elements of different columns in a two-dimensional array can have different types.
- e. A function cannot return a two-dimensional array.
- f. All array parameters are reference parameters.
- g. A function cannot change the dimensions of a two-dimensional array that is passed as a parameter.

### R6.25
How do you perform the following tasks with vectors in C++?

- a. Test that two vectors contain the same elements in the same order.
- b. Copy one vector to another.
- c. Fill a vector with zeroes, overwriting all elements in it.
- d. Remove all elements from a vector.

### R6.26
True or false?

- a. All elements of a vector are of the same type.
- b. Vector subscripts must be integers.
- c. Vectors cannot contain strings as elements.
- d. Vectors cannot use strings as subscripts.
- e. All vector parameters are reference parameters.
- f. A function cannot return a vector.
- g. A function cannot change the length of a vector that is a reference parameter.

## PROGRAMMING EXERCISES

### P6.1
Write a program that initializes an array with ten random integers and then prints four lines of output, containing

- Every element at an even index.
- Every even element.
- All elements in reverse order.
- Only the first and last element.

### P6.2
Write array functions that carry out the following tasks for an array of integers:

- a. Swap the first and last element in an array.
- b. Shift all elements by one to the right and move the last element into the first position. For example, 1 4 9 16 25 would be transformed into 25 1 4 9 16.
- c. Replace all even elements with 0.
- d. Replace each element except the first and last by the larger of its two neighbors.
- e. Remove the middle element if the array length is odd, or the middle two elements if the length is even.
- f. Move all even elements to the front, otherwise preserving the order of the elements.
- g. Return the second-largest element in the array.

and

11 1 4 9 16 9 7 4 9

would be considered identical, but

1 4 9 16 9 7 4 9 11

and

11 11 7 9 16 4 1 4 9

would not. You will probably need one or more helper functions.

### P6.12
Write a function that removes duplicates from an array. For example, if `remove_duplicates` is called with an array containing

1 4 9 16 9 7 4 9 11

then the array is changed to

1 4 9 16 7 11

Your function should have a reference parameter for the array size that is updated when removing the duplicates.

### P6.13
A *run* is a sequence of adjacent repeated values. Write a program that generates a sequence of 20 random die tosses and prints the die values, marking the runs by including them in parentheses, like this:

1 2 (5 5) 3 1 2 4 3 (2 2 2 2) 3 6 (5 5) 6 3 1

Use the following pseudocode:

```text
Set a Boolean variable in_run to false.
For each valid index i in the array
   If in_run
      If values[i] is different from the preceding value
         Print ).
         in_run = false
   If not in_run
      If values[i] is the same as the following value
         Print (.
         in_run = true
   Print values[i].
If in_run, print ).
```

### P6.14
Write a program that generates a sequence of 20 random die tosses and that prints the die values, marking only the longest run, like this:

1 2 5 5 3 1 2 4 3 (2 2 2 2) 3 6 5 5 6 3 1

If there is more than one run of maximum length, mark the first one.

### P6.15
Write a program that generates a sequence of 20 random values between 0 and 99, prints the sequence, sorts it, and prints the sorted sequence. Use the sort function from the standard C++ library.

### P6.16
Write a program that produces ten random permutations of the numbers 1 to 10. To generate a random permutation, you need to fill an array with the numbers 1 to 10 so that no two elements have the same contents. You could do it by brute force, by generating random values until you have a value that is not yet in the array. But that is inefficient. Instead, follow this algorithm:

- Make a second array and fill it with the numbers 1 to 10.
- Repeat 10 times
  - Pick a random element from the second array.
  - Remove it and append it to the permutation array.

### P6.17
It is a well-researched fact that men in a restroom generally prefer to maximize their distance from already occupied stalls, by occupying the middle of the longest sequence of unoccupied places.

For example, consider the situation where all ten stalls are empty.

`- - - - - - - - - -`

The first visitor will occupy a middle position:

`- - - - X - - - - -`

The next visitor will be in the middle of the empty area at the right.

`- - - - X - - X - -`

Given an array of bool values, where true indicates an occupied stall, find the position for the next visitor. Your computation should be placed in a function

```cpp
next_visitor(bool occupied[], int stalls)
```

### P6.18
In this assignment, you will model the game of *Bulgarian Solitaire*. The game starts with 45 cards. (They need not be playing cards. Unmarked index cards work just as well.) Randomly divide them into some number of piles of random size. For example, you might start with piles of size 20, 5, 1, 9, and 10. In each round, you take one card from each pile, forming a new pile with these cards. For example, the sample starting configuration would be transformed into piles of size 19, 4, 8, 9, and 5. The solitaire is over when the piles have size 1, 2, 3, 4, 5, 6, 7, 8, and 9, in some order. (It can be shown that you always end up with such a configuration.)

In your program, produce a random starting configuration and print it. Then keep applying the solitaire step and print the result. Stop when the solitaire final configuration is reached.

### P6.19
*Magic squares.* An n × n matrix that is filled with the numbers 1, 2, 3, . . . , n² is a magic square if the sum of the elements in each row, in each column, and in the two diagonals is the same value.

| 16 | 3 | 2 | 13 |
|----|----|----|----|
| 5 | 10 | 11 | 8 |
| 9 | 6 | 7 | 12 |
| 4 | 15 | 14 | 1 |

Write a program that reads in 16 values from the keyboard and tests whether they form a magic square when put into a 4 × 4 array. You need to test two features:

- 1. Does each of the numbers 1, 2, ..., 16 occur in the user input?
- 2. When the numbers are put into a square, are the sums of the rows, columns, and diagonals equal to each other?

### P6.20
Implement the following algorithm to construct magic n × n squares; it works only if n is odd.

Then write a program that reads one hundred terrain height values and shows how the terrain gets flooded when the water level increases in ten steps from the lowest point in the terrain to the highest.

### Engineering P6.34
Modify the ch06/image.cpp program in the book's companion code to generate the image of a sine wave.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_329_0.png)

Draw a line of pixels for every five degrees.

### Engineering P6.35
Modify the ch06/animation.cpp program to show an animated sine wave. In the ith frame, shift the sine wave by 5 × i degrees.

### Engineering P6.36
Write a program that models the movement of an object with mass m that is attached to an oscillating spring. When a spring is displaced from its equilibrium position by an amount x, Hooke's law states that the restoring force is

$F = -kx$

where k is a constant that depends on the spring. (Use 10 N/m for this simulation.)

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_329_1.png)

Start with a given displacement x (say, 0.5 meter). Set the initial velocity v to 0. Compute the acceleration a from Newton's law (F = ma) and Hooke's law, using a mass of 1 kg. Use a small time interval Δt = 0.01 second. Update the velocity—it changes by aΔt. Update the displacement—it changes by vΔt. Every ten iterations, plot the spring displacement as a bar, where 1 pixel represents 1 cm. Modify the program ch06/image.cpp for creating an image.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_329_2.png)
