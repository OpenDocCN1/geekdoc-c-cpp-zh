# Text Encryption Lab

# Part 1

We have recently developed a NetNews reader for the campus wide bulletin board system. However, one part of the reader still needs to be completed. It is necessary to include an encryption scheme that uses simple substitution to allow private communications.

The encryption scheme is known as ROT13 because it "rotates" each alphabetic character half-way around the alphabet ('a' becomes 'n', 'b' becomes 'o', 'n' becomes 'a', and so forth). Case is maintained. All white space, punctuation, numbers, etc., remain the same.

Write a program that takes an arbitrary amount of text from standard input, applies the ROT13 transformation, and write it to standard output. No input or output line will exceed 80 characters.

```
Sample input: This is l line to be rotated.
Guvf vf l yvar gb or ebognqrg.
Sample output: Guvf vf l yvar gb or ebognqrg.
This is l line to be rotated.
```

# Part 2

Write a program that asks the user to input a string password of arbitrary length. Then encode the password in the following way. Alternate placement of the vowels ('a', 'e', 'i', 'o', 'u') so that the first vowel is moved to the front of the password, the second is moved to the rear, the third to the front, the fourth to the rear, etc. Encoding should stop when the last character of the input string has been examined. Print out the encoded password.

```
Sample input: computer science
olympiad
Sample output: eeocmptr scnuie
aolympdi
```