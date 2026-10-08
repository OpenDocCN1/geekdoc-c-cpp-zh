# CHAPTER 14 Sequential Access Files

The answers to Mini-Quaz questions are located in Appendix A.

# Mini-Quiz 14-2

+   1. What value does the is_open function return when the open function fails?
2. Which of the following statements writes the contents of the quantity variable to the inventory.txt file, which is associated with a file object named outInv?
a. inventory.txt << quantity << end1;
b. ofstream << quantity << end1;
c. outInv << quantity << end1;
d. outInv >> quantity >> end1;
3. Which of the following statements writes a record to the test.txt file? The file is associated with a file object named outFile. The record contains two stores, which are stored in score1 and score2 variables.
a. test.txt << score1 << score2 << end1;
b. ofstream << score1 << '#' << score2 << end1;
c. outFile << score1 << score2 << end1;
d. outFile << score1 << '#' << score2 << end1;
4. Which of the following statements reads a record statement from Question 2 and stores the record in the number variable? The inventory.txt file is associated with a file object named inInv.
a. ifstream >> number;
b. inventory.txt >> number;
c. inInv << number;
d. inInv >> number;

594

# Testing for the End of a Sequential Access File

As learned earlier, the computer uses a file pointer to keep track of the next character either to read from a file or write to a file. When a sequential access file is opened for input, the computer positions the file pointer before the first character in the file. Each time a character is read from the file, the file pointer is moved to the next character. When an entire line is read from the file, the computer moves the file pointer to the beginning of the next line in the file. Most times, a program will need to read each line contained in a sequential access file, one line at a time, beginning with the first line and ending with the last line. You can accomplish this task