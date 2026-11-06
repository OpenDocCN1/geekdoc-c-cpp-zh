
### 21.22 *(Converting Strings to Floating-Point Numbers)*

Write a program that inputs four strings that represent floating-point values, converts the strings to double values, sums the values, and prints the total of the four values. Use only the C-style string-processing techniques shown in this chapter.

### 21.23 *(Searching for Substrings)*

Write a program that inputs a line of text and a search string from the keyboard. Using function `strstr`, locate the first occurrence of the search string in the line of text, and assign the location to variable `searchPtr` of type `char *`. If the search string is found, print the remainder of the line of text beginning with the search string. Then use `strstr` again to locate the next occurrence of the search string in the line of text. If a second occurrence is found, print the remainder of the line of text beginning with the second occurrence. *Hint:* The second call to `strstr` should contain the expression `searchPtr + 1` as its first argument.

### 21.24 *(Searching for Substrings)*

Write a program based on the program of Exercise 21.23 that inputs several lines of text and a search string, then uses function `strstr` to determine the total number of occurrences of the string in the lines of text. Print the result.

### 21.25 *(Searching for Characters)*

Write a program that inputs several lines of text and a search character and uses function `strchr` to determine the total number of occurrences of the character in the lines of text.

### 21.26 *(Searching for Characters)*

Write a program based on the program of Exercise 21.25 that inputs several lines of text and uses function `strchr` to determine the total number of occurrences of each letter of the alphabet in the text. Uppercase and lowercase letters should be counted together. Store the totals for each letter in an array, and print the values in tabular format after the totals have been determined.

### 21.27

*The chart in Appendix B shows the numeric code representations for the characters in the ASCII character set. Study this chart, then state whether each of the following is true or false:*

- a) The letter “A” comes before the letter “B.”
- b) The digit “9” comes before the digit “0.”
- c) The commonly used symbols for addition, subtraction, multiplication, and division all come before any of the digits.
- d) The digits come before the letters.
- e) If a sort program sorts strings into ascending sequence, then the program will place the symbol for a right parenthesis before the symbol for a left parenthesis.

### 21.28 *(Strings Beginning with b)*

Write a program that reads a series of strings and prints only those strings beginning with the letter “b.”

### 21.29 *(Strings Ending with ED)*

Write a program that reads a series of strings and prints only those strings that end with the letters “ED.”

### 21.30 *(Displaying Characters for Given ASCII Codes)*

Write a program that inputs an ASCII code and prints the corresponding character. Modify this program so that it generates all possible three-digit codes in the range 000–255 and attempts to print the corresponding characters. What happens when this program is run?

### 21.31 *(Write Your Own Character-Handling Functions)*

Using the ASCII character chart in Appendix B as a guide, write your own versions of the character-handling functions in Fig. 21.17.

### 21.32 *(Write Your Own String Conversion Functions)*

Write your own versions of the functions in Fig. 21.27 for converting strings to numbers.

### 21.33 *(Write Your Own String Searching Functions)*

Write your own versions of the functions in Fig. 21.34 for searching strings.

### 21.34 *(Write Your Own Memory Handling Functions)*

Write your own versions of the functions in Fig. 21.41 for manipulating blocks of memory.

### 21.35 What does this program do?

```cpp
// Ex. 21.35: ex21_35.cpp
// What does this program do?
#include <iostream>
using namespace std;

bool mystery3( const char *, const char * ); // prototype

int main()
{
   char string1[ 80 ], string2[ 80 ];

   cout << "Enter two strings: ";
   cin >> string1 >> string2;
   cout << "The result is " << mystery3( string1, string2 ) << endl;
} // end main

// What does this function do?
bool mystery3( const char *s1, const char *s2 )
{
   for ( ; *s1 != '\0' && *s2 != '\0'; s1++, s2++ )
   {
      if ( *s1 != *s2 )
         return false;
   }

   return true;
} // end function mystery3
```

### 21.36 *(Comparing Strings)*

Write a program that uses function `strcmp` to compare two strings input by the user. The program should state whether the first string is less than, equal to, or greater than the second string.

### 21.37 *(Comparing Strings)*

Write a program that uses function `strncmp` to compare two strings input by the user. The program should input the number of characters to compare. The program should state whether the first string is less than, equal to, or greater than the second string.

### 21.38 *(Randomly Creating Sentences)*

