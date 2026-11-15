
After a successful build, we select Run from the Xcode Product menu. When our program prompts us for the name of the input file, we must provide the full path as well as the file name. Notice in above project window that on the left side of the window, the data file WeatherData has been selected. The data is displayed in the center window and on the right side of the window there is information about the project, including the full path of the selected file. This window is very useful when working with input files. If this window is not visible, select Show File Inspector from the Xcode View->Utilities menu. From the File Inspector window, copy the full path name and paste it into the console window when the program prompts for the name of the input file. A successful run of the program is shown in the console window below.

![](img/0235a4ea835dc4575bd036e024a533b3_264_0.png)

Console Window

## Modify 5.7

- 1. Modify program chapter5_9 to write the output to a file named daysAbove50.
- 2. Modify program chapter5_9 to allow the user at least four attempts at the beginning of the program to enter a valid file name before exiting the program.
- 3. Modify program chapter5_9 to determine the number of days that had measurable precipitation. (Do not include days with only trace amounts.)

## SUMMARY

In this chapter, we covered the statements necessary to read information from a data file so that we could use the information in a program. We also presented the statements to generate a data file from a program. Data files are commonly used in solving engineering problems; therefore, this concept was presented early in the text so that we could use it in many of the later problem solutions. We introduced a technique for handling errors that may occur when inputting data. Finally, we covered the concept of generating a linear model for a set of data points and included the equations for determining the best fit in terms of least squares.

## Key Terms

- data file
- data filters
- end-of-file indicator
- error condition
- input file stream
- least squares
- linear modeling
- linear regression
- output file stream
- sentinel signal
- standard input buffer
- stream class inheritances
- stream flags
- stream state
- summation notation
- trailer signal

## C++ Statement Summary

Declaration for file stream objects:

```
ifstream sensor1;
ofstream balloon;
```

File open function:

```
//filename is a string object
sensor1.open(filename);
balloon.open(filename);
```

File fail function:

```
if(sensor1.fail())
```

File input:

```
sensor1 >> t >> motion;
```

File output:

```
balloon << setw(8) << time << setw(8) << height << setw(8) << velocity;
```

Output to standard error:

```
cerr << "Error encountered on input";
```

File close function:

```
sensor1.close();
```

Stream clear function

```
sensor1.clear()
```

## Notes

- 1. Prompt the user to enter filenames so that they can be determined at run time.

![](img/0235a4ea835dc4575bd036e024a533b3_266_0.png)

## Notes

![](img/0235a4ea835dc4575bd036e024a533b3_266_1.png)

- 1. When debugging a program that reads data from a data file, print the values as soon as they are read to check for errors in reading the information.
- 2. When debugging a program that reads a data file, be sure that your program checks for successful opening of the file.
- 3. To avoid infinite loops when inputting data, check the error status of the istream object before each iteration of the loop.
- 4. To avoid problems with operating systems that are case sensitive, use filenames with lowercase letters.

## Problems

## Exam Practice!

### True/False Problems

Indicate whether the following statements are true (T) or false (F).

- 1. cin, cout and cerr are C++ keywords. T F
- 2. When a program attempts to open a data file for input, and the file is not found, the program will terminate. T F
- 3. The statement block of a while loop will be executed at least once. T F
- 4. The statement block of a for loop will be executed at least once. T F
- 5. If a comma is encountered when attempting to read an integer value from standard input, the program will terminate. T F

### Multiple-Choice Problems

- 6. When an end of file is encountered, which of the following stream state flags are set to true?
  - (a) badbit
  - (b) failbit
  - (c) eofbit
  - (d) goodbit

- 7. When an input stream is in an error state, the program will
  - (a) terminate.
  - (b) continue normal execution.
  - (c) continue to execute but input operations applied to the stream will result in a null operation.
  - (d) send a warning message to cerr and continue normal execution.

### Memory Snapshot Problems

Assume the following line of data is entered at the keyboard:

```
1 5 2 a,b
```

Give the corresponding memory snapshot, and the value of the stream state flags, after each of the following sets of statements is executed:

- 8. int i(0), j(0);
     double x, y;
     char ch1, ch2;
     cin >> x >> y >> ch1 >> ch2;

- 9. int i(0), j(0);
     double x, y;
     char ch1, ch2;
     cin >> x >> i >> j >> ch1 >> ch2;

