# Recursion Exercises

**7.31**　*(Selection Sort)* A selection sort searches an array looking for the smallest element. Then, the smallest element is swapped with the first element of the array. The process is repeated for the subarray beginning with the second element of the array. Each pass of the array results in one element being placed in its proper location. This sort performs comparably to the insertion sort—for an array of *n* elements, *n* − 1 passes must be made, and for each subarray, *n* − 1 comparisons must be made to find the smallest value. When the subarray being processed contains one element, the array is sorted. Write recursive function selectionSort to perform this algorithm.

**7.32**　*(Palindromes)* A palindrome is a string that is spelled the same way forward and backward. Examples of palindromes include “radar” and “able was I ere I saw elba.” Write a recursive function testPalindrome that returns true if a string is a palindrome, and false otherwise. Note that like an array, the square brackets ([]) operator can be used to iterate through the characters in a string.

**7.33**　*(Linear Search)* Modify the program in Fig. 7.18 to use recursive function linearSearch to perform a linear search of the array. The function should receive an integer array and the size of the array as arguments. If the search key is found, return the array subscript; otherwise, return −1.

**7.34**　*(Eight Queens)* Modify the Eight Queens program you created in Exercise 7.26 to solve the problem recursively.

**7.35**　*(Print an Array)* Write a recursive function printArray that takes an array, a starting subscript and an ending subscript as arguments, returns nothing and prints the array. The function should stop processing and return when the starting subscript equals the ending subscript.

**7.36**　*(Print a String Backward)* Write a recursive function stringReverse that takes a string and a starting subscript as arguments, prints the string backward and returns nothing. The function should stop processing and return when the end of the string is encountered. Note that like an array the square brackets ([]) operator can be used to iterate through the characters in a string.

**7.37**　*(Find the Minimum Value in an Array)* Write a recursive function recursiveMinimum that takes an integer array, a starting subscript and an ending subscript as arguments, and returns the smallest element of the array. The function should stop processing and return when the starting subscript equals the ending subscript.

# Vector Exercises

**7.38**　*(Salesperson Salary Ranges with vector)* Use a vector of integers to solve the problem described in Exercise 7.10.

**7.39**　*(Dice Rolling with vector)* Modify the dice-rolling program you created in Exercise 7.17 to use a vector to store the numbers of times each possible sum of the two dice appears.

**7.40**　*(Find the Minimum Value in a vector)* Modify your solution to Exercise 7.37 to find the minimum value in a vector instead of an array.

# Making a Difference

**7.41**　*(Polling)* The Internet and the web are enabling more people to network, join a cause, voice opinions, and so on. The presidential candidates in 2008 used the Internet intensively to get out their messages and raise money for their campaigns. In this exercise, you’ll write a simple polling program that allows users to rate five social-consciousness issues from 1 (least important) to 10 (most important). Pick five causes that are important to you (e.g., political issues, global environmental issues). Use a one-dimensional array topics (of type string) to store the five causes. To summarize the survey responses, use a 5-row, 10-column two-dimensional array responses (of type int), each row corresponding to an element in the topics array. When the program runs, it should