
18. Modify the program in Problem 17 so that it prints a message to the user giving the range of angles that are covered in the data file after reading the values.

19. Write a function that could be used to verify that the flight-path angles are in ascending order. The function should return a zero if the angles are not in order and a 1 if they are in order. Assume that the corresponding function prototype is

```
int ordered(double x[], int num_pts);
```

20. Write a function that receives two one-dimensional arrays that correspond to the flight-path angles and the corresponding coefficients of lift. The function should sort the flight-path angles into ascending order while maintaining the correspondence between the flight-path angles and the corresponding coefficients of lift. Assume that the corresponding function prototype is

```
void reorder(double x[], double y[]);
```

21. Modify the program developed in Problem 17 such that it uses the function developed in Problem 19 to determine whether the data are in the desired order. If they are not in the desired order, use the function developed in Problem 20 to reorder them.

## Noise Signals

In engineering simulations, we often want to generate a floating-point sequence of values with a specified mean and variance. The function developed in this chapter allows us to generate numbers between limits $a$ and $b$, but it does not allow us to specify the mean and variance. By using results from probability, the following relationships can be derived between the limits of a uniform random sequence and its theoretical mean $\mu$ and variance $\sigma^2$: $\sigma^2 = \frac{(b-a)^2}{12}, \quad \mu = \frac{(a+b)}{2}.$

22. Write a program that uses the rand_float function developed in Chapter 5 to generate sequences of random floating-point values between 4 and 10. Then compare the computed mean and variance to the theoretical values computed. As you use more and more random numbers, the computed values and the theoretical values should become closer.

23. Write a program that uses the rand_float function developed in Chapter 5 to generate two sequences of 500 points. Each sequence should have a theoretical mean of 4, but one sequence should have a variance of 0.5, and the other should have a variance of 2. Check the computed means and compare to the theoretical means. (Hint: Use the two previous equations to write two equations with two unknowns. Then solve for the unknowns by hand.)

24. Write a program that uses the rand_float function developed in Chapter 5 to generate two sequences of 500 points. Each sequence should have the same variance of 3.0, but one sequence should have a mean of 0.0, and the other should have a mean of -4.0. Compare the theoretical and computed values for mean and variance. (Hint: Use the two previous equations to write two equations with two unknowns. Then solve for the unknowns by hand.)

25. Write a function named rand_mv that generates a random floating-point value with a specified mean and variance that are input parameters to the function. Assume that the corresponding function prototype is

```
double rand_mv(double mean, double var);
```

Use the rand_float function developed in Chapter 5.

## Cryptography

Cryptography. The science of developing secret codes has interested many people for centuries. Some of the simplest codes involve replacing a character, or a group of characters with another character, or group of characters. To easily decode these messages, the decoder needs the “key” that shows the replacement characters. In recent times, computers have been used very successfully to decode many codes that initially were assumed to be unbreakable. The next set of problems considers simple codes and schemes for decoding them. Generate files to the programs.

26. One step in decoding a simple code without knowing the coding scheme, involves counting the number of occurrences of each character. Then, knowing that the most common letter in English is ‘e’, the letter that occurs most commonly in the coded message is replaced by ‘e’. Similar replacements are then made based on the number of occurrences of characters in the coded message and the known occurrences of characters in the English language. This decoding often provides enough of the correct replacements that the incorrect replacements can then be determined. For this problem, write a program that reads a data file and determines the number of occurrences of each of the characters in the file. Then, print the characters and the number of times that they occurred. If a character does not occur, do not print it. (Hint: Use an array to store the occurrences of the characters based on their ASCII codes.)

27. Another simple code encodes a message in text such that the true message is represented by the first letter of each word. There are no spaces between the words, but the decoded string of characters can easily be separated into words by a person. Write a program to read a data file and determine the secret message stored by the sequence of first letters of the words. (Hint: Store the first letter of each word in a character string.)

28. Assume that the true secret message in Problem 27 is stored in the second letter of each word. Write a program to read a data file and determine the secret message stored in the file.

29. Assume that the true secret message in Problem 27 is represented by the characters that are three characters to the right in the collating sequence from the first letters of the words. Write a program to read a data file and determine the secret message stored in the file using this decoding scheme.

30. Write a program that encodes the text in a data file using a character array named key that contains 26 characters. This key is read from the keyboard, the first letter contains the character that is to replace the letter a in the data file, the second letter contains the letter that is to replace the letter b in the data file, and so on. Assume that all punctuation is to be replaced by spaces. Check to be sure that the key does not map two different characters to the same one during the encoding.

31. Write a program which decodes the file that is the output of Problem 30. Assume that the same integer key is read from the keyboard by this program and is used in the decoding steps. Note that you will not be able to restore the punctuation characters. (A palindrome is a word (noon), sentence (Draw a level award), or number (18781) that reads the same backward or forward. (Note that whitespace is ignored when determining whether a word, sentence, or number is a palindrome.))

32. Write a program that reads a line of text from standard input and determines whether the line of text is a palindrome.

33. Write a program that reads text from a data file. The program should read each line in the data file (read lines until an end of file is encountered), print each line, and also print a message that indicates whether the line is a palindrome.

## Calculating Probabilities

34. Add a method to the CardDeck class named randomDraw(). This method should return one card, drawn from a random location in the deck. Use this method to simulate the probability of drawing two face cards from a shuffled deck.

35. Add a method to the CardDeck class named isEmpty(). This method should return true if the deck is empty, false otherwise. Write a driver to test the new method.

36. Write a program that uses the Card and CardDeck classes to deal a hand of 13 cards and count the value of the hand based on the number of face cards in the hand. Assume an Ace is worth 4 points, a King is worth 3 points, a Queen is worth 2 points and a Jack is worth 1 point. Thus, if the hand held 2 Aces, 1 King and 3 Jacks, the value of the hand would be 14. The program should display the hand that was dealt and the value of the hand.

37. Write a simulation to estimate the probability of drawing a 13-card hand having no face cards, from a deck of 52 cards.

38. Write a simulation to estimate the probability of drawing a 5-card hand that holds 2 Kings and 1 Ace.

39. Write a simulation to estimate the probability of drawing a 5-card hand that holds 2 pairs.

## Programmer-Defined Data Types

40. Define a class to implement the concept of a line. Your class should have two private data members: length, fixedPoint. Include a complete set of accessors, mutators, constructors, and additional methods to:

- print location and length of a line
- move (translate) a line
- resize a line

Draw a UML class diagram and write a driver to test your class.

41. Define a class to implement the concept of a circle. Your class should have two private data members: radius, centerPoint. Include a complete set of accessors, mutators, constructors, and additional methods to:

- print location and radius of a circle
- move (translate) a circle
- resize a circle

Draw a UML class diagram and write a driver to test your class.

42. Define a class to represent a date. Your class should have three data members: month, day, and year. Include a complete set of accessors, mutators, constructors, and additional functions to:

- print a date as month/day/year (10/1/1999)
- print a date as month day, year (October 1, 1999)

Draw a UML class diagram and write a driver to test your class.
