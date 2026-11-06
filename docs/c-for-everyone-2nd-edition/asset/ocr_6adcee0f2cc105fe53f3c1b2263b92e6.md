We discussed the algorithm for `min_position` in the preceding section:

```
```cpp
/**
   Gets the position of the minimum value from an array.
   @param values a partially filled array
   @param size the number of elements in values
   @return the position of the smallest element in values
*/
int min_position(double values[], int size)
{
   int smallest_position = 0;
   for (int i = 1; i < size; i++)
   {
      if (values[i] < values[smallest_position])
      {
         smallest_position = i;
      }
   }
   return smallest_position;
}
```
```

The remaining helper functions use the algorithms from Section 6.2. You will find the implementations in the book's companion code.

# Step 4 Consider boundary conditions for the functions that you are implementing

Most functions that operate on arrays are a bit intricate, and you have to be careful that you handle both normal and exceptional situations. What happens with an empty array? An array that contains a single element? When no match is found? When there are multiple matches? Consider these boundary conditions and make sure that your functions work correctly.

Here is one example of such a consideration. How do we know that the `min_position` function will be called with an array of size at least 1? (Recall that you must have at least one element in order to find the minimum.) That function is called from the `final_score` function. However, the `final_score` function could conceivably be called with an empty array. We need to either include a test or add a restriction to the function comment. We will opt for the latter and change the comment for the `values` parameter variable of the `min_position` function to

```
```cpp
@param values a partially filled array of size >= 1
```
```

Consider another potential problem. What if there are multiple matches? That means that a student had more than one test with a low score. The `final_score` function removes only one of the occurrences of that low score, and that is the desired behavior.

# Step 5 Assemble and test the complete program.

Now we are ready to combine the individual functions into a complete program. Before doing this, consider some test cases and their expected output:

| Test Case | Expected Output | Comment |
| :--- | :---: | :--- |
| 8 7 8.5 9.5 7 5 10 | 50 | See Step 1. |
| 8 7 7 9 | 24 | Only one instance of the low score should be removed. |
| 8 | 0 | After removing the low score, no score remains. |
| (no inputs) | **Error** | That is not a legal input. |