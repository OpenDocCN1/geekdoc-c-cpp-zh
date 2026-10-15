PP 8.7 The programming projects of Chapter 4 discussed a Card class that represents a standard playing card. Create a class called DeckOfCards that stores 52 objects of the Card class. Include methods to shuffle the deck, deal a card, and report the number of cards left in the deck. The shuffle method should assume a full deck. Create a driver class with a main method that deals each card from a shuffled deck, printing each card as it is dealt.

PP 8.8 Design and implement an application that reads a sequence of up to 25 pairs of names and postal (ZIP) codes for individuals. Store the data in an object designed to store a first name (string), last name (string), and postal code (integer). Assume each line of input will contain two strings followed by an integer value, each separated by a tab character. Then, after the input has been read in, print the list in an appropriate format to the screen.

PP 8.9 Modify the program you created in PP 8.8 to accomplish the following:

+   - Support the storing of additional user information: street address (string), city (string), state (string), and 10 digit phone number (long integer, contains area code and does not include special characters such as '(' , ')' , or '-')
+   - Store the data in an ArrayList object.

PP 8.10 Use the Question class from Chapter 7 to define a Quiz class. A quiz can be composed of up to 25 questions. Define the add method of the Quiz class to add a question to a quiz. Define the giveQuiz method of the Quiz class to present each question in turn to the user, accept an answer for each one, and keep track of the results. Define a class called QuizTime with a main method that populates a quiz, presents it, and prints the final results.

PP 8.11 Modify your answer to PP 8.10 so that the complexity level of the questions given in the quiz is taken into account. Overload the giveQuiz method so that it accepts two integer parameters that specify the minimum and maximum complexity levels for the quiz questions and presents only questions in that complexity range. Modify the main method to demonstrate this feature.

PP 8.12 Design a class that represents a star with a specified radius and color. Use a filled polygon to draw the star. Design and implement a program that draws 10 stars of random radius in random locations.