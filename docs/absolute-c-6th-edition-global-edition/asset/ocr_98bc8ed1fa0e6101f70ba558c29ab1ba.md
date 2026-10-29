movie ratings are to the ratings input by the user. This technique is a simple version of the nearest neighbor classification algorithm.

For example, if the user inputs a rating of 5 for movie 102, 2 for movie 104, and 5 for movie 105, then the closest match is reviewer 0 with a distance of sqrt((5 − 5)² + (2 − 1)² + (5 − 5)²) = 1. The program would then predict a rating of 3 for movie 100, a rating of 1 for movie 101, and a rating of 2 for movie 103.

# 15. Traditional password entry schemes are susceptible to "shoulder surfing" in which an attacker watches an unsuspecting user enter their password or PIN number and uses it later to gain access to the account. One way to combat this problem is with a randomized challenge-response system. In these systems, the user enters different information every time based on a secret in response to a randomly generated challenge. Consider the following scheme in which the password consists of a five-digit PIN number (00000 to 99999). Each digit is assigned a random number that is 1, 2, or 3. The user enters the random numbers that correspond to their PIN instead of their actual PIN numbers.

For example, consider an actual PIN number of 12345. To authenticate, the user would be presented with a screen such as

```
PIN: 0 1 2 3 4 5 6 7 8 9
NUM: 3 2 3 1 1 3 2 2 1 3
```

The user would enter 23113 instead of 12345. This does not divulge the password even if an attacker intercepts the entry because 23113 could correspond to other PIN numbers, such as 69440 or 70439. The next time the user logs in, a different sequence of random numbers would be generated, such as

```
PIN: 0 1 2 3 4 5 6 7 8 9
NUM: 1 1 2 3 1 2 2 3 3 3
```

Your program should simulate the authentication process. Store an actual PIN number in your program. The program should use an array to assign random numbers to the digits from 0 to 9. Output the random digits to the screen, input the response from the user, and output whether or not the user's response correctly matches the PIN number.

# 16. Do Programming Project 5.14 except instead of only four reviewers, allow for up to 1000 reviewers and store the reviews in a text file. While your program should support up to 1000 reviewers, the actual number of reviewers stored in the file could vary from 1 to 1000. The only movies that are reviewed are numbered from 100 to 105 as in Programming Project 5.14. You are welcome to design the format used to store the reviews in the text file. After the reviews are read from the text file the program should input three movies and make predictions for the remaining two movies as in Programming Project 5.14.

# 17. Programming Project 2.12 asked you to explore Benford's Law. An easier way to write the program is to use an array to store the digit counts. That is, count[0] might store the number of times 0 is the first digit (if that is possible in your data set), count[1] might store the number of times 1 is the first digit, and so forth. Redo Programming Project 2.12 using arrays.