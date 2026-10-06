
+ 5. Create a project for a sandwich shop. The named SalsSandwiches, allows a user to use a ListBox to choose a sandwich from at least four choices (for example, Roast beef). When the user selects a sandwich type, the program should display a second ListBox that contains at least three types of bread (for example, Whole wheat). After the user selects a bread type, the program should display a third ListBox with least three choices for additions (for example, Lettuce). Display a message on a Label that lists all the chosen options, and make the bread and additions ListBox invisible. If the user makes a new selection from the first ListBox with the main sandwich choices, the bread option becomes available, and if a new bread selection is chosen, the additions option becomes available.

## CHAPTER 13 Handling Events

6. Create a project named GuessNumber with a Form that contains a guessing game with RadioButtons labeled 1 through 5. Randomly choose one of the RadioButtons as the winning button. When the user clicks a RadioButton, display a message indicating whether the user is right.

Add a Label to the Form that provides a hint. When the user's mouse hovers over the label, notify the user of one RadioButton that is incorrect. After the user makes a selection, display all the RadioButtons.

You can create a random number that is at least min less than max using the following statements:

```

Random ran = new Random();
int randomNumber;
randomNumber = ran.Next(min, max);
```

7. Create a project PickLarg with a Form that contains two randomly generated arrays, containing 100 numbers. Include two Buttons labeled 1 and 2. Starting with position 0 in each array, ask the user to guess which of the two arrays contains the higher number and to click one of the buttons to indicate the guess. After each button click, the program displays the values of the two compared numbers, as well as running counts of the number of correct and incorrect guesses. After the user makes a guess, disable the Buttons while the user views the results. After clicking a Next Button, the user can make another guess using the next array values. If the user makes more than 100 guesses, the program should reset the array subscript to 0 so the comparisons start over but continue to keep a running score.

## Debugging Exercises

1. Each of the following files or projects in the Chapter13 folder of your student files has syntax and/or logical errors. Immediately save the two project folders with their new names before starting to correct their errors. After you correct the errors, save each file or project using the filename preceded by Fixed. For example, the file DebugThirteen.cs will become FixedDebugThirteen.cs and the project folder for DebugThirteen will become FixedDebugThirteen.

- a. DebugThirteen1.cs
- b. DebugThirteen2.cs
- c. DebugThirteen3
- d. DebugThirteen4

## Case Problems

+ 1. In Chapter 12, you created an interactive advertisement named GreenvilleAdvertisement that can be used to recruit contestants for the Greenville Idol competition. Now, modify that program to include at least one handled event using the techniques you learned in this chapter.

+ 2. In Chapter 12, you created an interactive advertisement named MarshallsAdvertisement that can be used to advertise the available murals painted by Marshall's Murals. Now, modify that program to include at least one handled event using the techniques you learned in this chapter.

## CHAPTER 14
### Files and Streams

Upon completion of this chapter, you will be able to:

- Describe computer files and the File and Directory classes
- Describe file data organization
- Describe streams
- Write to and read from a sequential access text file
- Search a sequential access text file
- Appreciate serialization and deserialization

In the early chapters of this book, you learned that using variables to store values in computer memory provides programs with flexibility; a program that uses variables to replace constants manipulate different values each time the program executes. However, when data values are stored in memory, they are lost when the program ends. To retain data values for future use, you must store them in files. In this chapter, you will learn to create and manage files in C#.

## Files and the File and Directory Classes

Data items are stored in a computer system either temporarily or permanently.

Temporary storage is usually called computer memory, or random access memory (RAM). When you write a C# program that stores a value in a variable, you are using temporary storage; the value is lost when the program ends or the computer loses power. The type of storage is volatile.

Permanent storage, on the other hand, is not lost when a computer loses power; it is non-volatile. When you write a program and save it to a disk, you are using permanent storage. Likewise, use permanent storage when you write a program that saves data to a file.

> When discussing computer storage, temporary and permanent refer to volatility, not length of time. For example, a temporary variable might exist for several hours in a large program or one that the user forgets to end, but a permanent piece of data in a file might be saved and deleted within a few seconds.

A computer file is a collection of data stored on a nonvolatile device in a computer system. Files exist on permanent storage devices, such as hard disks, USB drives, reels of magnetic tape, and optical discs, include CDs and DVDs.

You can categorize files by the way they store:

- * Text files contain data that can be read in a text editor because the data has been encoded using a scheme such as ASCII or Unicode. Text files might include-
- * Binary files contain data that has not been encoded. Examples include images, videos, and compiled programs.

## Files and the File and Directory Classes

Although their contents vary, text and binary files have many common

- Each has a name. The name often includes a dot and describes the type of file.
- Each has a specific time of creation.
- Each file occupies space on a device. Sizes are measured in bytes. A byte is small for example, in a simple text file, a byte holds only one character. Because a byte is so small, file sizes are usually expressed in kilobytes (thousands of bytes), megabytes (millions of bytes), and gigabytes (billions of bytes).

When you use a device you never directly use the copy that is stored in file. Instead, you use a copy that has been loaded into memory. When you copy data from a storage device into RAM, you read from the file. When you store data in a computer on a storage device, you write to the file.

> Because you can erase data from files, some programmers prefer the term persistent to permanent storage. In other words, you can remove data from a file on a device such as a disk, even if it is not technically permanent. However, the data remains in the file when the computer loses power, so using RAM, the data persists, or perseveres.

The terms directory and folder are used synonymously to mean an entity is used to organize files. Directory is the more general term; the folder can come into use in graphical systems. For example, Microsoft began calling directories with the introduction of Windows 95. The folder was first used in the 1950s with the Electronic Recording Machine, Accounting (ERMA).
