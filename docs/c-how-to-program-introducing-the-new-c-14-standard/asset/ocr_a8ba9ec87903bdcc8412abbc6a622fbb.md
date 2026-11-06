placed in row 3 and 100 is placed in row 0. This procedure is called a *distribution pass*.

+   B. Loop through the bucket `array` row by row, and copy the values back to the original `array`. This procedure is called a *gathering pass*. The new order of the preceding values in the one-dimensional `array` is 100, 3 and 97.
+   
+   C. Repeat this process for each subsequent digit position (tens, hundreds, thousands, etc.).

On the second (tens digit) pass, 100 is placed in row 0, 3 is placed in row 0 (because 3 has no tens digit) and 97 is placed in row 9. After the gathering pass, the order of the values in the one-dimensional `array` is 100, 3 and 97. On the third (hundreds digit) pass, 100 is placed in row 1, 3 is placed in row 0 and 97 is placed in row 0 (after the 3). After this last gathering pass, the original `array` is in sorted order.

Note that the two-dimensional `array` of buckets is 10 times the length of the integer `array` being sorted. This sorting technique provides better performance than a bubble sort, but requires much more memory—the bubble sort requires space for only one additional element of data. This comparison is an example of the space–time trade-off. The bucket sort uses more memory than the bubble sort, but performs better. This version of the bucket sort requires copying all the data back to the original `array` on each pass. Another possibility is to create a second two-dimensional bucket `array` and repeatedly swap the data between the two bucket `array`s.