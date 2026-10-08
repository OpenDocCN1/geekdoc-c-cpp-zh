logically correct for 99% of the times. Table 1 gives the trace of the flowchart shown in Figure 5:

Table 1: Trace Table to Calculate the Area of the Rectangular Surface

| Case No. | Input 1 length | length > 0 | Input 2 breadth | breadth > 0 | Output |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 150 | True | 200 | True | Area = 30000 |
| 2 | 0 | False | -- | -- | Error in input |
| 3 | -100 | False | -- | -- | Error in input |
| 4 | 50 | True | 0 | False | Error in input |
| 5 | 75 | True | -125 | False | Error in input |
| 6 | 225 | True | 125 | True | Area = 28125 |

As shown in Table 1, the results now depend on the entered values of length and breadth. In case numbers 1 and 6, two different values of an area are obtained, while in all other cases, we are getting an error. The - - in the table entry indicates that these instructions did not get executed at all. From now onward, we will devise generalized solutions for given problems. The algorithm for the generalized solution for the preceding problem is mentioned as follows:

+   Step 1: Start

Step 2: Define length, breadth, and area

Step 3: Accept value of length.

Step 4: If length > 0 go to step 5

			Else go to step 9

Step 5: Accept value of breadth

Step 6: If breadth > 0 go to step 7

			Else go to step 9

Step 7: area = length × breadth

Step 8: Print value of area go to step 10

Step 9: Print "Error in input"  

Step 10: Stop

# **Example 2:**

Find whether a number $y$ is a factor of number $x$.

Solution 2:

+   a.  Using a flowchart to find whether a number $y$ is a factor of number $x$.

The number $y$ would be considered as a factor of number $x$ if and only if $x$ is fully divisible by $y$, i.e., the remainder is always zero. In addition, if the number $y$ is greater than number $x$, then there is no need to perform the division operation as the factor would be always smaller than the multiple. Assume that the number $x$ is represented by a variable *num1* and the number $y$ is represented by another variable *num2*. The flowchart for example 2 is shown in Figure 6: