
## Programming Projects

**EX 8.11** Describe a program for which you would use the ArrayList class instead of arrays. Describe a program for which you would use arrays instead of the ArrayList class. Explain your choices.

**EX 8.12** What would happen if, in the Dots program, we did not provide empty definitions for one or more of the unused mouse events?

**EX 8.13** The Dots program listens for a mouse pressed event to draw a dot. How would the program behave differently if it listened for a mouse released event instead? A mouse clicked event?

**EX 8.14** What would happen if the call to super.paintComponent were removed from the paintComponent method of the DotsPanel1 class? Remove it and run the program to test your answer.

**EX 8.15** What would happen if the call to super.paintComponent were removed from the paintComponent method of the RubberLinesPanel1 class? Remove it and run the program to test your answer. In what ways is the answer different from the answer to Exercise 8.13?

**EX 8.16** Create a UML class diagram for the Direction program.

## Programming Projects

Visit www.myprogramminglab.com to complete many of these Programming Projects online and get instant feedback.

**PP 8.1** Design and implement an application that reads an arbitrary number of integers that are in the range 0 to 50 inclusive and counts how many occurrences of each are entered. After all input has been processed, print all of the values (with the number of occurrences) that were entered one or more times.

**PP 8.2** Modify the program from PP 8.1 so that it works for numbers in the range between -25 and 25.

**PP 8.3** Design and implement an application that creates a histogram that allows you to visually inspect the frequency distribution of a set of values. The program should read in an arbitrary number of integers that are in the range 1 to 100 inclusive; then produce a chart similar to the one below that indicates how many input values fell in the range 1 to 10, 11 to 20, and so on. Print one asterisk for each value entered.

| 1 - 10 | ***** |
| 11 - 20 | ** |
| 21 - 30 | ************************ |
| 31 - 40 |  |
| 41 - 50 | *** |
| 51 - 60 | ******** |
| 61 - 70 | ** |
| 71 - 80 | ***** |
| 81 - 90 | ******* |
| 91 - 100 | ********* |

**PP 8.4** The lines in the histogram in PP 8.3 will be too long if a large number of values is entered. Modify the program so that it prints an asterisk for every five values in each category. Ignore leftovers. For example, if a category had 17 values, print three asterisks in that row. If a category had 4 values, do not print any asterisks in that row.

**PP 8.5** Design and implement an application that computes and prints the mean and standard deviation of a list of integers x1 through xn. Assume that there will be no more than 50 input values. Compute both the mean and standard deviation as floating point values, using the following formulas.

mean = (∑ᵢ₌₁ⁿ Xᵢ) / n

sd = √[∑ᵢ₌₁ⁿ (Xᵢ − mean)²]

**PP 8.6** The L&L Bank can handle up to 30 customers who have savings accounts. Design and implement a program that manages the accounts. Keep track of key information and allow each customer to make deposits and withdrawals. Produce appropriate error messages for invalid transactions. Hint: you may want to base your accounts on the Account class from Chapter 4. Also provide a method to add 3 percent interest to all accounts whenever the method is invoked.

VideoNote
Developing a solution of PP 8.5.

**PP 8.7** The programming projects of Chapter 4 discussed a Card class that represents a standard playing card. Create a class called DeckOfCards that stores 52 objects of the Card class. Include methods to shuffle the deck, deal a card, and report the number of cards left in the deck. The shuffle method should assume a full deck. Create a driver class with a main method that deals each card from a shuffled deck, printing each card as it is dealt.

**PP 8.8** Design and implement an application that reads a sequence of up to 25 pairs of names and postal (ZIP) codes for individuals. Store the data in an object designed to store a first name (string), last name (string), and postal code (integer). Assume each line of input will contain two strings followed by an integer value, each separated by a tab character. Then, after the input has been read in, print the list in an appropriate format to the screen.

**PP 8.9** Modify the program you created in PP 8.8 to accomplish the following:

- Support the storing of additional user information: street address (string), city (string), state (string), and 10 digit phone number (long integer, contains area code and does not include special characters such as '(' , ')' , or '-')
- Store the data in an ArrayList object.

**PP 8.10** Use the Question class from Chapter 7 to define a Quiz class. A quiz can be composed of up to 25 questions. Define the add method of the Quiz class to add a question to a quiz. Define the giveQuiz method of the Quiz class to present each question in turn to the user, accept an answer for each one, and keep track of the results. Define a class called QuizTime with a main method that populates a quiz, presents it, and prints the final results.

**PP 8.11** Modify your answer to PP 8.10 so that the complexity level of the questions given in the quiz is taken into account. Overload the giveQuiz method so that it accepts two integer parameters that specify the minimum and maximum complexity levels for the quiz questions and presents only questions in that complexity range. Modify the main method to demonstrate this feature.

**PP 8.12** Design a class that represents a star with a specified radius and color. Use a filled polygon to draw the star. Design and implement a program that draws 10 stars of random radius in random locations.

**PP 8.13** Design a class that represents the visual representation of a car. Use polylines and polygons to draw the car in any graphics context and at any location. Create a main driver to display the car.

**PP 8.14** Modify the solution to PP 8.13 so that it uses the Polygon class to represent all polygons used in the drawing.

**PP 8.15** Modify the QuoteOptions program from Chapter 5 so that it provides three additional quote options. Use an array to store all of the quote strings.

**PP 8.16** Design and implement a program that draws 20 circles, with the radius and location of each circle determined at random. If a circle does not overlap any other circle, draw that circle in black. If a circle overlaps one or more other circles, draw it in cyan. Use an array to store a representation of each circle, then determine the color of each circle. Two circles overlap if the distance between their center points is less than the sum of their radii.

**PP 8.17** Design and implement a program that draws a checkerboard with five red and eight black checkers on it in various locations. Store the checkerboard as a two-dimensional array.

**PP 8.18** Modify the program from PP 8.17 so that the program determines whether any black checkers can jump any red checkers. Under the checkerboard, print (using drawString) the row and column position of all black checkers that have possible jumps.

**PP 8.19** Modify the RubberLines program from this chapter so that it shows all of the lines drawn. Show only the final lines (from initial mouse press to mouse release), not the intermediate lines drawn to show the rubberbanding effect. Hint: Keep track of a list of objects that represent the lines similar to how the Dots program kept track of multiple dots.

**PP 8.20** Design and implement a program that counts the number of times the mouse has been clicked. Display that number in the center of the applet window.

**PP 8.21** Design and implement an application that creates a polyline shape dynamically using mouse clicks. Each mouse click adds a new line segment from the previous point. Include a button below the drawing area to clear the current polyline and begin another.

**PP 8.22** Design and implement an application that draws a circle using a rubberbanding technique. The circle size is determined by a mouse drag. Use the original mouse click location as a fixed
