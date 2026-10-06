
# Chapter 10 Files

of the sales.dat file containing the data entered by the user in the sample run. Figure 10-13 shows a flowchart for the program.

## Program 10-3

```
1 // Variable to hold the number of days
2 Declare Integer numDays
3
4 // Counter variable for the loop
5 Declare Integer counter
6
7 // Variable to hold an amount of sales
8 Declare Real sales
9
10 // Declare an output file.
11 Declare OutputFile salesFile
12
13 // Get the number of days.
14 Display "For how many days do you have sales?"
15 Input numDays
16
17 // Open a file named sales.dat.
18 Open salesFile "sales.dat"
19
20 // Get the amount of sales for each day and write
21 // it to the file.
22 For counter = 1 To NumDays
23 // Get the sales for a day #
24 Display "Enter the sales for day #", counter
25 Input sales
26
27 // Write the amount to the file.
28 Write salesFile sales
29
30 End For
31 // Close the file.
32 Close salesFile
33 Display "Data written to sales.dat."
```

## Program Output (with Input Shown in Bold)

For how many days do you have sales?
5 [Enter]
Enter the sales for day #1
1000.00 [Enter]
Enter the sales for day #2
2000.00 [Enter]
Enter the sales for day #3
3000.00 [Enter]
Enter the sales for day #4
4000.00 [Enter]
Enter the sales for day #5
5000.00 [Enter]
Data written to sales.dat.

## Figure 10-12 Contents of the sales.dat

| 1000.00 Delimiter | 2000.00 Delimiter | 3000.00 Delimiter | 4000.00 Delimiter | 5000.00 Delimiter | EOF |

## Figure 10-13 Flowchart for Program 10-3

![](img/c939132f7878c7f339c6977b3fc885_415.png)

## Reading a File with a Loop and Detecting the End of the File

Quite often a program must read the contents of a file without knowing the number of items stored in the file. For example, the sales.dat file created by Program 10-3 can have any number of items stored in it because the program asks the user for the number of days he or she has. If the user enters 5 as the number of days, the program gets 5 sales amounts and stores them in the file. If the user enters 100 as the number of days, the program gets 100 sales amounts and stores them in the file. This presents a problem if you want to write a program that processes all the items in the file, regardless of how many there are. For example, suppose you need to write a program that reads all the amounts in the file and calculates their total. You can use a loop to read the items in the file, but an error will occur if the program tries to read beyond the end of the file. The program needs some way of knowing when the end of the file has been reached.

Most programming languages provide a library function for this purpose. In our pseudocode we will use the `eof` function. Here is the function's general format:

```
eof(fileName)
```

The `eof` function accepts a file's name as an argument, and returns True if the end of the file has been reached or False if the end of the file has not been reached. The pseudocode in Program 10-4 shows an example of how to use the eof function. The program displays all the sales amounts in the sales.dat file.

## Program 10-4

```
// Declare an input file.
Declare File inputFile
// Declare a variable to hold a sales amount
// that is read from the file.
Declare Real sales
// Open the sales.dat file.
Open inputFile "sales.dat"
Display "Here are the sales amounts:"
// Read all of the items in the file
// and display them.
While NOT eof(inputFile)
  Read inputFile
  Display currencyFormat(sales)
End While
// Close the file.
Close inputFile
```

## Program Output

Here are the sales amounts:

```
$1,000.00
$2,000.00
$3,000.00
$4,000.00
$5,000.00
```

## 10.2 Using Loops to Process Files

Take a closer look at line 15:

```
While NOT eof(inputFile)
```

When you read this pseudocode, you naturally think: *While not at the end of the file...* This statement could have been written as:

```
While eof(inputFile) == False
```

Although this is logically equivalent, most programmers will prefer to use the NOT operator as shown in line 15 because it more clearly states the condition that is being tested. Figure 10-14 shows a flowchart for the program.

## Figure 10-14 Flowchart for Program 10-4

![](img/c939132f7878c7f339c6977b3fc885_417.png)

## In the Spotlight: Working with Files

Kevin is a freelance video producer who makes TV commercials for local businesses. When he makes a commercial, he usually films several videos. Later, he puts these shots together to make the final commercial. He has asked you to design the following two programs:

1. A program that allows him to enter the running time (in seconds) of each video in a project. The running times are saved to a file.
2. A program that reads the contents of the file, displays the running times, and then displays the total running time of all the segments.

Here is the general algorithm for the first program:

1. Get the number of videos in the project.
2. Open an output file.
3. For each video in the project:
   Get the video's running time to the file.
   Write the file.
4. Close the file.

Program 10-5 shows the pseudocode for the first program. Program 10-15 shows the flowchart.

## Program 10-5

```
1 // Declare an output file.
2 Declare outputFile videoFile
3
4 // A variable to hold the number of videos.
5 Declare Integer numVideos
6
7 // A variable to hold a video's running time.
8 Declare Real runningTime
9
10 // Counter variable for the loop
11 Declare Integer counter
12
13 // Get the number of videos.
14 Display "Enter the number of videos in the project."
15 Input numVideos
16
17 // Open an output file to save the running times.
18 Open outputFile "time.dat"
19
20 // Write each video's running time to the file.
21 For counter = 1 To numVideos
22 // Get the running time.
23 Display "Enter the time for video #"
24 Input runningTime
25
26 // Write the running time to the file.
27 Write outputFile runningTime
28 End For
29 // Close the file.
30 Close outputFile
31 Display "The times have been saved to time.dat."
```

## Program Output (with Input Shown in Bold)

Enter the number of videos in the project.
6 [Enter]
Enter the time for video #1
24.5 [Enter]
Enter the time for video #2
12.2 [Enter]
Enter the time for video #3
14.6 [Enter]
Enter the time for video #4
20.4 [Enter]
Enter the time for video #5
22.5 [Enter]
Enter the time for video #6
19.3 [Enter]
The times have been saved to time.dat.

## Figure 10-15 Flowchart for Program 10-5

![](img/c939132f7878c7f339c6977b3fc885_419.png)

Here is the general algorithm for the second program:

1. Initialize an accumulator to 0.
2. Open the input file.
3. While not at the end of the file:
   Read a value from the file.
   Add the value to the accumulator.
4. Close the file.
5. Display the contents of the accumulator as the total running time.

## Program 10-6

```
// Declare an input file.
Declare File inputFile

// A variable to hold a time
// that is read from the file.
Declare Real videoRunningTime

// Accumulator to hold the total time,
// initialized to 0.
Declare Real total = 0

// Open the input file.
Open inputFile "time.dat"

// Display "Here are the running times, in seconds, of
// each video in the project:"

// Read all of the times in the file,
// display them, and calculate their total.
While NOT eof(inputFile)
  // Read a time.
  Read inputFile videoRunningTime

// Display the time for this video.
  Display videoRunningTime

// Add videoRunningTime to total.
  Set total = total + videoRunningTime
End While

// Close the file.
Close inputFile

// Display the total running time.
Display "The total running time of the videos is ",
  total, "seconds."
```
