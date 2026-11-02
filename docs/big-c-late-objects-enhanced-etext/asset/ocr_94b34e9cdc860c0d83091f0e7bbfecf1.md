This plan will work—see Section 6.4. But there is an alternate approach. It is easy to compute the sum and subtract the minimum. Then we don't have to find its position. The revised plan is

+   - Read inputs.
+   - Find the minimum.
+   - Calculate the sum.
+   - Subtract the minimum from the sum.

# Step 3 Use functions to structure the program.

Even though it may be possible to put all steps into the main function, this is rarely a good idea. It is better to make each processing step into a separate function. In our example, we will implement three functions:

+   - `read_inputs`
+   - `sum`
+   - `minimum`

The main function simply calls these functions:

```
const int CAPACITY = 1000;
double scores[CAPACITY];
int scores_size = read_inputs(scores, CAPACITY);
double total = sum(scores, scores_size) - minimum(scores, scores_size);
```

For each function that processes an array, you will need to pass the array itself and the array size. For example,

```
double sum(double values[], int size)
```

If the function modifies the size, it needs to tell the caller what the new size is. The function reading inputs returns the new size:

```
int read_inputs(double inputs[], int capacity) // Returns the size
```

# Step 4 Assemble and test the program.

Combine your functions into a program. Review your code and check that you handle both normal and exceptional situations. What happens with an empty array? One that contains a single element? When no match is found? When there are multiple matches? Consider these boundary conditions and make sure that your program works correctly.

In our example, it is impossible to compute the minimum if the array is empty. In that case, we should terminate the program with an error message before attempting to call the main function.

What if the minimum value occurs more than once? That means that a student had more than one test with the same low score. We subtract only one of the occurrences of that low score, and that is the desired behavior.

The following table shows test cases and their expected output:

| Test Case | Expected Output | Comment |
|---|---|---|
| 8 7 8.5 9.5 7 5 10 | 50 | See Step 1. |
| 8 7 7 9 | 24 | Only one instance of the low score should be removed. |
| 8 | 0 | After removing the low score, no score remains. |
| (no inputs) | Error | That is not a legal input. |