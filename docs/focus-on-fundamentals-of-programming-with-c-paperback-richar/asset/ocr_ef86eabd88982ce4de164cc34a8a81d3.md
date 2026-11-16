# An introduction to Algorithms

An algorithm is a step-by-step process for solving a problem. For example, let's explore an algorithm for driving a car. Here are the steps:

```
Open the car door.
Enter the car.
Close the door.
Put on your seat belt.
Put the key in the ignition and turn on the ignition.
Put the car in drive.
Step on the gas.
```

Did we omit any steps?

# Greatest Common Divisor

Sometimes an algorithm can be more mathematical in nature. Actually the oldest known arithmetic algorithm was reported around 300 B.C. by Euclid and is a method for computing the greatest common divisor of two whole numbers. The greatest common divisor is the largest whole number that divides both numbers without remainders.

If the two numbers are A and B, Euclid's algorithm is as follows:

```
1. Compute the remainder of the division of A and B.
2. Replace A by B.
3. Replace B by the remainder computed in step 1.
4. Repeat steps 1 - 3 until B is zero.
5. The greatest common divisor is the final value of A.
```