+   c) Initialize each of the 5 elements of one-dimensional integer array g to 8.
+   d) Total and print the elements of floating-point array c of 100 elements.
+   e) Copy array a into the first portion of array b. Assume double a[ 11 ], b[ 34 ];
+   f) Determine and print the smallest and largest values contained in 99-element floating-point array w.

7.9 Consider a 2-by-3 integer array t.

+   a) Write a declaration for t.
+   b) How many rows does t have?
+   c) How many columns does t have?
+   d) How many elements does t have?
+   e) Write the names of all the elements in row 1 of t.
+   f) Write the names of all the elements in column 2 of t.
+   g) Write a single statement that sets the element of t in the first row and second column to zero.
+   h) Write a series of statements that initialize each element of t to zero. Do not use a loop.
+   i) Write a nested for statement that initializes each element of t to zero.
+   j) Write a statement that inputs the values for the elements of t from the keyboard.
+   k) Write a series of statements that determine and print the smallest value in array t.
+   l) Write a statement that displays the elements in row 0 of t.
+   m) Write a statement that totals the elements in column 3 of t.
+   n) Write a series of statements that prints the array t in neat, tabular format. List the column subscripts as headings across the top and list the row subscripts at the left of each row.

7.10 *(Salesperson Salary Ranges)* Use a one-dimensional array to solve the following problem. A company pays its salespeople on a commission basis. The salespeople each receive $200 per week plus 9 percent of their gross sales for that week. For example, a salesperson who grosses $5000 in sales in a week receives $200 plus 9 percent of $5000, or a total of $650. Write a program (using an array of counters) that determines how many of the salespeople earned salaries in each of the following ranges (assume that each salesperson's salary is truncated to an integer amount):

+   a) $200–299
+   b) $300–399
+   c) $400–499
+   d) $500–599
+   e) $600–699
+   f) $700–799
+   g) $800–899
+   h) $900–999
+   i) $1000 and over

7.11 *(Bubble Sort)* In the bubble sort algorithm, smaller values gradually "bubble" their way upward to the top of the array like air bubbles rising in water, while the larger values sink to the bottom. The bubble sort makes several passes through the array. On each pass, successive pairs of elements are compared. If a pair is in increasing order (or the values are identical), we leave the values as they are. If a pair is in decreasing order, their values are swapped in the array. Write a program that sorts an array of 10 integers using bubble sort.

7.12 *(Bubble Sort Enhancements)* The bubble sort described in Exercise 7.11 is inefficient for large arrays. Make the following simple modifications to improve the performance of the bubble sort:

+   a) After the first pass, the largest number is guaranteed to be in the highest-numbered element of the array; after the second pass, the two highest numbers are "in place," and so on. Instead of making nine comparisons on every pass, modify the bubble sort to make eight comparisons on the second pass, seven on the third pass, and so on.