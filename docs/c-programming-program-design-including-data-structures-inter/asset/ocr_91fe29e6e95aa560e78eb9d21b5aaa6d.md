**14.** Suppose that the first number of a sequence is $x$, in which $x$ is an integer. Define $a_0=x$; $a_{n+1}=a_n/2$ if $a_n$ is even; $a_{n+1}=3\times a_n+1$ if $a_n$ is odd. Then, the exercise is to find a $k$ such that $a_k=1$. Write a program that prompts the user to input the value of $x$. The program output the integer $k$ such that $a_k=1$ and the numbers $a_0$, $a_1$, $a_2$, ..., $a_k$. (For example, if $x=75$, then $k=14$, and the numbers are 75, 226, 113, 340, 170, 85, 256, 128, 64, 32, 16, 8, 4, 2, 1.) Test your program for the following values of $x$: 75, 111, 678, 732, 873, 2048, and 65535.

**15.** Enhance your program from Programming Exercise 14 by outputting the position of the largest number and the largest number of the sequence $a_0$, $a_1$, ..., $a_k$. (For example, the largest number of the sequence 75, 226, 113, 340, 170, 85, 256, 128, 64, 32, 16, 8, 4, 2, 1 is 340, and its position is 4.) Test your program for the following values of $x$: 75, 111, 678, 732, 873, 2048, and 65535.

**16.** The program in Example 5-6 implements the Number Guessing Game. However, in that program, the user is given as many tries as needed to guess the correct number. Rewrite the program so that the user has no more than five tries to guess the correct number. Your program should print an appropriate message, such as “You win!” or “You lose!”.

**17.** Example 5-6 implements the Number Guessing Game program. If the guessed number is not correct, the program outputs a message indicating whether the guess is low or high. Modify the program as follows: Suppose that the variables `num` and `guess` are declared as in Example 5-6 and `diff` is an `int` variable. Let `diff` = the absolute value of (`num − guess`). If `diff` is 0, then the guess is correct and the program outputs a message indicating that the user guessed the correct number. Suppose `diff` is not 0. Then the program outputs the message as follows:

+   a. If `diff` is greater than or equal to 50, the program outputs the message indicating that the guess is very high (if guess is greater than num) or very low (if guess is less than num).
+   
+   b. If `diff` is greater than or equal to 30 and less than 50, the program outputs the message indicating that the guess is high (if guess is greater than num) or low (if guess is less than num).
+   
+   c. If `diff` is greater than or equal to 15 and less than 30, the program outputs the message indicating that the guess is moderately high (if guess is greater than num) or moderately low (if guess is less than num).
+   
+   d. If `diff` is greater than 0 and less than 15, the program outputs the message indicating that the guess is somewhat high (if guess is greater than num) or somewhat low (if guess is less than num).

As in Programming Exercise 16, give the user no more than five tries to guess the number. (To find the absolute value of `num − guess`, use the expression `abs(num − guess)`. The function `abs` is from the header file `cstdlib`.)