- 10. int i(0), j(0);
      double x, y;
      char ch1, ch2;
      cin >> i >> j >> ch1 >> ch2;

- 11. int i(0), j(0);
      double x, y;
      char ch1, ch2;
      cin >> i >> j >> x >> ch1 >> ch2;

## Data Filters.

Programs called data filters are often used to read the information in a data file and then analyze the contents. In many cases, this data filter program is designed to remove any data errors that would cause problems with other programs that read the information from the data file. The next set of programs is designed to perform error checking and data analysis on information in a data file. Generate data files to test all features of the programs.

- 12. Write a program that reads a data file that should contain only integer values and thus should contain only digits, plus or minus signs, and whitespace. The program should print any invalid characters located in the file, and at the end it should print a count of the invalid characters located.

- 13. Write a program that analyzes a data file that has been determined to contain only integer values and whitespace. The program should print the number of lines in the file and the number of integer values (not integer digits).

- 14. Write a program that reads a file that contains only integers, but some of the integers have embedded commas, as in 145,020. The program should copy the information to a new file, removing any commas from the information. Do not change the number of values per line in the file.

- 15. Write a program that reads a file containing integer and floating-point values separated by commas, which may or may not be followed by additional whitespace. Generate a new file that contains the integers and floating-point values separated only by spaces; remove all whitespace characters between the values, and insert a single space between the values. Do not change the number of values per line in the file.

- 16. Write a program that reads a file containing data values computed by an accounting software package. While the file contains only numerical information, the values may contain embedded commas and dollar signs, as in $3,200, and negative values are enclosed in parentheses, as in (200.56). Write a program to generate a new file that contains the values with the commas and dollar signs removed, and with a leading minus sign instead of the parentheses. Do not change the number of values per line in the file.

- 17. A very useful program is one that compares two files, character by character, to determine whether they are exactly the same. Write a program to compare two files. The program should print a message indicating that the files are exactly the same or that there are differences. If the files are different, the program should print the line numbers for lines that are not the same.

- 18. Developing secret codes has interested people for centuries. A simple coding scheme can be developed by replacing each character in a text file by another character that is a fixed number of positions away in the collating sequence. For example, if each character is replaced by the character that is two characters to its right in the alphabet, then the letter a is replaced by the letter c, the letter b is replaced by the letter d, and so on. Write a program that reads the text in a file and then generates a new file that contains the coded text using this scheme. Change only the alphanumeric characters.

- 19. Write a program to decode the scheme presented in Problem 18. Test the Program by using files generated by Problem 18.

## Sounding Rocket Trajectory.

Sounding rockets are used to probe different levels of the atmosphere to collect information such as that used to monitor the levels of ozone in the atmosphere. In addition to carrying the scientific package for collecting data in the upper atmosphere, the rocket carries a telemetry system in its nose to transmit data to a receiver at the launch site. Besides the scientific data, performance measurements on the rocket itself are transmitted to be monitored by range safety personnel and to be later analyzed by engineers. These performance data include altitude, velocity, and acceleration data. Assume that this information is stored in a file and that each line contains four values: time, altitude, velocity, and acceleration. Assume that the units are s, m, m/s, and m/s^2, respectively.

- 20. Assume that the file rocket1.txt contains an initial line that specifies the number of actual data lines that follows. Write a program that reads these data and determines the time at which the rocket begins falling back to Earth. (Hint: Determine the time at which the altitude begins to decrease.)

- 21. The number of stages in the rocket can be determined by the number of times that the velocity increases to some peak and then begins decreasing. Write a program that reads this data and determines the number of stages on the rocket. Use the data file rocket2.txt. It contains a trailer line with the value -99 for all four values.

- 22. Modify the program in Problem 10 so that it prints the times that correspond to the firing of each stage. Assume that the firing corresponds to the point at which the velocity begins to increase.

- 23. After each stage of the rocket is fired, the acceleration will initially increase and then decrease to -9.8 m/s^2, which is the downward acceleration due to gravity. Find the periods of the rocket flight during which the acceleration is due only to gravity. Allow the acceleration to range within 65% of theoretical value for these periods. Use the data file rocket3.txt, which does not contain a header line or a trailer line.

## Suture Packaging.

Sutures are strands or fibers used to sew living tissue together after an injury or an operation. Packages of sutures must be sealed carefully before they are shipped to hospitals so that contaminants cannot enter the packages. The object that seals the package
