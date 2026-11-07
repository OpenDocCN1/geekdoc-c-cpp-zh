**13.25** *(Word Frequency Counting)* Write a program that uses a map to count the number of occurrences of each word in a sentence entered by the user. Treat uppercase and lowercase letters the same and assume there is no punctuation in the sentence. The map’s keys should be the unique words (strings), and its values will be integer counts of how many times each word appears in the sentence. You can break the sentence into its individual words (or tokens) using `std::string`’s `find` and `substr` functions that we introduced in Chapter 8. Given the following input

```
this is sample text with several words this is more sample text with
some different words
```

you program should produce the following output:

```
WORD          COUNT
different     1
is            2
more          1
sample        2
several       1
some          1
text          2
this          2
with          2
words         2
Number of unique words: 10
```

**13.26** *(Character Counts)* Use techniques similar to Exercise 13.25 to write a program that inputs a sentence from the user, then uses a map to summarize the number of occurrences of each letter. Ignore case, ignore blanks and assume the user does not enter any punctuation. Display a two-column table of the letters and their counts with the letters in sorted order.

**13.27** *(Duplicate Word Removal)* Write a function that receives a list of words, then determines and displays in alphabetical order only the unique words. Treat uppercase and lowercase letters the same. The function should use a `set` to get the unique words in the list. Test your function with several sentences.

**13.28** *(Analyzing the Game of Craps)* Modify the program of Fig. 5.5 to play 1,000,000 games of craps. Use a `wins` map to keep track of the number of games won for a particular number of rolls. Similarly, use a `losses` map to keep track of the number of games lost for a particular number of rolls. As the simulation proceeds, keep updating the maps.

A typical key–value pair in the wins dictionary might be 4 and 50217, indicating that 50217 games were won on the 4th roll. Display a summary of the results including:

+   a) the percentage of the total games played that were won.
+   b) the percentage of the total games played that were lost.
+   c) the percentages of the total games played that were won or lost on a given roll (column 2 of the sample output).
+   d) the cumulative percentage of the total games played that were won or lost up to and including a given number of rolls (column 3 of the sample output).

Your output should be similar to the following: