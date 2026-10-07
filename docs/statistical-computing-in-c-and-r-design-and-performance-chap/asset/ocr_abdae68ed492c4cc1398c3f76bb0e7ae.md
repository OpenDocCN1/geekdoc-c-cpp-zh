# 194 PROGRAMMING IN R

If a minimum of five observations are required per cell/group for carrying out a chi-square test for uniformity, how many observations would be needed to test for uniform selection over every possible function combination that can occur in the Guess5 game?

5.13. Use the invisible function to suppress the NULL output from the guess5 function of 5.6.

5.14. Develop a C++ program that will read in the Guess5 data from Section 5.6 and count the frequency of occurrence of the numbers over the entire collection of draws.

5.15. Numbers are drawn five times with replacement from the integers 0 to 9. Use R to calculate the probability distribution for the sum of the numbers that are drawn.

5.16. Consider a lottery game where k are selected from balls numbered 1 to n1 without replacement and an additional (single) ball is drawn independently from a set of balls numbered 1 to n2. Players win prizes depending on how many of the balls they match the k lottery draws from the 1 to n1 range and the lottery’s bonus ball selection.

+   Use the R function to create an R function that will compute the chance of winning for all possible outcomes for the game.

+   What are the chances for all the outcomes when k = 5, n1 = 40 and n2 = 20?

5.17. Suppose the Guess5 game from Section 5.6 adds a bonus ball where every draw an independent draw is made of a single ball from a set of balls numbered 1 to 20. There are five ball sets and two machines that are used for the bonus drawings.

+   Create a similar program to the one in Listing 5.5 that will generate a set of artificial data for this game.

+   Use your program from part a) to create a data file containing the results of 100 simulated draws of the new Guess5 game.

+   Import the data from the file you created in R a format that will allow you to analyze the data using a chi-square test. Note that there are two separate tests that must be performed corresponding to the 5 of 40 drawings and those involving the bonus ball.

+   Compute appropriate chi-square statistics to determine if the data you generated shows departure from uniform selection in your generation methodology.

5.18. Compare the run-times for the three ways of reading in the Guess5.txt file in Section 5.6 using replicate runs of each program to the approach used to compare the meanComp, meanCompD and vecPoolLed functions in Section 5.5.

5.19. A person buys four-generated tickets for playing the Guess5 game. That is, the player chooses four sets of numbers selected from the integers 1 to 40 without replacement that have been produced by an assumed fair random generator of some algorithm. Use R to calculate the probability distribution for the number of unique numbers on the four tickets.

5.20. Refer to Exercise 3.10. Write an R program that will perform the same calculations as the C++ program you created for part a) of that exercise. Compare its computation speed to that of the C++ implementation.

5.21. Modify the class X from Section 5.7 to where the constructor and destructor will out "Hello World!" and "Goodbye World!" a total of n1 and n2, respectively, for user-supplied values of n1 and n2. Import the resulting program into R as a shared library and verify that it behaves as expected.

5.22. Import the C++ code using the Cauchy density to generate pseudo-random normals (Listings 4.8–9) in Section 4.6 and package it in an R function that will gen