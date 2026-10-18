should produce the output

```
I love you, you love!
```

Of course, the output will not always make sense. For example, the input string

```
John will run home.
```

should produce the output

```
Love love run love.
```

If the four-letter word starts with a capital letter, it should be replaced by "Love", not by "love". You need not check capitalization, except for the first letter of a word. A word is any string consisting of the letters of the alphabet and delimited at each end by a blank, the end of the line, or any other character that is not a letter. Your program should repeat this action until the user says to quit.

+   6. Write a program that reads in a line of text and outputs the line with all the digits in all integer numbers replaced with 'x'. For example,

Input:

```
My userID is john17 and my 4 digit pin is 1234 which is secret.
```

Output:

```
My userID is john17 and my x digit pin is xxxx which is secret.
```

Note that if a digit is part of a word, then the digit is not changed to an 'x'. For example, note that john17 is NOT changed to johnxx. Include a loop that allows the user to repeat this calculation again until the user says she or he wants to end the program.

+   7. Write a program that can be used to train the user to use less sexist language by suggesting alternative versions of sentences given by the user. The program will ask for a sentence, read the sentence into a string variable, and replace all occurrences of masculine pronouns with gender-neutral pronouns. For example, it will replace "he" with "she or he". Thus, the input sentence

```
See an adviser, talk to him, and listen to him.
```

should produce the following suggested changed version of the sentence:

```
See an adviser, talk to her or him, and listen to her or him.
```

Be sure to preserve uppercase letters for the first word of the sentence. The pronoun "his" can be replaced by "her(s)"; your program need