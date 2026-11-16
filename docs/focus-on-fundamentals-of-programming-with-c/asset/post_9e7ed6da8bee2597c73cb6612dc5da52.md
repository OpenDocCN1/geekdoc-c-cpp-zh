
## Chapter 14. Storage Class ................ 367

- Storage Class ................................. 368
- Storage Location .............................. 375
- ♦ Storage Class Homework ........................ 376

## Chapter 15. Preprocessor ................. 377

- Preprocessor .................................. 378
- ♦ Preprocessor Homework ......................... 385
- ♦ Preprocessor Lab .............................. 386

## Chapter 16. Enumerations & Typedef Statement ... 388

- Enumerations .................................. 389
- Typedef Statement ............................. 393
- ♦ Enumerations & Typedef Homework ............... 395

## Chapter 17. Structures ................... 397

- Introduction to Structures .................... 398
- Manipulating Entire Structures ................ 402
- Struct Example: Today's Date and Tomorrow's Date ... 406
- Arrays of Structures .......................... 412

- Nesting Structures ........................................................ 415
- ✦ Structures Homework .................................................... 418
- ✦ Database Lab............................................................ 419

## Chapter 18. Dynamic Allocation of Variables ........................ 422

- Dynamic Allocation of Variables......................................... 423
- Dynamic Arrays - Advanced............................................... 430

## Chapter 19. Linear Linked Lists ........................................ 436

- Introduction to Linear Linked Lists .................................... 437
- Operations on Linear Linked Lists....................................... 441
- Three List Algorithms..................................................... 443
- Additional List Operations................................................ 451
- Linear Linked List Examples ............................................ 456
- ✦ Linear Linked List Homework........................................... 458

## Chapter 20. Implementation of Linear Linked Lists .................... 459

- Defining Nodes in C ...................................................... 460
- Linear Linked List Operations .......................................... 462
- Separate Compilation...................................................... 470
- Linear Linked List Code .................................................. 473
- Addition of Polynomials................................................... 482
- ✦ Linear Linked List Lab.................................................... 486
- ✦ Calculating Very Large Factorials Lab................................ 494

## Chapter 21. Bitwise Operators ............................................ 500

- Introduction to Bitwise Operators ...................................... 501
- Bitwise And .................................................................... 502
- Masks............................................................................. 505
- WordStar.......................................................................... 508
- Bitwise Or........................................................................ 510

- Bitwise Exclusive-Or .................................................................... 513
- Bitwise Negate ............................................................................ 516
- Left Shift Operator ....................................................................... 518
- Right Shift Operator ...................................................................... 520
- Rotate Example .............................................................................. 523
- ❖ Bitwise Operator Homework ........................................................... 525
- ❖ Bitwise Operator Lab ...................................................................... 526

## Chapter 22. An Overview of Object-Oriented Programming .................... 529

- Introduction to Object-Oriented Programming .................................... 530
- OOP is Programming by Simulation .................................................... 539
- OOP is Programming with Objects ....................................................... 555
- OOP is Programming with Messages .................................................... 566
- OOP is Programming with Classes ....................................................... 569
- OOP is Programming with Encapsulation ............................................. 574
- OOP is Programming with Inheritance ................................................. 579
- OOP is Programming with Polymorphism .............................................. 593
- Object-Oriented Languages ............................................................... 602

## Chapter 1. Algorithms

### Introduction to Algorithms

### Stepwise Refinement – Part 1

### Stepwise Refinement – Part 2

.c --> compile --> link --> .exe
BUILD
Can be done in VS 2005 IDE

### An introduction to Algorithms

An algorithm is a step-by-step process for solving a problem. For example, let's explore an algorithm for driving a car. Here are the steps:

- Open the car door.
- Enter the car.
- Close the door.
- Put on your seat belt.
- Put the key in the ignition and turn on the ignition.
- Put the car in drive.
- Step on the gas.

Did we omit any steps?

### Greatest Common Divisor

Sometimes an algorithm can be more mathematical in nature. Actually the oldest known arithmetic algorithm was reported around 300 B.C. by Euclid and is a method for computing the greatest common divisor of two whole numbers. The greatest common divisor is the largest whole number that divides both numbers without remainders.

If the two numbers are A and B, Euclid's algorithm is as follows:

- 1. Compute the remainder of the division of A and B.
- 2. Replace A by B.
- 3. Replace B by the remainder computed in step 1.
- 4. Repeat steps 1 - 3 until B is zero.
- 5. The greatest common divisor is the final value of A.

For example, find the greatest common divisor of A = 24 and B = 9:

```
1. The remainder of 24 / 9 = 6.
2. A = 9.
3. B = 6.
4. Repeat steps 1 - 3.

1. The remainder of 9 / 6 = 3.
2. A = 6.
3. B = 3.
4. Repeat steps 1 - 3.

1. The remainder of 6 / 3 = 0.
2. A = 3.
3. B = 0.
5. The greatest common divisor is 3.
```

There are typically three important features of an algorithm:

- 1. The algorithm must have a finite number of instructions or steps.
- 2. Each instruction in the algorithm is well defined (not ambiguous).
- 3. The algorithm eventually halts.

A computer program is also an example of an algorithm. In fact, here's a program written in C to compute the greatest common divisor of two numbers following Euclid's algorithm:

```
// Program to calculate the greatest common divisor of two numbers

#include <stdio.h>

int main(void) {
    int A, B, remainder;

    printf("Enter two positive integers: ");
    scanf("%d%d", &A, &B);

    while (B != 0) {
        remainder = A % B;
        A = B;
        B = remainder;
    }

    printf("The greatest common divisor = %d\n", A);

    return 0;
}
```

### Stepwise Refinement – Part 1

To show you an example of top-down design or stepwise refinement, we'll take the act of making scrambled eggs. Starting from the top we have the task to:

- Make scrambled eggs

But saying that by itself isn't enough to actually make any scrambled eggs, so we need to break the task down:

- Make some scrambled eggs
  - 1. Organise the kitchen
  - 2. Make scrambled eggs
  - 3. Serve the scrambled eggs

Each of these tasks can then be broken down further:

- 1. Organize the kitchen
  - 1. Clean surfaces
  - 2. Get out mixing bowl, whisk, spoon
  - 3. Get out eggs, salt, milk, and butter
  - 4. Put on apron

- 2. Make scrambled eggs
  - 1. Break eggs into bowl
  - 2. Whisk the eggs
  - 3. Add water and milk to the bowl
  - 4. Whisk
  - 5. Cook the scrambled eggs

- 3. Serve the scrambled eggs

And each of these tasks can be broken down further, let us take a look at the Cook the scrambled eggs component:
