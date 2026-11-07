**5.50** (*Computer-Assisted Instruction: Reducing Student Fatigue*) One problem in CAI environments is student fatigue. This can be reduced by varying the computer’s responses to hold the student’s attention. Modify the program of Exercise 5.49 so that various comments are displayed for each answer as follows:

Possible responses to a correct answer:

+   - Very good!
+   - Excellent!
+   - Nice work!
+   - Keep up the good work!

Possible responses to an incorrect answer:

+   - No. Please try again.
+   - Wrong. Try once more.
+   - Don’t give up!
+   - No. Keep trying.

Use random-number generation to choose a number from 1 to 4 that will be used to select one of the four appropriate responses to each correct or incorrect answer. Use a switch statement to issue the responses.

**5.51** (*Computer-Assisted Instruction: Monitoring Student Performance*) More sophisticated computer-assisted instruction systems monitor the student’s performance over a period of time. The decision to begin a new topic is often based on the student’s success with previous topics. Modify the program of Exercise 5.50 to count the number of correct and incorrect responses typed by the student. After the student types 10 answers, your program should calculate the percentage that are correct. If the percentage is lower than 75%, display “Please ask your teacher for extra help.”, then reset the program so another student can try it. If the percentage is 75% or higher, display “Congratulations, you are ready to go to the next level!”, then reset the program so another student can try it.

**5.52** (*Computer-Assisted Instruction: Difficulty Levels*) Exercises 5.49–5.51 developed a computer-assisted instruction program to help teach an elementary-school student multiplication. Modify the program to allow the user to enter a difficulty level. At a difficulty level of 1, the program should use only single-digit numbers in the problems; at a difficulty level of 2, numbers as large as two digits, and so on.

**5.53** (*Computer-Assisted Instruction: Varying the Types of Problems*) Modify the program of Exercise 5.52 to allow the user to pick a type of arithmetic problem to study. An option of 1 means addition problems only, 2 means subtraction problems only, 3 means multiplication problems only and 4 means a random mixture of all these types.

# ## Random-Number Simulation Case Study: The Tortoise and the Hare

**5.54** (*The Tortoise and the Hare Race*) In this problem, you’ll recreate one of the truly great moments in history—the classic race of the tortoise and the hare. You’ll use random-number generation to develop a simulation of this memorable event.