
# 494 Chapter 12 Text Processing

## True or False

- 1. When subscripts are used to specify character positions in a string, the first character's subscript is 0.
- 2. When subscripts are used to specify character positions in a string, the last character's subscript is the same as the string's length.
- 3. If the String variable str contains the string "Might", then the statement str[5] = "y" will change its contents to "Mighty".
- 4. The insert library module automatically expands the size of the string to accommodate inserted characters.
- 5. The delete library module does not actually remove characters from a string, but replaces them with spaces.
- 6. The isUpper function converts a character to uppercase, and the isLower library function converts a character to lowercase.
- 7. An error will occur if you use a subscript on an empty String variable.

## Short Answer

- 1. When using subscript notation to specify a character position in a string, what are the subscripts of the first and last characters?
- 2. If the following pseudocode were an actual program, what would it display?
  Declare String greeting = "Happy"
  insert(greeting, 0, "Birthday")
  Display greeting
- 3. If the following pseudocode were an actual program, what would it display?
  Declare String str = "Yada yada yada"
  delete(str, 4, 9)
  Display str
- 4. If the following pseudocode were an actual program, what would it display?
  Declare String str = "AaBbCcDd"
  Declare Integer index
  For Index = 0 To length(str) - 1
    If isLower(str[index]) Then
      Set str[index] = "-"
    End If
  Display str
- 5. If the following pseudocode were an actual program, what would it display?
  Declare String str = "AaBbCcDd"
  delete(str, 0, 0)
  delete(str, 3, 3)
  delete(str, 3, 3)
  Display str

## Algorithm Workbench

- 1. Design an algorithm that counts the number of digits that appear in the String variable str.
- 2. Design an algorithm that counts the number of lowercase characters that appear in the String variable str.
- 3. Design an algorithm that counts the number of uppercase characters that appear in the String variable str.
- 4. Design an algorithm that deletes the first and last characters in the String variable str.
- 5. Design an algorithm that converts each occurrence of the character "t" in the String variable str to uppercase.
- 6. Design an algorithm that replaces each occurrence of the character "x" in the String variable str with a space.
- 7. Assume the following declaration exists in a program:
  Declare String str = "Mr. Bean"
  Design an algorithm that replaces "Mr." with "Mister" in the variable.

## Debugging Exercises

- 1. What is wrong with the following pseudocode?
  // This Program assigns a character to the first element
  // a string.
  Declare String letters
  Set letters[0] = "A"
  Display "The first letter of the alphabet is ", letters
- 2. What is wrong with the following pseudocode?
  // This Program determines whether the user's input is a single
  // digit.
  Declare Integer digit

  ```
  // Get the input from the user.
  Display "Enter a single digit."
  digit

  // Determine if the input is a single digit.
  If isDigit(digit[0]) AND length(digit) == 1 Then
    Display digit, " " is a single digit.
  Else
    Display digit, " " is NOT a single digit.
  End If
  ```
- 3. Why doesn't the following pseudocode perform as indicated in the comments?
  ```
  // This program counts the characters in a string.
  Declare String word
  Declare Integer index
  Declare Integer letters = 0
  ```
  ```
  // Get the input from the user.
  Display "Enter a word."
  Input word
  ```
  ```
  // Count the characters in the string.
  For index = 0 To length(word)
    Set count = count + 1
  End For
  Display "That word contains ", count, " characters."
  

## Programming Exercises

- 1. Backward String
  Design a program that prompts the user to enter a string and then displays the string contents backward. For instance, if the user enters "gravity" the program should display "ytivarg."
- 2. Sentence Capitalizer
  Design a program that prompts the user to enter a string containing multiple sentences, and then displays the string with the first character of each sentence capitalized. For, if the user enters "hello. my name is Joe. What is your name?" (Hint: the program should display "Hello. My name is Joe. The Upper function can be used to convert a single character to uppercase.)
- 3. Vowels and Consants
  Design a program that prompts the user to enter a string. The program should then display the number of vowels and consonants in the string.
- 4. Sum of Digits in a String
  Design a program that asks the user to enter a string containing a series of digits without separating them. The program should display the sum of all digit numbers in the string. For example, if the user enters 2514, the method should return 12, which is the sum of 2, 5, and 4. (Hint: stringTo function can be used.)
- 5. Most Frequent Character
  Design a program that prompts the user to enter a string, and displays the character that appears most frequently in the string.
- 6. Alphabetic Number Translator
  Many companies use telephone numbers like 555-GET-FOOD so the number is easier for customers to remember. On a standard telephone, the alphabetic letters are mapped to numbers in the following fashion:
  | Letter | Number |
  | :--- | :--- |
  | A, B, and C | 2 |
  | D, E, and F | 3 |
  | G, H, and I | 4 |
  | J, K, and L | 5 |
  | M, N, and O | 6 |
  | P, Q, and R | 7 |
  | T, U, and V | 8 |
  | W, X, Y, and Z | 9 |
  Design a program that asks the user to enter a character in the format XXX-XXXX. The program should display the telephone number with all alphabetic characters that appeared in the original translated to their numeric equivalent. For example, if the user enters 555-GET-FOOD the program should display 555-438-3663.
- 7. Word Separator
  Design a program that accepts as input a sentence in which all the words run together, the first character of each word is uppercase. Convert the sentence to a string in which words are separated by spaces and only the first word starts with an uppercase letter. For example, the string "StopAndSmellTheRoses." (Hint: toLower library can be used to lowercase).
- 8. Pig Latin
  Design a program that reads a sentence as input and converts each word to "Pig Latin." In one version of Pig Latin you convert a word by removing the first letter, placing it at the end of the word, and then appending "ay" to the word. Here is an example:
  English: SLEPT OF THE NIGHT
  Pig Latin: IAY LAYPS OSTMAY FOAY IGHTNA
- 9. Morse Code Converter
  Design a program that asks the user to enter a string, and then converts it to Morse code. Morse code is a code where each letter of the English alphabet, each digit, and various punctuation characters are represented by a series of dots and dashes. Table 12-4 shows part of the code.
- 10. File Encryption
  File encryption is the science of writing the contents of a file in a secret code. For this assignment you will design a program that opens a file and encrypts its contents. Assume the file that you are encrypting contains a list of strings. The program should open the file and read its contents, one string at a time. The program reads a string from the file, it substitutes each character of the string for an alternate character. It writes the encoded string out to a second file. When the program is finished, the second file will be a version of the first file, but written in a secret code.
- 11. File Decryption Filter
  Design a program that decrypts the file produced by the program in Programming Exercise 10. The decryption program should read the contents of the coded file, restore the data to its original state, and write it to another file.

| Character | Code | Character | Code | Character | Code | Character | Code |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| space | space | 6 | . . . . | G | -- -- | Q | -- - |
| comma | --, -- | 7 | . -- . | H | .. | R | - . |
| period | .-- .. | 8 | --- | I | -- | S | ... |
| ? | . . . . | 9 | .... | J | . . . | T | . - |
| 0 | ---- | A | - - | K | -- - | U | -- - |
| 1 | ---- | B | .-- . | L | .-- . | V | ... |
| 2 | .. --- | C | . - . | M | -- | W | --- |
| 3 | . . -- | D | -- . | N | - | X | --, - |
| 4 | . . . - | E | . | O | --- | Y | --, -- |
| 5 | .... | F | .-- . | P | --- . | Z | --, -- |