Write a program that uses random number generation to create sentences. The program should use four arrays of pointers to `char` called `article`, `noun`, `verb`, and `preposition`. The program should create a sentence by selecting a word at random from each array in the following order: article, noun, verb, preposition, article, and noun. As each word is picked, it should be concatenated to the previous words in a character array that is large enough to hold the entire sentence. The words should be separated by spaces. When the final sentence is output, it should start with a capital letter and end with a period. The program should generate 20 such sentences.

The arrays should be filled as follows: The article array should contain the articles “the,” “a,” “one,” “some,” and “any”; the noun array should contain the nouns “boy,” “girl,” “dog,” “town,” and “car”; the verb array should contain the verbs “drove,” “jumped,” “ran,” “walked,” and “skipped”; the preposition array should contain the prepositions “to,” “from,” “over,” “under,” and “on.”

After completing the program, modify it to produce a short story consisting of several of these sentences. (How about a random term-paper writer!)

### 21.39 *(Limericks)*

A limerick is a humorous five-line verse in which the first and second lines rhyme with the fifth, and the third line rhymes with the fourth. Using techniques similar to those developed in Exercise 21.38, write a C++ program that produces random limericks. Polishing this program to produce good limericks is a challenging problem, but the result will be worth the effort!

### 21.40 *(Pig Latin)*

Write a program that encodes English-language phrases into Pig Latin. Pig Latin is a form of coded language often used for amusement. Many variations exist in the methods used to form Pig Latin phrases. For simplicity, use the following algorithm: To form a Pig Latin phrase from an English-language phrase, tokenize the phrase into words with function `strtok`. To translate each English word into a Pig Latin word, place the first letter of the English word at the end of the English word and add the letters “ay.” Thus, the word “jump” becomes “umpjay,” the word “the” becomes “hetay,” and the word “computer” becomes “omputercay.” Blanks between words remain as blanks. Assume that the English phrase consists of words separated by blanks, that there are no punctuation marks, and that all words have two or more letters. Function `printLatinWord` should display each word. *Hint:* Each time a token is found in a call to `strtok`, pass the token pointer to function `printLatinWord` and print the Pig Latin word.

### 21.41 *(Tokenizing Phone Numbers)*

Write a program that inputs a telephone number as a string in the form `(555) 555-5555`. The program should use function `strtok` to extract the area code as a token, the first three digits of the phone number as a token, and the last four digits of the phone number as a token. The seven digits of the phone number should be concatenated into one string. Both the area code and the phone number should be printed.

### 21.42 *(Tokenizing and Reversing a Sentence)*

Write a program that inputs a line of text, tokenizes the line with function `strtok`, and outputs the tokens in reverse order.

### 21.43 *(Alphabetizing Strings)*

Use the string-comparison functions discussed in Section 21.10 and the techniques for sorting arrays developed in Chapter 7 to write a program that alphabetizes a list of strings. Use the names of 10 towns in your area as data for your program.

### 21.44 *(Write Your Own String Copy and Concatenation Functions)*

Write two versions of each string-copy and string-concatenation function in Fig. 21.21. The first version should use array subscripting, and the second should use pointers and pointer arithmetic.

### 21.45 *(Write Your Own String Comparison Functions)*

Write two versions of each string-comparison function in Fig. 21.21. The first version should use array subscripting, and the second should use pointers and pointer arithmetic.

### 21.46 *(Write Your Own String Length Function)*

Write two versions of function `strlen` in Fig. 21.21. The first version should use array subscripting, and the second should use pointers and pointer arithmetic.

## Special Section: Advanced String-Manipulation Exercises

The preceding exercises are keyed to the text and designed to test your understanding of fundamental string-manipulation concepts. This section includes a collection of intermediate and advanced string-manipulation exercises. You should find these problems challenging, yet enjoyable. The problems vary considerably in difficulty. Some require an hour or two of program writing and implementation. Others are useful for lab assignments that might require two or three weeks of study and implementation. Some are challenging term projects.

### 21.47 *(Text Analysis)*

The availability of computers with string-manipulation capabilities has resulted in some rather interesting approaches to analyzing the writings of great authors. Much attention has been focused on whether William Shakespeare ever lived. Some scholars believe there is substantial evidence that Francis Bacon, Christopher Marlowe, or other authors actually penned the masterpieces attributed to Shakespeare. Researchers have used computers to find similarities in the writings of these authors. This exercise examines three methods for analyzing texts with a computer. Thousands of texts, including Shakespeare, are available online at www.gutenberg.org.

- a) Write a program that reads several lines of text from the keyboard and prints a table indicating the number of occurrences of each letter of the alphabet in the text. For example, the phrase
