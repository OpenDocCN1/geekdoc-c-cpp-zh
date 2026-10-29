+   8. Write a program that outputs a histogram of grades for an assignment given to a class of students. The program should input each student’s grade as an integer and store the grade in a vector. Grades should be entered until the user enters −1 for a grade. The program should then scan through the vector and compute the histogram. In computing the histogram, the minimum value of a grade is 0, but your program should determine the maximum value entered by the user. Output the histogram to the console. See Programming Project 5.7 for information on how to compute a histogram.

+   9. Prior to 2009 the bar code on an envelope used by the U.S. Postal Service represented a five (or more) digit zip code using a format called POSTNET. The bar code consists of one long and thirty bars as shown here:

![](bbox=[0.268, 0.329, 0.837, 0.391])

For this program, we will represent the bar code as a string of digits. The digit 1 represents a long bar, and the digit 0 represents a short bar. Therefore, the bar code shown would be represented in our program as follows:

```
110010010010100101000101001
```

The first and last digits of the bar code are always 1. Removing these leave 25 digits. If these 25 digits are split into groups of five digits each then we have the following:

```
10100 10100 01010 11000 01001
```

Next, consider each group of five digits. There always will be exactly two 1’s in each group of digits. Each digit stands for a number. From left to right, the digits encode the values 7, 4, 2, 1, and 0. Multiply the corresponding value with the digit and compute the sum to get the final encoded digit for the zip code. The following table shows the encoding for 10100.

|  | 1 | 0 | 1 | 0 | 0 |
|---|---:|---:|---:|---:|---:|
| **Value** | 7 | 4 | 2 | 1 | 0 |
| **Product of Digit * Value** | 7 | 0 | 2 | 0 | 0 |

Zip Code Digit = 7 + 0 + 2 + 0 + 0 = **9**

Repeat this for each group of five digits and concatenate to get the complete zip code. There is one special value. If the sum of a group of five digits is 11, then this represents the digit 0 (this is necessary because with two digits per group it is not possible to represent zero). The zip code for the sample bar code decodes to 90504. While the POSTNET scheme may seem unnecessarily complex, its design allows machines to detect whether errors have been made in scanning the zip code.