# Arrays Homework

1. Write some code to perform each of the following tasks:

+   a) Define a constant `MAX` that holds a value of 50.
+   b) Define an array of integers, `num`, containing `MAX` elements and initialize each of the elements of the array to 0.
+   c) What is the name of the fourth element of the array?
+   d) Output the value of the sixth element of the array.
+   e) Assign a value into the third element of array `num`.
+   f) Initialize each of the 50 elements of the array to 500.
+   g) Sum up the elements of array `num` into summation variable `sum`.
+   h) Copy the contents of array `num` into array `foo`, also of size `MAX`.
+   i) Increment each element of array `foo` by a value of 1.

2. The code below assigns a random number from 1 to 10,000 into each element of array num. Write a function that receives the array as a parameter and returns the smallest value of array.

```
srand((unsigned int) time(NULL));
for (i = 0; i < MAX; ++i) {
    num[i] = rand() % 10000 + 1;
}
```

3. As a practical joke, a friend gives you an int array for your birthday. As if that weren't bad enough, your friend tells you that the array contains almost all 0's except for a small string of consecutive 1's contained somewhere in the middle. Overwhelmed by the novelty of this you decide to write a function that will print out the location of the first 1 in the array, the location of the last 1 in the array, and the total number of 1's in the list of consecutive 1 values. Given below is the function prototype: