
### R4.23 The nested loops

```
for (int i = 1; i <= height; i++)
{
    for (int j = 1; j <= width; j++) { cout << "*"; }
    cout << endl;
}
```

display a rectangle of a given width and height, such as

```
****
****
****
```

Write a *single* for loop that displays the same rectangle.

### R4.24

Suppose you design an educational game to teach children how to read a clock. How do you generate random values for the hours and minutes?

### R4.25

In a travel simulation, Harry will visit one of his friends that are located in three states. He has ten friends in California, three in Nevada, and two in Utah. How do you produce a random number between 1 and 3, denoting the destination state, with a probability that is proportional to the number of friends in each state?

## PROGRAMMING EXERCISES

### P4.1

Write programs with loops that compute

- a. The sum of all even numbers between 2 and 100 (inclusive).
- b. The sum of all squares between 1 and 100 (inclusive).
- c. All powers of 2 from 2⁰ up to 2²⁰.
- d. The sum of all odd numbers between a and b (inclusive), where a and b are inputs.
- e. The sum of all odd digits of an input. (For example, if the input is 32677, the sum would be 3 + 7 + 7 = 17.)

### P4.2

Write programs that read a sequence of integer inputs and print

- a. The smallest and largest of the inputs.
- b. The number of even and odd inputs.
- c. Cumulative totals. For example, if the input is 1 7 2 9, the program should print 1 8 10 19.
- d. All adjacent duplicates. For example, if the input is 1 3 3 4 5 5 6 6 2, the program should print 3 5 6.

### P4.3

Write programs that read a line of input as a string and print

- a. Only the uppercase letters in the string.
- b. Every second letter of the string.
- c. The string, with all vowels replaced by an underscore.
- d. The number of vowels in the string.
- e. The positions of all vowels in the string.

### P4.4

Complete the program in How To 4.1 on page 162. Your program should read twelve temperature values and print the month with the highest temperature.

### P4.5 Credit Card Number Check

The last digit of a credit card number is the *check digit*, which protects against transcription errors such as an error in a single digit or switching two digits. The following method is used to verify actual credit card numbers but, for simplicity, we will describe it for numbers with 8 digits instead of 16:

- Starting from the rightmost digit, form the sum of every other digit. For example, if the credit card number is 43589795, then you form the sum 5 + 7 + 8 + 3 = 23.
- Double each of the digits that were not included in the preceding step. Add all digits of the resulting numbers. For example, with the number given above, doubling the digits, starting with the next-to-last one, yields 18 18 10 8. Adding all digits in these values yields 1 + 8 + 1 + 8 + 1 + 0 + 8 = 27.
- Add the sums of the two preceding steps. If the last digit of the result is 0, the number is valid. In our case, 23 + 27 = 50, so the number is valid.

Write a program that implements this algorithm. The user should supply an 8-digit number, and you should print out whether the number is valid or not. If it is not valid, you should print out the value of the check digit that would make the number valid.

### P4.6 Currency conversion

Write a program that first asks the user to type today’s exchange rate between U.S. dollars and Japanese yen, then reads U.S. dollar values and converts each to yen. Use 0 as a sentinel.

![](img/23fb3582e93ebc95909e1de029c3d388_206_0.png)

### P4.7

Write a program that first asks the user to type in today’s exchange rate between U.S. dollars and Japanese yen, then reads U.S. dollar values and converts each to Japanese yen. Use 0 as the sentinel value to denote the end of dollar inputs. Then the program reads a sequence of yen amounts and converts them to dollars. The second sequence is terminated by another zero value.

### P4.8

Write a program that reads a set of floating-point values. Ask the user to enter the values, then print

- the average of the values.
- the smallest of the values.
- the largest of the values.
- the range, that is the difference between the smallest and largest.

Of course, you may only prompt for the values once.

### P4.9

Translate the following pseudocode for finding the minimum value from a set of inputs into a C++ program.

- Set a Boolean variable `first` to true.
- While another value has been read successfully
  - If first is true
    - Set the minimum to the value.
    - Set first to false.
  - Else if the value is less than the minimum
    - Set the minimum to the value.
- Print the minimum.

### P4.10

Translate the following pseudocode for randomly permuting the characters in a string into a C++ program.

- Read a word.
- Repeat `word.length()` times
  - Pick a random position `i` in the word.
  - Pick a random position `j > i` in the word.
  - Swap the letters at positions `j` and `i`.
- Print the word.

![](img/23fb3582e93ebc95909e1de029c3d388_207_0.png)

To swap the letters, construct substrings as follows:

![](img/23fb3582e93ebc95909e1de029c3d388_207_1.png)

Then replace the string with

```
first + word.substr(j, 1) + middle + word.substr(i, 1) + last
```

### P4.11

Write a program that reads a word and prints each character of the word on a separate line. For example, if the user provides the input "Harry", the program prints

- H
- a
- r
- r
- y

### P4.12

Write a program that reads a word and prints the word in reverse. For example, if the user provides the input "Harry", the program prints

`yrraH`

### P4.13

Write a program that reads a word and prints the number of vowels in the word. For this exercise, assume that a, e, i, o, u, and y are vowels. For example, if the user provides the input "Harry", the program prints 2 vowels.

### P4.14

Write a program that reads a word and prints the number of syllables in the word. For this exercise, assume that syllables are determined as follows: Each sequence of adjacent vowels a, e, i, o, u, y, except for the last e in a word, is a syllable. However, if that algorithm yields a count of 0, change it to 1. For example,

| Word | Syllables |
|---|---:|
| Harry | 2 |
| hairy | 2 |
| hare | 1 |
| the | 1 |

### P4.15

Write a program that reads a word and prints all substrings, sorted by length. For example, if the user provides the input "rum", the program prints

- r
- u
- m
- ru
- um
- rum

### P4.16

Write a program that reads a number and prints all of its *binary digits*: Print the remainder number % 2, then replace the number with number / 2. Keep going until the number is 0. For example, if the user provides the input 13, the output should be

- 1
- 0
- 1
- 1

### P4.17 Mean and standard deviation

Write a program that reads a set of floating-point data values. Choose an appropriate mechanism for prompting for the end of the data set. When all values have been read, print out the count of the values, the average, and the standard deviation. The average of a data set \(\{x_1, \ldots, x_n\}\) is \(\bar{x} = \sum x_i/n\), where \(\sum x_i = x_1 + \cdots + x_n\) is the sum of the input values. The standard deviation is

\[
s = \sqrt{\frac{\sum (x_i - \bar{x})^2}{n - 1}}
\]

However, this formula is not suitable for the task. By the time the program has computed \(\bar{x}\), the individual \(x_i\) are long gone. Until you know how to save these values, use the numerically less stable formula

\[
s = \sqrt{\frac{\sum x_i^2 - \frac{1}{n}(\sum x_i)^2}{n - 1}}
\]

You can compute this quantity by keeping track of the count, the sum, and the sum of squares as you process the input values.

### P4.18

The *Fibonacci numbers* are defined by the sequence

\(f_1 = 1\)

\(f_2 = 1\)

\(f_n = f_{n-1} + f_{n-2}\)

Reformulate that as

```
fold1 = 1;
fold2 = 1;
fnew = fold1 + fold2;
```

After that, discard fold2, which is no longer needed, and set fold2 to fold1 and fold1 to fnew. Repeat fnew an appropriate number of times.

Implement a program that computes the Fibonacci numbers in that way.

![](img/23fb3582e93ebc95909e1de029c3d388_208_0.png)
