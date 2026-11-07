salespeople earned salaries in each of the following ranges—assume that each salesperson’s salary is truncated to an integer amount:

+   a) $200–299
+   b) $300–399
+   c) $400–499
+   d) $500–599
+   e) $600–699
+   f) $700–799
+   g) $800–899
+   h) $900–999
+   i) $1000 and over

6.11 (*Bubble Sort*) The bubble sort presented in Fig. 6.12 is inefficient for large arrays. Make the following modifications to improve its performance:

+   a) After the first pass, the largest number is guaranteed to be in the highest-numbered array element; after the second pass, the two highest numbers are “in place,” and so on. Instead of making nine comparisons on every pass, modify the bubble sort to make eight comparisons on the second pass, seven on the third pass and so on.
+   
+   b) The data in the array may already be in the proper or near-proper order, so why make nine passes if fewer will suffice? Modify the sort to check at the end of each pass whether any swaps have been made. If there were none, then the data must already be in the proper order, so the sort should terminate. If swaps have been made, then at least one more pass is needed.

6.12 Write loops that perform each of the following one-dimensional array operations:

+   a) Initialize the 10 elements of integer array counts to zeros.
+   b) Add 1 to each of the 15 elements of integer array bonus.
+   c) Read the 12 values of float array monthlyTemperatures from the keyboard.
+   d) Print the five values of integer array bestScores in column format.

6.13 Find the error(s) in each of the following statements:

+   a) Assume: `char str[5] = "";`  
+      `scanf("%s", str); // User types hello`
+   
+   b) Assume: `int a[3];`  
+      `printf("%d %d %d\n", a[1], a[2], a[3]);`
+   
+   c) `double f[3] = {1.1, 10.01, 100.001, 1000.0001};`
+   
+   d) Assume: `double d[2][10] = {0};`  
+      `d[1, 9] = 2.345;`

6.14 (*Mean, Median and Mode Program Modifications*) Modify the program of Fig. 6.13 so function mode can handle a tie for the mode value. If there are two values with the same frequency, the data is “bimodal” and both values should be displayed. If there are more than two values with the same frequency, the data is “multimodal” and all the values with the same frequency should be displayed. Also modify the me-