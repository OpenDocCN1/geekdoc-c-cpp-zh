Enter eye distance and nose-chin distance for image 2:
6.0 5.0
Enter eye distance and nose-chin distance for image 3:
6.0 5.6
Best match is between images 1 and 3

The answer matches the hand example, so we can then test the program with additional lengths. Print an image of each of three different friends and see if you can predict which pair would be the best match for this very simple face recognition system. Run the program with information from two different images of the same person and a third person to see if this technique selects the two images that are from the same person.

# MODIFY!

These problems relate to the program developed in this section for finding the best matching pair from three images.

+   1. Modify the program so that it also prints out all three differences. This gives additional information about the quality of the match; if the differences are small, the quality of the match is better.
+   
+   2. What would the output be if two of the ratios were the same minimum value? What would the output be if all three of the ratios were the same value? Generate data to make these cases happen and check your answers.
+   
+   3. Modify the program to use a nested if statement in the solution instead of three independent if statements. Does the answer to Problem 2 change with this solution?
+   
+   4. Modify the program to print the image numbers for the two images that are the most different.
+   
+   5. Modify the program to print the best match between four images. (Note that this causes the program to get longer, because with four images there are six possibilities. In Chapter 5 we will learn additional C language functionality that allows us to handle situations such as this one without ever increasing lines of code.)

# 3.5 Loop Structures

Loops are used to implement repetitive structures. C contains three different loop structures—the while loop, the do/while loop, and the for loop. In addition, C allows us to use two additional statements with loops to modify their performance—the break statement (which we used with the switch statement) and the continue statement.