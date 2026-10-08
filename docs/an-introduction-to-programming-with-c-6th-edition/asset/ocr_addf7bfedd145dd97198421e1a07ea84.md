# CHAPTER 10

# Void Functions

The answers to Mini-Quiz questions are located in Appendix A.

# Mini-Quiz 10-2

+   1. Which of the following is a valid function header for a function named getInput? The function is passed the addresses of two double variables.
   a. void getInput(double &hours, double &rate)
   b. void getInput(&double hours, &double rate)
   c. void getInput(double hours, %rate)
   d. void getInput(double %hours, double %rate)
2. Which of the following statements can be used to call the getInput function from Question 1, passing the addresses of two double variables named hoursWkd and payRate?
   a. getInput(&hoursWkd, &payRate);
   b. getInput(hoursWkd, payRate);
   c. getInput(payRate, & hoursWkd &);
   d. getInput(double &hoursWkd, double &payRate);
3. Write the function prototype for the getInput function from Question 1.
4. When a variable is passed by reference, the computer assigns the name of its corresponding formal parameter to the same location in memory.
   a. True
   b. False

# The Salary Program

In the age message program (earlier in Figure 10-10), each function call passed one variable to its respective function. the getAge(age); statement passed the age by reference to the getAge function, while the displayAge(age); statement passed the age by value to the displayAge function. The program you will view in this section contains a function that calls more than one variable. Specifically, it passes four variables: by value and two by reference. Figure 10-18 shows the problem specification for the salary program's main. It also includes the IPO chart and C++ instructions. The program allows the user to enter an employee's salary and raise rate. It calculates and displays the employee's raise and new salary. Notice that the main function calls the getNewInfo function to calculate the raise and new salary. The main function passes four items of information to