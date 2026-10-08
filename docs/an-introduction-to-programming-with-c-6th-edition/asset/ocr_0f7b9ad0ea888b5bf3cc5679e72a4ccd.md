# CHAPTER 11

# One-Dimensional Arrays

ADVANCED

30. In this exercise, you create a program that uses two parallel-dimensional arrays. Ms. Jenkins uses the grade table shown in Figure 11-60 for her Introduction to Programming course. She wants a program that displays the grade after she enters the total points earned. If necessary, create a new project named Advanced30Project. Also create a new source file named Advanced30.cpp. Store the minimum points in a one-dimensional int array. Store the grades in a one-dimensional char array. Use a sentinel value to stop the program. Save and then run the program. Test the program using the following amounts: 455, 210, 400, and 349.

| Minimum points | Maximum points | Grade |
| :--- | :--- | :--- |
| 0 | 299 | F |
| 300 | 349 | D |
| 350 | 399 | C |
| 400 | 449 | B |
| 450 | 500 | A |

Figure 11-60

ADVANCED

31. In this exercise, you modify the program from Computer Exercise 30. The modified program allows the user to change the grading scale while the program is running. If necessary, create a new project named Advanced31Project. Also create a new source file named Advanced31.cpp. Copy the instructions from the Advanced31.cpp file. Change the filename in the first comment. Modify the program so that it allows the user to enter the total number of possible points of other words; the total number of points a student can earn—when the program is running. Also modify the program so that it uses the grading scale shown in Figure 11-61. For example, when the user enters the number 500 as the total number of possible points, the program should use 450 (which is 90% of 500) as the minimum points for an A. When the user enters the number 300 as the total number of possible points, the program should use 270 (which is 90% of 300) as the minimum points for an A. Save and then run the program. The program using 300 as the total number of possible points and 185 as the number of points earned. The program should display D as the grade. Stop the program. Then test it using 500 and 363 as the total number of possible points and the total points earned, respectively. The program should display C as the grade.

| Minimum points | Grade |
| :--- | :--- |
| 60% of the possible points | F |
| 70% of the possible points | D |
| 80% of the possible points | C |
| 90% of the possible points | B |

Figure 11-61

482