Write a program that reads the posted voting list from a file and outputs the percent of votes cast for each ballot item. You may assume that the file does not have any header lines. The first line will contain a voter ID and a string representing votes. Define a class named Voter that stores an individual's voting record. The class should have a constructor that takes as input a string of votes (for example, "CDGH"), a voter ID, and accessor function(s) that return the person's ID and vote for a specific question. Store each Voter instance in an array or vector. Your program should iterate over the array to compute and output the percent of votes cast for each candidate, proposition, and measure. It should then prompt the user to enter a voter ID, iterate over the list again to find the object with that ID, and print his or her votes.

13. Create a class called Document which stores a vector of String objects. Define a default constructor which creates an empty vector. Define a copy constructor which copies a Document object including all the strings contained inside it. Create a method called addString which accepts and adds a string to the end of the document. Overload the << operator so that the document can be output with a space between each string object. Define a method called getLength which returns the total length of the document. (Hint: use the method string.length() to get the length of each individual string.) Write a driver program to test your class.

14. Do Programming Project 16 from Chapter 8 except use a Racer class to store information about each race participant. The class should store the racer's name, bib number, finishing position, and all of his or her split times as recorded by the RFID sensors. You can choose appropriate structures to store this information. Include appropriate functions to access or change the racer's information, along with a constructor. Make an array or vector of Racer objects to store the entire race results.

The racer's name should come from a separate text file. The information for this file is collected before the race when the participant registers for the event. Listed below is a sample file:

```
100,Bill Rodgers
132,Frank Shorter
182,Joan Benoit
```

15. Define a class called Box which contains fields for this shape's length, width and height. Include a function to calculate the volume of the box. Overload the ==, <, <=, >, >= operators to compare the volume of different box objects. Write a driver program to test your class.