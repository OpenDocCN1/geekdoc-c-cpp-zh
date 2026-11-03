Write a program to read the table elements into a two-dimensional array temperature, and to find the city and day corresponding to (a) the highest temperature and (b) the lowest temperature.

# 3.3

An election is contested by 5 candidates. The candidates are numbered 1 to 5 and the voting is done by marking the candidate number on the ballot paper. Write a program to read the ballots and count the votes cast for each candidate using an array variable count. In case, a number read is outside the range 1 to 5, the ballot should be considered as a 'spoilt ballot' and the program should also count the number of spoilt ballots.

# 3.4

The following set of numbers is popularly known as Pascal's triangle.

1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
1 5 10 10 5 1
- - - - - - -
- - - - - - -

If we denote rows by i and columns by j, then any element (except the boundary elements) in the triangle is given by
p_ij = p_{i-1,j-1} + p_{i-1,j}

Write a program to calculate the elements of the Pascal triangle for 10 rows and print the results.

# 3.5

The annual examination results of 100 students are tabulated as follows:

| Roll No. | Subject 1 | Subject 2 | Subject 3 |
|---|---|---|---|
| . | . | . | . |
| . | . | . | . |

Write a program to read the data and determine the following:
(a) Total marks obtained by each student.
(b) The highest marks in each subject and the Roll No. of the student who secured it.
(c) The student who obtained the highest total marks.

# 3.6

Given are two one-dimensional arrays A and B which are sorted in ascending order. Write a program to merge them into a single sorted array C that contains every item from arrays A and B, in ascending order.

# 3.7

Two matrices that have the same number of rows and columns can be multiplied to produce a third matrix. Consider the following two matrices
A = [ a11 a12 ..... a1n ; a21 a22 ..... a2n ; . . . ; an1 ..... ann ]
B = [ b11 b12 ..... b1n ; b21 b22 ..... b2n ; . . . ; bn1 ..... bnn ]
The product of A and B is a third matrix C of size n × n where each element of C is given by the following equation.
C_ij = a_ik b_kj
Write a program that will read the values of elements of A and B and produce the product matrix C.

# 3.8

Write a program that fills a five-by-five matrix as follows:

+   - Upper left triangle with +1s
+   - Lower right triangle with −1s
+   - Right to left diagonal with zeros

Display the contents of the matrix using not more than two printf statements

# 3.9

Selection sort is based on the following idea: Selecting the largest array element and swapping it with the last array element leaves an unsorted list whose size is 1 less than the size of the original list. If we repeat this step again on the unsorted list we will have an ordered list of size 2 and an unordered list