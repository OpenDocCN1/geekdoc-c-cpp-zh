The `print()` function comment #3 identifies allows you a bit more control over the element from the hash. In this instance, as Figure 8.4 shows, you see the first few elements of the array as keys and values. The `printf()` function accesses keys and values sequentially. You employ a `%s` specifier for each item you want to see. You also employ the implicit form (`%`) of the hash.

Comment #4 introduces the most convenient approach to accessing the keys and values stored in a hash. You first assign the implicit form of the hash to an array (`@ElementArray`). As the `printf()` example discussed previously reveals, the hash stores the key-value pairs in a continuous list, so when you use the assignment operator, you transfer an alternating list of keys and values to the array.

You can then print the list. One approach involves printing the contents of the interpolated array. As Figure 8.4 illustrates, the result appears as a somewhat unsightly series of terms, but you still see spaces between the items. Alternatively, you can use a `foreach` statement to iterate through the list and print each of its elements on separate lines. The `foreach` statement continues to read the array until it reaches an undefined element that marks the end of the array.

Comment #5 introduces an innovation that you are not likely to use, but it shows you that you can fold control statements, flags, and the `printf()` function for formatting. This example allows you to fetch the elements from an array (`@ElementArray`). Using the `foreach` statement, you iterate through the array as before, but this time, you employ selection statements inside the `foreach` loop to retrieve keys and values alternatively and display them in formatted columns.

The example following comment #5, as well as the other examples shown in Listing08_03, are intended purely as introductory demonstrations. The Perl functions and control statements provide much more elegant approaches to accessing keys and values in a hash. Subsequent sections of this chapter, along with examples in Chapters 9 and 10, provide further discussion. Here are a few common approaches:

+   - Use the `keys()` function to transfer the keys to an array.
+   - Use the `values()` function to transfer the values to an array.
+   - Employ the `each()` function to access both the keys and the values.