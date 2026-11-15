characters in the English language. This decoding often provides enough of the correct replacements that the incorrect replacements can then be determined. For this problem, write a program that reads a data file and determines the number of occurrences of each of the characters in the file. Then, print the characters and the number of times that they occurred. If a character does not occur, do not print it. *(Hint: Use an array to store the occurrences of the characters based on their ASCII codes.)*

+   **24.** Another simple code encodes a message in text such that the true message is represented by the first letter of each word. There are no spaces between the words, but the decoded string of characters can easily be separated into words by a person. Write a program to read a data file and determine the secret message stored by the sequence of first letters of the words. *(Hint: Store the first letter of each word in a character string.)*

+   **25.** Assume that the true secret message in Problem 24 is stored in the second letter of each word. Write a program to read a data file and determine the secret message stored in the file.

+   **26.** Assume that the true secret message in Problem 24 is represented by the characters that are three characters to the right in the collating sequence from the first letters of the words. Write a program to read a data file and determine the secret message stored in the file using this decoding scheme.

+   **27.** Write a program that encodes the text in a data file using a character array named **key** that contains 26 characters. This key is read from the keyboard; the first letter contains the character that is to replace the letter **a** in the data file, the second letter contains the letter that is to replace the letter **b** in the data file, and so on. Assume that all punctuation is to be replaced by spaces. Check to be sure that the key does not map two different characters to the same one during the encoding.

+   **28.** Write a program which decodes the file that is the output of Program 27. Assume that the same integer key is read from the keyboard by this program and is used in the decoding steps. Note that you will not be able to restore the punctuation characters.

**(A palindrome is a word (noon), sentence (Draw a level award), or number (18781) that reads the same backward or forward. (Note that whitespace is ignored when determining whether a word, sentence, or number is a palindrome.)**

+   **29.** Write a program that reads a line of text from standard input and determines whether the line of text is a palindrome.

+   **30.** Write a program that reads text from a data file. The program should read each line in the data file (read lines until an end of file is encountered), print each line, and also print a message that indicates whether the line is a palindrome.

# **Calculating Probabilities.**

+   **31.** Add a method to the `CardDeck` class named `randomDraw()`. This method should return one card, drawn from a random location in the deck. Use this method to simulate the probability of drawing two face cards from a shuffled deck.

+   **32.** Add a method to the `CardDeck` class named `isEmpty()`. This method should return true if the deck is empty, false otherwise. Write a driver to test the new method.