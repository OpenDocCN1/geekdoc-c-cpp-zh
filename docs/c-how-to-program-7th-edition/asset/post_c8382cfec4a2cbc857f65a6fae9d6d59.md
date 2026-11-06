
- a) Write a program that encrypts a message using rot13.
- b) Write a program that decrypts the scrambled message using 13 as the key.
- c) After writing the programs of part (a) and part (b), briefly answer the following question: If you did not know the key for part (b), how difficult do you think it would be to break the code? What if you had access to substantial computing power (e.g., supercomputers)? In Exercise 18.25 we ask you to write a program to accomplish this.

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

**18.16** (*Counting Palindromes*) Write a program that inputs a sentence and counts the number of palindromes in it. A palindrome is a word that reads the same backward and forward. For example, "tree" is not a palindrome, but "noon" is.

**18.17** (*Counting Vowels*) Write a program that counts the total number of vowels in a sentence. Output the frequency of each vowel.

**18.18** Write a program that inserts the characters "******" in the exact middle of a string.

**18.19** (*Erasing Characters from a string*) Write a program that erases the sequences "by" and "By" from a string.

**18.20** (*Replacing Punctuation and Tokenizing strings*) Write a program that inputs a line of text, replaces all punctuation marks with spaces and uses the C-string library function strtok to tokenize the string into individual words.

**18.21** (*Reversing a string with Iterators*) Write a program that inputs a line of text and prints the text backward. Use iterators in your solution.

**18.22** (*Reversing a string with Iterators using Recursion*) Write a recursive version of Exercise 18.21.

**18.23** (*Using the erase Functions with Iterator Arguments*) Write a program that demonstrates the use of the erase functions that take iterator arguments.

**18.24** (*Letter Pyramid*) Write a program that generates the following from the string "abcdefghijklmnopqrstuvwxyz":

```
        a
       bcb
      cdedc
     defgfed
    efghihgfe
   fghijkjihgf
  ghijklmlkjihg
 hijklmnonmlkjih
ijklmnopqponmlkji
jklmnopqrstsrqponmlkj
klmnopqrstuvwvutsrqponmlk
lmnopqrstuvwxyxwvutsrqponml
mnopqrstuvwxyzazyxwvutsrqponm
nopqrstuvwxyzzyxwvutsrqpon
```

**18.25** (*Simple Decryption*) In Exercise 18.7, we asked you to write a simple encryption algorithm. Write a program that will attempt to decrypt a "rot13" message using simple frequency substitution. (Assume that you do not know the key.) The most frequent letters in the encrypted phrase should be replaced with the most commonly used English letters (a, e, i, o, u, s, t, r, etc.). Write the possibilities to a file. What made the code breaking easy? How can the encryption mechanism be improved?

**18.26** (*Sorting strings*) Write a version of the selection sort routine (Fig. 8.20) that sorts strings. Use function swap in your solution.

**18.27** (*Enhanced Employee Class*) Modify class Employee in Figs. 13.6–13.7 by adding a private utility function called isValidSocialSecurityNumber. This member function should validate the format of a social security number (e.g., ###-##-####, where # is a digit). If the format is valid, return true; otherwise return false.

## Making a Difference

**18.28** (*Cooking with Healthier Ingredients*) Obesity in the United States is increasing at an alarming rate. Check the map from the Centers for Disease Control and Prevention (CDC) at

# 19 Searching and Sorting

> With sobs and tears
> he sorted out
> Those of the largest size ...
> —Lewis Carroll
>
> Attempt the end, and never
> stand to doubt;
> Nothing's so hard, but search
> will find it out.
> —Robert Herrick
>
> 'Tis in my memory lock'd,
> And you yourself shall keep the
> key of it.
> —William Shakespeare
>
> It is an immutable law in
> business that words are words,
> explanations are explanations,
> promises are promises — but
> only performance is reality.
> —Harold S. Green

## Objectives

In this chapter you'll learn:

- To search for a given value in a vector using binary search.
- To use Big O notation to express the efficiency of searching and sorting algorithms and to compare their performance.
- To sort a vector using the recursive merge sort algorithm.
- To understand the nature of algorithms of constant, linear and quadratic runtime.

![](img/023f159fdd47d944d48e08843cea732d_820_0.png)

## Outline

- **19.1** Introduction
- **19.2** Searching Algorithms
  - 19.2.1 Efficiency of Linear Search
  - 19.2.2 Binary Search
- **19.3** Sorting Algorithms
  - **19.3.1** Efficiency of Selection Sort
  - **19.3.2** Efficiency of Insertion Sort
  - **19.3.3** Merge Sort (A Recursive Implementation)
- **19.4** Wrap-Up

*Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises*

## 19.1 Introduction

Searching data involves determining whether a value (referred to as the search key) is present in the data and, if so, finding the value’s location. Two popular search algorithms are the simple linear search (introduced in Section 7.7) and the faster but more complex binary search, which is introduced in this chapter.

Sorting places data in order, typically ascending or descending, based on one or more sort keys. A list of names could be sorted alphabetically, bank accounts could be sorted by account number, employee payroll records could be sorted by social security number, and so on. Previously, you learned about insertion sort (Section 7.8) and selection sort (Section 8.6). This chapter introduces the more efficient, but more complex merge sort. Figure 19.1 summarizes the searching and sorting algorithms discussed in the examples and exercises of this book. This chapter also introduces Big O notation, which is used to estimate the worst-case runtime for an algorithm—that is, how hard an algorithm may have to work to solve a problem.

| Algorithm | Location |
|---|---|
| *Searching Algorithms* | |
| Linear search | Section 7.7 |
| Binary search | Section 19.2.2 |
| Recursive linear search | Exercise 19.8 |
| Recursive binary search | Exercise 19.9 |
| Binary tree search | Section 20.7 |
| Linear search of a linked list | Exercise 20.21 |
| `binary_search` standard library function | Section 22.5.6 |
| *Sorting Algorithms* | |
| Insertion sort | Section 7.8 |
| Selection sort | Section 8.6 |
| Recursive merge sort | Section 19.3.3 |
| Bubble sort | Exercises 19.5 and 19.6 |
| Bucket sort | Exercise 19.7 |
| Recursive quicksort | Exercise 19.10 |

**Fig. 19.1** Searching and sorting algorithms in this text. (Part 1 of 2.)
