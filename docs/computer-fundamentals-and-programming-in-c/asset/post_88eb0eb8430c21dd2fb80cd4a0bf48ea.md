
- 5. INPUT D
- 6. Q ← N/D (integer division)
- 7. R ← N - Q * D
- 8. PRINT R
- 9. STOP

Only integer value is obtained and remainder ignored

**Explanation** The first step indicates the starting point of the algorithm. The next step asks the programmer to enter the dividend value. The third step keeps the dividend value in the variable N. Step 4 asks for the divisor value to be entered. This is kept in the variable D. In step 6, the value in N is divided by that in D. Since both the numbers are integers, the result is an integer. This value is assigned to Q. Any remainder in this step is ignored. In step 7, the remainder is computed by subtracting the product of the integer quotient and the integer divisor from integer dividend N. The computed value of the remainder is an integer here and obviously less than the divisor. The remainder value is assigned to the variable R. This value is printed on an output device in step 8. Step 9 terminates the algorithm.

### 3. Construct the algorithm for interchanging the numeric values of two variables.

**Solution** Let the two variables be A and B. Consider C to be a third variable that is used to store the value of one of the variables during the process of interchanging the values.

The algorithm for the given problem is as follows.

- 1. START
- 2. PRINT “ENTER THE VALUE OF A & B”
- 3. INPUT A, B
- 4. C ← A
- 5. A ← B
- 6. B ← C
- 7. PRINT A, B
- 8. END

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_137_0.png)

**Explanation** Like the previous examples, the first step indicates the starting point of the algorithm. The second step is an output message asking for the two values to be entered. Step 3 puts these values into the variables A and B. Now, the value in variable A is copied to variable C in step 4. In fact the value in A is saved in C. In step 5 the value in variable B is assigned to variable A. This means a copy of the value in B is put in A. Next, in step 6 the value in C, saved in it in the earlier step 4 is copied into B. In step 7 the values in A and B are printed on an output device. Step 8 terminates the procedure.

### 4. Write an algorithm that compares two numbers and prints either the message identifying the greater number or the message stating that both numbers are equal.

**Solution** This example demonstrates how the process of selection or decision making is implemented in an algorithm using the step-form. Here, two variables, A and B, are assumed to represent the two numbers that are being compared. The algorithm for this problem is given as follows.

- 1. START
- 2. PRINT “ENTER TWO NUMBERS”
- 3. INPUT A, B
- 4. IF A > B THEN
      PRINT “A IS GREATER THAN B”
- 5. IF B > A THEN
      PRINT “B IS GREATER THAN A”
- 6. IF A = B THEN
      PRINT “BOTH ARE EQUAL”
- 7. STOP

**Explanation** The first step indicates the starting point of the algorithm. The next step prints a message asking for the entry of the two numbers. In step 3 the numbers entered are kept in the variables A and B. In steps 4, 5 and 6, the values in A, B and C are compared with the IF ... THEN construct. The relevant message is printed whenever the proposition between IF and THEN is found to agree otherwise the next step is acted upon. But in any case one of the message would be printed because at least one of the propositions would be true. Step 7 terminates the procedure.

### 5. Write an algorithm to check whether a number given by the user is odd or even.

**Solution** Let the number to be checked be represented by N. The number N is divided by 2 to give an integer quotient, denoted by Q. If the remainder, designated as R, is zero, N is even; otherwise N is odd. This logic has been applied in the following algorithm.

- 1. START
- 2. PRINT “ENTER THE NUMBER”
- 3. INPUT N
- 4. Q ← N/2 (Integer division)
- 5. R ← N - Q * 2
- 6. IF R = 0 THEN
      PRINT “N IS EVEN”
- 7. IF R != 0 THEN
      PRINT “N IS ODD”
- 8. STOP

**Explanation** The primary aim here is to find out whether the remainder after the division of the number with 2 is zero or not. If the number is even the remainder after the division will be zero. If it is odd, the remainder after the division will not be zero. So by testing the remainder it is possible to determine whether the number is even or odd.

The first step indicates the starting point of the algorithm while the next prints a message asking for the entry of the number. In step 3, the number is kept in the variable N. N is divided by 2 in step 4. This operation being an integer division, the result is an integer. This result is assigned to Q. Any remainder that occurs is ignored. Now in step 5, the result Q is multiplied by 2 which obviously produces an integer that is either less than the value in N or equal to it. Hence in step 5 the difference between N and Q * 2 gives the remainder. This remainder value is then checked in step 6 and step 7 to print out that it is either even or odd respectively. Step 8 just terminates the procedure.

### 6. Print the largest number among three numbers.

**Solution** Let the three numbers be represented by A, B, and C. There can be three ways of solving the problem. The three algorithms, with some differences, are given below.

- 1. START
- 2. PRINT “ENTER THREE NUMBERS”
- 3. INPUT A, B, C
- 4. IF A >= B AND B >= C
      THEN PRINT A
