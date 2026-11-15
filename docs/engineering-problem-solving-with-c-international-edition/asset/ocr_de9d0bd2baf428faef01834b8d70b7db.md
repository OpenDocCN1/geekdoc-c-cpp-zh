then generate a list of potential error conditions that could arise. If possible, discuss these with the person or group that will be using the program. Otherwise, include error checks that seem to catch the most common types of errors, and then include written documentation with the program. This documentation should describe the error conditions that your program will catch and the ones that your program will not catch.

Once you have decided which error conditions you will incorporate in your algorithm, you still need to decide what to do if one of the error conditions occurs. There are usually two possibilities—you can exit the program or you can attempt to correct the error and continue with the program. In either case, you should probably print an error message that describes the error condition that occurred and the action that you are taking. Make sure that the error message gives as much information as possible. Instead of printing “Error occurred in input data,” print messages such as “Temperature out of bounds,” “Time value is negative,” or “Pressure exceeds safety limits.”

Data file

In this chapter, we discuss how to read and write data files, which are files (similar to program files) that contain information used in other programs. Sometimes programs called data filters are written that check the information in the data files for error conditions. Then, programs that use the data files do not need to check for the same error conditions.

# Generation of Test Data

Test data

The generation of test data is a very important part of developing problem solutions. Test data should include data to test each of the error conditions that is checked in our programs. Test data should also test each path through our program. As programs become longer, generating test data to completely test the program becomes very difficult. Entire courses and books are based on this validation and verification topic.

Validation and verification

We now give some suggestions on generating test data sets. First, use the data from the hand example. If this does not work properly, we are not off to a good start! Once the program works correctly for these data, begin using test data that cover different ranges of values. Be sure to use test data that test the boundary conditions, or limits, if the data are supposed to be in certain ranges. Once the program seems to work for valid data, then begin including the error conditions to see if the program handles them properly. In general, use many small sets of data instead of one large set of data to test the program.

If you find an error in testing the program, go back to the algorithm development step. Correct the error in the decomposition outline and the pseudocode or flowchart, and then correct the C program. When you make a major change in the program, you should completely retest the program. Sometimes changes affect parts of the program that we had not anticipated. This retesting is easier if we keep a log of the test sets used so that we can repeat them.

![](bbox=[0.13, 0.63, 0.19, 0.69])

Program walkthrough

Finally, we want to mention a technique called a program walkthrough that is commonly used in industry in the development of large programs. In a program walkthrough, the people who have developed an algorithm for a complicated problem present their solution to a small group of people who are knowledgeable about the problem, but did not take part in the algorithm development. The interaction between the people who developed the algorithm and the people who are analyzing it usually results in identifying potential problems with the algorithm and the generation of potential test data for the software after it is coded. The result is that the final program is completed sooner with more confidence in its accuracy. You might try simple program walkthroughs with other students in your class as you solve more complicated problems.