7. The Nimble Fingers Typing School assigns grades based on words typed per minute, as shown in Figure 6-26. Write a program named TypingGrades that allows a user to enter a student's number of words typed. The output is the letter grade.

| Words typed | Grade |
| 0-15 | F |
| 16–30 | D |
| 31-50 | C |
| 51–75 | B |
| 76 and over | A |

**Figure 6-26** Typing grades

8. Write a program for The Carefree Resort named ResortPrices that prompts the user to enter the number of days for a resort stay. Then display the price per night and the total price. Nightly rates are $200 for one or two nights; $180 for three or four nights; $160 for five, six, or seven nights; $145 for eight or more.

9. In Chapter 5, you wrote a HomeSales application for three salespeople: Danielle, Edward, and Francis. Now, modify the program to use arrays to store the salesperson names, initials, and accumulated sales values.

10. Create a game similar to Hangman named GuessWord in which a player guesses letters to replicate a hidden word. Store at least eight words in an array, and randomly select one to be the hidden word. (The statements to generate a random number are shown in the Exercises in the “Decision Making” and “Looping” chapters.) Initially, display the hidden word using asterisks to represent each letter. Allow the user to guess letters to replace the asterisks in the hidden word until the user completes the entire word. If the user guesses a letter that is not in the hidden word, display an appropriate message. If the user guesses a letter that appears multiple times in the hidden word, make sure that each correct letter is played. Figure 6-27 shows typical games in a console-based application and in a GUI application. In the GUI, the user has successfully guessed *e*, and is about to guess *r*. *Hint*: If you create the GUI version of the game, you might want to include a Start button that selects the random word and performs other startup tasks before you reveal the game interface. After the startup tasks are complete, you can remove the Start button from the form.