- 5. IF B >= C AND C >= A
      THEN PRINT B
      ELSE
           PRINT C
- 6. STOP

**Explanation** To find the largest among the three numbers A, B and C, A is compared with B to determine whether A is larger than or equal to B. At the same time it is also determined whether B is larger than or equal to C. If both these propositions are true then the number A is the largest otherwise A is not the largest. Step 4 applies this logic and prints A.

If A is not the largest number as found by the logic in step 4, then the logic stated in step 5 is applied. Here again, two propositions are compared. In one, B is compared with C and in the other C is compared with A. If both these propositions are true then B is printed as the largest otherwise C is printed as the largest.

Steps 1, 2, 3 and 6 needs no mention as it has been used in earlier examples.

Or

This algorithm uses a variable MAX to store the largest number.

- 1. START
- 2. PRINT “ENTER THREE NUMBERS”
- 3. INPUT A, B, C
- 4. MAX ← A
- 5. IF B > MAX THEN MAX ← B
- 6. IF C > MAX THEN MAX ← C
- 7. PRINT MAX
- 8. STOP

**Explanation** This algorithm differs from the previous one. After the numbers are stored in the variables A, B and C, the value of any one of these is assigned to a variable MAX. This is done in step 4. In step 5, the value assigned to MAX is compared with that assigned to B and if the value in B is larger only then it's value is assigned to MAX otherwise it remains unchanged. In step 6, the proposition “IF C > MAX” is true then the value in C is assigned to MAX. On the other hand, if the proposition is false then the value in MAX remains unchanged. So at the end of step 6, the value in MAX is the largest among the three numbers. Step 1 is the beginning step while step 8 is the terminating one for this algorithm.

Or

Here, the algorithm uses a nested if construct.

- 1. START
- 2. PRINT “ENTER THREE NUMBERS”
- 3. INPUT A, B, C
- 4. IF A > B THEN
      IF A > C THEN
          PRINT A
      ELSE
          PRINT C
      ELSE IF B > C THEN
          PRINT B
      ELSE
          PRINT C
- 5. STOP

**Explanation** Here, the nested if construct is used. The construct “IF p1 THEN action1 ELSE action2” decides if the proposition “p1” is true then action1 is implemented otherwise if it is false action2 is implemented. Now, action1 and action2 may be either plain statements like PRINT X or INPUT X or another “IF p2 THEN action3 ELSE action4” construct. Here, p2 is a proposition. This means that a second “if p1 THEN action1 ELSE action2” construct can be interposed within the first “if p1 THEN action1 ELSE action2” construct. Such an implementation is known as “nested if construct”.

Step 4 implements the nested if construct. First the proposition “A > B” is checked to find whether it is true or false. If true, the proposition “A > C” is verified and if this is found to be true, the value in A is printed otherwise C is printed. But if the first proposition “A > B” is found to be false then the next proposition that is checked is “B > C”. At this point if this proposition is true then the value in B is printed whereas if it is false C is printed.

### 7. Take three sides of a triangle as input and check whether the triangle can be drawn or not. If possible, classify the triangle as equilateral, isosceles, or scalene.

**Solution** Let the length of three sides of the triangle be represented by A, B, and C. Two alternative algorithms for solving the problem are given, with explanations after each step, as follows:

- 1. START  
  Step 1 starts the procedure.
- 2. PRINT “ENTER LENGTH OF THREE SIDES OF A TRIANGLE”  
  Step 2 outputs a message asking for the entry of the lengths for each side of the triangle.
- 3. INPUT A, B, C  
  Step 3 reads the values for the lengths that has been entered and assigns them to A, B and C.
- 4. IF A + B > C AND B + C > A AND A + C > B THEN  
      PRINT “TRIANGLE CAN BE DRAWN”  
  ELSE  
      PRINT “TRIANGLE CANNOT BE DRAWN”; GOTO 6

It is well known that in a triangle, the summation of lengths of any two sides is always greater than the length of the third side. This is checked in step 4. So for a triangle all the propositions “A + B > C”, “B + C > A” and “A + C > B” must be true. In such a case, with the lengths of the three sides, that has been entered, a triangle can be formed. Thus, the message “TRIANGLE CAN BE DRAWN” is printed and the next step 5 is executed. But if any one of the above three propositions is not true then the message “TRIANGLE CANNOT BE DRAWN” is printed and so no classification is required. Thus in such a case the algorithm is terminated in step 6.

- 5. IF A = B AND B = C THEN
       PRINT “EQUILATERAL”
   ELSE
       IF A != B AND B != C AND C != A THEN
           PRINT “SCALENE”
       ELSE
           PRINT “ISOSCELES”

After it has been found in step 4 that a triangle can be drawn, this step is executed. To find whether the triangle is an “EQUILATERAL” triangle the propositions “A = B” and “B = C” are checked.
