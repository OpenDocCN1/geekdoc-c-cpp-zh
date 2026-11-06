+   - a) Write a program that encrypts a message using rot13.
+   - b) Write a program that decrypts the scrambled message using 13 as the key.
+   - c) After writing the programs of part (a) and part (b), briefly answer the following question: If you did not know the key for part (b), how difficult do you think it would be to break the code? What if you had access to substantial computing power (e.g., supercomputers)? In Exercise 18.25 we ask you to write a program to accomplish this.

**18.8** (*Using string Iterators*) Write a program using iterators that demonstrates the use of functions rbegin and rend.

**18.9** (*Words Ending in "r" or "ay"*) Write a program that reads in several strings and prints only those ending in "r" or "ay". Only lowercase letters should be considered.

**18.10** (*string Concatenation*) Write a program that separately inputs a first name and a last name and concatenates the two into a new string. Show two techniques for accomplishing this task.

**18.11** (*Hangman Game*) Write a program that plays the game of Hangman. The program should pick a word (which is either coded directly into the program or read from a text file) and display the following:

```
    Guess the word:    XXXXXX
```

Each X represents a letter. The user tries to guess the letters in the word. The appropriate response yes or no should be displayed after each guess. After each incorrect guess, display the diagram with another body part filled. After seven incorrect guesses, the user should be hanged. The display should look as follows:

```
    0
   /|\
   / \
```

After each guess, display all user guesses. If the user guesses the word correctly, the program should display

```
    Congratulations!!! You guessed my word. Play again? yes/no
```

**18.12** (*Printing a string Backward*) Write a program that inputs a string and prints the string backward. Convert all uppercase characters to lowercase and all lowercase characters to uppercase.

**18.13** (*Alphabetizing Animal Names*) Write a program that uses the comparison capabilities introduced in this chapter to alphabetize a series of animal names. Only uppercase letters should be used for the comparisons.

**18.14** (*Cryptograms*) Write a program that creates a cryptogram out of a string. A cryptogram is a message or word in which each letter is replaced with another letter. For example the string

```
    The bird was named squawk
```

might be scrambled to form

```
    cin vrjs otz ethns zxqtop
```

Spaces are not scrambled. In this particular case, 'T' was replaced with 'x', each 'a' was replaced with 'h', etc. Uppercase letters become lowercase letters in the cryptogram. Use techniques similar to those in Exercise 18.7.

**18.15** (*Solving Cryptograms*) Modify Exercise 18.14 to allow the user to solve the cryptogram. The user should input two characters at a time: The first character specifies a letter in the cryptogram, and the second letter specifies the replacement letter. If the replacement letter is correct, replace the letter in the cryptogram with the replacement letter in uppercase.