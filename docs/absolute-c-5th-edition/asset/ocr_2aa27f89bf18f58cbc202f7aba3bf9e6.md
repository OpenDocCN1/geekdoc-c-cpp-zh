# Programming Projects 233

the degree of difficulty for that dive. The degree of difficulty ranges from 1.2 to 3.8 points. The total is multiplied by 0.6 to determine the diver’s score.
Write a computer program that inputs a degree of difficulty and seven judges' scores, and outputs the overall score for that dive. The program should ensure that all inputs are within the allowable data ranges.

+   7. Generate a text-based histogram for a quiz to a class of students. The quiz is graded on a scale from 0 to 5. Write a program that allows the user to enter grades for each student. As the grades are being entered, the program should count using an array, the number of 0s, the number of 1s, the number of 2s, the number of 3s, the number of 4s, and the number of 5s. The program should be capable of handling an array of student grades.

You can do this by making an array of size 6, where each element in the array is initialized to zero. Whenever a zero is entered, increment the value in the array at index 0, and so on, up to index 5.

Output the histogram count at the end. For example, if the input grades are 3, 0, 1, 3, 3, 5, 5, 4, 5, then the program should output

+   grade(s) of 0
grade(s) of 1
grade(s) of 2
grade(s) of 3
rade(s) of 4
rade(s) of 5

+   8. The birthday paradox is that there are two people in the same room happen to share the same birthday. By birthday, we mean the same day of the year (ignoring leap years), but not the exact birthday including the birth year or time of day. Write a program that approximates the probability that two people in the same room have the same birthday, for 2 to 50 people in the room.

The program should use simulation to approximate the answer. Over many trials (say, 5000), randomly assign birthdays to everyone in the room. Count the number of times at least two people have the same birthday, and divide by the number of trials to get an estimated probability that two people share the same birthday for a room size.

Your output should look something like the following. It will not be exactly the same due to the random numbers:

+   For 2 people, the probability of two birthdays is about 0.0002
For 3 people, the probability of two birthdays is about 0.0082
For 4 people, the probability of two birthdays is about 0.0163
...
For 49 people, the probability of two birthdays is about 0.9654
For 50 people, the probability of two birthdays is about 0.969

![](bbox=[0.06, 0.198, 0.105, 0.233])