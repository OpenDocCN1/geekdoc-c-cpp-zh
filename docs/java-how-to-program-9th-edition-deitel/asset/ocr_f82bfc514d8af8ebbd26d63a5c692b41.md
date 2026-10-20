# 14.12 (Temperature Conversion) Write a temperature-conversion application that converts from Fahrenheit to Celsius. The Fahrenheit temperature should be entered from the keyboard (via a JTextField). A JLabel should be used to display the converted temperature. Use the following formula for the conversion:

```
Celsius = 5/9 × ( Fahrenheit - 32 )
```

# 14.13 (Temperature-Conversion Modification) Enhance the temperature-conversion application of Exercise 14.12 by adding the Kelvin temperature scale. The application should also allow the user to make conversions between any two scales. Use the following formula for the conversion between Kelvin and Celsius (in addition to the formula in Exercise 14.12):

```
Kelvin = Celsius + 273.15
```

# 14.14 (Guess-the-Number Game) Write an application that plays “guess the number” as follows: Your application chooses the number to be guessed by selecting an integer at random in the range 1–1000. The application then displays the following in a label:

```
I have a number between 1 and 1000. Can you guess my number?
Please enter your first guess.
```

A JTextField should be used to input the guess. As each guess is input, the background color should change to either red or blue. Red indicates that the user is getting “warmer,” and blue, “colder.” A JLabel should display either "Too High" or "Too Low" to help the user zero in. When the user gets the correct answer, "Correct!" should be displayed, and the JTextField used for input should be changed to be uneditable. A JButton should be provided to allow the user to play the game again. When the JButton is clicked, a new random number should be generated and the input JTextField changed to be editable.

# 14.15 (Displaying Events) It’s often useful to display the events that occur during the execution of an application. This can help you understand when the events occur and how they’re generated. Write an application that enables the user to generate and process every event discussed in this chapter. The application should provide methods from the ActionListener, ItemListener, ListSelectionListener, MouseListener, MouseMotionListener and KeyListener interfaces to display messages when the events occur. Use method toString to convert the event objects received in each event handler into Strings that can be displayed. Method toString creates a String containing all the information in the event object.

# 14.16 (GUI-Based Craps Game) Modify the application of Section 6.10 to provide a GUI that enables the user to click a JButton to roll the dice. The application should also display four JLabels and four JTextFields, with one JLabel for each JTextField. The JTextFields should be used to display the values of each die and the sum of the dice after each roll. The point should be displayed in the fourth JTextField when the user does not win or lose on the first roll and should continue to be displayed until the game is lost.

# (Optional) GUI and Graphics Case Study Exercise: Expanding the Interface

# 14.17 (Interactive Drawing Application) In this exercise, you’ll implement a GUI application that uses the MyShape hierarchy from GUI and Graphics Case Study Exercise 10.2 to create an interactive drawing application. You’ll create two classes for the GUI and provide a test class that launches the application. The classes of the MyShape hierarchy require no additional changes.

The first class to create is a subclass of JPanel called DrawPanel, which represents the area on which the user draws the shapes. Class DrawPanel should have the following instance variables:

+   a) An array shapes of type MyShape that will store all the shapes the user draws.
+   b) An integer shapeCount that counts the number of shapes in the array.
+   c) An integer shapeType that determines the type of shape to draw.
+   d) A MyShape currentShape that represents the current shape the user is drawing.