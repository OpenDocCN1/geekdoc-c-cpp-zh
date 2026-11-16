# 8.11 Assignments

Assignment 8.1: The histogram of an image is defined and discussed in section 8.2.2. In that section, the histogram plays a significant part in identifying regions to be segmented. But what if the histogram were flat? Take the image assigned by your instructor and compute its histogram. It is easy from this histogram to find the best dark/bright threshold? Discuss that. Find some way to run histogram equalization. That program will produce a histogram very close to flat. Consider the histogram of that image. Discuss.

Assignment 8.2. In Otsu’s method, prove the statement that minimizing the intra-class variance is equivalent to maximizing the inter-class variance.

Assignment 8.3. In Otsu’s method, derive the between-class variance expression in Eq. 8.3 and explain how it can be recursively calculated to speed up the procedure.

Assignment 8.4: Derive Eq. 8.41.

Assignment 8.5: You have a set of pixels that are drawn from an image that you know is black and white, but the paper is old and dirty, and the histogram clearly has two peaks, with lots of noise. You have an idea: consider only points near the two peaks. That would give you two independent histograms, and you could fit each of those with just 3 parameters (or ... you decide). Try this. You do not need to write software, just think about the question. Find the two peaks independently. Do you encounter any problems?

Assignment 8.6: Here are 6 points in a 3-space: [1, 2, 0], [2, 7, 2], [3, 4, 1], [7, 7, 6], [5, 6, 4], [0, 0, 1]. Start the k-means algorithm with 2 clusters located at [5, 6, 0] and [7, 1, 6]. Run two iterations of the algorithm using Euclidean distance. Show the output at each iteration. Repeat with Manhattan distance. What do you conclude? You may do it by hand, write a simple program, or just run some program that you find.

+   Assignment 8.7: Equation 8.4 presents the equation for the sum of two Gaussians. Consider the problem of estimating the six parameters:
+   
+   1. Write the equation for the sum-squared error between the model of Eq. 8.4 and an actual histogram of n points.
+   2. Differentiate that equation with respect to A1 and write the equation that needs to be solved to use the strategy of “take the derivative and set it equal to zero.”
+   3. Differentiate that equation with respect to A2 and write the equation that needs to be solved to use the strategy of “take the derivative and set it equal to zero.”
+   4. Discuss the feasibility of solving all six equations simultaneously and suggest an appropriate approach to this problem.

Assignment 8.8: A very small image is illustrated in Figure 8.26. Suppose the pixels marked in **boldface** font are edge pixels, and the values given for all the pixels may be ignored. Find the distance transform value for all remaining pixels. Use both Euclidean and 4-connected distances.

Assignment 8.9: On color clustering. In your images directory are three images, called faced.ifs, faceblue.ifs, and (can you guess?) facegreen.ifs. These are the red,