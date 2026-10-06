
# Text Files

4. For this project you will extend what you did as part of project 81 so that the courses you are interested in will be stored in a file for reuse. The script should take a single command-line argument for the name of the storage file. The file stores the course information along with the level of interest. Menu options should be as follows:

- Add course of interest.
- Print current courses.
- Remove course of interest.
- Modify course interest.
- Build a schedule.
- Quit

There is a new option to modify interest because the program is run over a period of time, the user might become more or less interested in the course. Also, for the build option, you should add the option to have the user say they are taking one of the printed schedules and remove all those courses from the list of interests. Save the modified list of courses of interest to the file when the user quits.

5. The National Weather Service computes the whirlwind index using the following formula:

```
33.74 + 0.6215T(V^0.16) - 35.75(V^-0.16) + 0.4275T(V^-0.16)
```

Where T is the temperature in degrees Fahrenheit, and V is the wind speed in miles per hour. This formula only applies for wind speeds over 3 miles per hour. Write a program that calculates the whirlwind for all data in a file. A file that you can use for this project can be found at http://www.underground.com/history/. Search for your location, and go to the bottom of the page for a separated file.

6. Write a hangman game. If you go to http://www.gutenberg.org/files/3201/files/, you will find a number of CROSSWD.TXT files you could play with. The text file you need for this project is CROSSWD.TXT. These files were placed in the public domain by Gray Ward and CROSSWD.TXT a list of words permitted in crossword games. Select a randomly word from this list and then prompt the player to guess what the word is - one letter at a time. At the beginning, display a series of asterisks * to represent each letter. When the player makes a correct guess, display the letter in correct location as well as the remaining asterisks *. After the player has guessed the correct word, display the number of misses and ask the user if they would like to continue to play.

7. Grimm's Fairy Tales are available in text format Project Gutenberg and can be found at http://www.gutenberg.org/files/2591/2591-txt. Download this file for it is one of the files that you will need for this project. You will need to look through Grimm's Fairy Tales for a series of words. These words will be found in a second file created by you. For example, you could create a file that has the words "gold", "kingdom", and "queen" in it. The goal of this project is to create an output file that contains each word, how many times that word was found in Grimm's Fairy Tales and a listing of all the lines that word was found on.

8. For this project, you will need to download a DVD list from the book's site. It is a relatively complete list of all the Region 1 DVD's that some may have in their home theater library. The original list was obtained at http://www.hometheaterinfo.com/dvlist.htm, and we are very grateful for the effort that it takes for the authors to maintain this list. You may find interesting to play with this data set, but for the purposes of this project, we want to simply search for several things: 1) Find the most expensive DVD in the list; 2) Find all the films produced by New Line™ studios; 3) Find how many titles are there from Netflix™ studios; 4) What is the title of the oldest DVD in the list; 5) Print out a list of the different Genre in the list (listing each Genre once).

9. The Beatles are an English rock band from the 60s. They were widely regarded as the greatest and most influential act of the rock era. The group broke up in 1970, but they are still considered one of the most successful groups of all time. A list of all the Beatles record titles through 1974 can be found at http://textfiles.com/music/beatles.u-k. Download this file. Then ask the user for a word and list of all the albums, singles, and extended plays contain that word. Next, print out all the dates that include that word in the title.

10. Sports should be able to go out to the Internet and find many text files that contain statistics information for basketball teams, football teams, water polo teams, etc. For this project you will need to find a text format of box scores for a sport that interests you. One place you can look for text file statistics is at http://www.doustats.com/ which has NBA and MLB statistics. Read in this data. Then provide a menu of relevant statistics to the user. For example, you may calculate average for a player, or averages for a team, and you can allow the user a menu option that allows them the ability to select which average they would like to see.

Additional exercises and projects, along with data files, are available on the book's web site.

# Chapter 10

# Case Classes

| | | |
|---|---|---|
| 10.1 | User Defined Types | 256 |
| 10.2 | case classes | 256 |
| 10.2.1 | Making Objects | 257 |
| 10.2.2 | Accessing Members | 257 |
| 10.2.3 | Named and Default Arguments (Advanced) | 258 |
| 10.2.4 | The Copy Method | 259 |
| 10.2.5 | case Class Patterns | 260 |
| 10.3 | Mutables | 260 |
| 10.4 | Putting It Together | 261 |
| | Tuple Zipped Type (Advanced) | 269 |
| 10.5 | End of Chapter Material | 270 |
| 10.5.1 | Summary of Concepts | 270 |
| 10.5.2 | Self-Directed Study | 271 |
| 10.5.3 | Exercises | 271 |
| 10.5.4 | Projects | 272 |

One of the things that you have noticed by this point is that there are times when it can be helpful to group pieces of data together. If all the data is the same type, you could use something like an Array or a List. The down side of this is that the simpler compiler cannot make to sure that you have the right number of elements. For example, if you have a point in 3-D with $x$, $y$, and $z$ coordinates having more or less could cause the code to break and Scala would not be able to check that until the program was running. The alternative, which also works if the types of values are different is to use a tuple. Some 3-D point could be represented as a (Double, Double, Double). While this works reasonably well for a 3-D point, it too has significant limitations.

To illustrate this, consider different things that could be represented as three Doubles. One is a point in 3-D. Another related one is a vector in 3-D. The vector or the point could be represented in Cartesian coordinates, cylindrical coordinates, or polar coordinates and the tuple would not tell you which is which. The three Doubles also represent the high temperature, low temperature and average temperature for a day; or the regular price, sale price, and cost of a sweater; or three sub-averages for a students grade in a class.
