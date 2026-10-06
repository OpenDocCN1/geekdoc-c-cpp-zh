# 250 Introduction to Programming and Problem-Solving Using Scala

+   - The split method on String is useful for breaking up lines into its constituent parts. It takes a delimiter as a String and returns an Array[String] of all the parts of the String that are separated by that delimiter.

+   - You can use the Source.URL(url:String) method to get a Source that can read data from a source on the web in the format of a URL.

+   - For applications it is easier to read data from a java.util.Scanner. This does not provide a Scala style collection, but it has methods for checking if types of values are present and reading them in a way that is more independent of line breaks.

+   - You can use the java.io.PrintWriter to write text data to file. This type has print methods like those that you have already familiar with.

# 9.6.2 Self-Directed Study

Enter the following statements in the REPL and see what they do. Some will produce errors. You should try to figure out why. Try some variations to make you understand what is going on.

# 9.6.3 Exercises

+   1. If you did project 6.7, you can modify it so that it does not have to use input redirection. Make a function that reads in the dictionary of words and then write a script that will allow the user to input Scrabble letters until they enter a special value to stop.