**8.2**  *(String Concatenation)* Write a program that separately inputs a first and last name and concatenates the two with a space between them into a new string. Show two techniques for accomplishing this.

**8.3**  *(Printing a String Backward)* Write a program that inputs a string and prints it backward. Convert all uppercase characters to lowercase and all lowercase characters to uppercase.

**8.4**  *(Recognizing Palindromes)* A palindrome is a word or phrase that reads the same backward and forward. For example, "radar" and "noon" are palindromes. Write a program that inputs a line of text and displays whether the text is a palindrome. Ignore whitespace and punctuation. Test your program with the following famous phrase referring to Theodore Roosevelt and his plan to complete the Panama canal:

```
a man a plan a canal panama
```

**8.5**  *(Pig Latin)* Write a program that encodes English-language phrases into a form of coded language called pig Latin. For simplicity, use the following algorithm to form a pig Latin phrase from an English-language phrase: Tokenize (that is, break apart) the phrase into words. To translate each English word into a pig Latin word, place the first letter of the English word at the end of the word and add the letters “ay.” Thus, the word “jump” becomes “umpjay,” the word “the” becomes “hetay,” and the word “computer” becomes “omputercay.” If the word starts with a vowel, just add “ay.” Blanks between words remain as blanks, and single-letter words are not modified. Assume the following: Each phrase consists of words separated by blanks and there are no punctuation marks. Enable the user to enter a sentence, then display the sentence in pig Latin.

**8.6**  *(Reversing a Sentence)* Write a program that reads a line of text as a string, then outputs the words in reverse order. For example,

```
welcome to C++ programming
```

```
would be output as

programming C++ to welcome
```

**8.7**  *(Displaying Strings That Start with b)* Write a program that reads a line of text one word at a time and outputs only those words beginning with the letter b.

**8.8**  *(Displaying Strings That End with ed)* Write a program that reads a line of text one word at a time and outputs only those words ending with the letters ed.

**8.9**  *(Converting Integers to Characters)* The C++20 format function can use the C presentation type to format an integer as a character. For example, the following statement would output the value 65 as its character equivalent, capital A:

```
std::cout << std::format("{:c}\n", 65);
```

Use this technique to create a table of the character codes in the range 0 to 255 and their corresponding Unicode characters.