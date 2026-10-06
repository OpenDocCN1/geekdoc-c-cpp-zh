
- 10. Correctly overloaded methods must have the same ________.
- a. return type c. parameter list
- b. identifier d. All of the above.

- 11. Methods are ambiguous when they ________.
- a. are overloaded
- b. are written in a confusing manner
- c. are indistinguishable to the compiler
- d. have the same parameter type as their return type

- 12. Which of the following pairs of method declarations correctly overloaded methods?
- a. private static void MethodA(int a)
  private static void MethodA(int b, double c)
- b. private static void MethodB(double d)
  private static void MethodB()
- c. private static double MethodC(int e)
  private static double MethodD(int f)
- d. Two of these are correctly overloaded methods.

- 13. Which of the following pairs of method declarations represent correctly overloaded methods?
- a. private static void Method(int a)
  private static void Method(int b)
- b. private static void Method(double d)
  private static int Method()
- c. private static double Method(int e)
  private static int Method(int f)
- d. Two of these are correctly overloaded methods.

- 14. The process of determining which overloaded version of a method to execute is overload
- a. confusion c. revolution
- b. infusion d. resolution

- 15. When one of a method's parameters is optional, it means that ________
- a. no arguments are required in a call to the method
- b. a default value will be assigned to the parameter if no argument is sent for it
- c. a default value will override any argument value sent to it
- d. you are not required to use the parameter within the method body

- 16. Which of the following is an illegal method declaration?
- a. private static void createState(int acctNum, double balance = 0.0)
- b. private static void createStatement(int acctNum = 0, double balance)
- c. private static void createState(int acctNum = 0, double balance = 0)
- d. All of these are legal.

- 17. Assume you have declared a method as follows:
  private static double ComputeBill(int acct, double price, double discount = 0)
  Which of the following is a legal method call?
- a. ComputeBill();
- b. ComputeBill(1001);
- c. ComputeBill(1001, 200.00);
- d. None of the above is legal.

- 18. Assume you have declared a method as follows:
  private static double CalculateDiscount(int acct = 0, double price = 0, double discount = 0)
  Which of the following is a legal method call?
- a. CalculateDiscount();
- b. CalculatedDiscount(200.00);
- c. CalculatedDiscount(3000.0, 0.02);
- d. None of the above is legal.

- 19. Assume you have declared a method as follows:
  private static double DisplayData(string name = "XX", double amount = -10.0)
  Which of the following is an illegal method call?
- a. DisplayData(name : "Albert");
- b. DisplayData(amount : 200, name : "Albert");
- c. DisplayData(amount : 900.0);
- d. All of these are legal.

# Exercises

## Programming Exercises

- 20. Suppose that you have declared an integer named scores, and you make the following method call:
  TotalScores(scores, num : 1);
  Of the overloaded method definitions, which would execute?
- a. private static void TotalScores(int[] scores)
- b. private static void TotalScores(int[] scores, int num)
- c. private static void TotalScores(int[] scores, int num = 10, int code = 10)
- d. The program would not compile.

- a. Create a program named Reverse3 whose Main() method declares three integers firstInt, middleInt, and lastInt. Assign values to the variables, display them, and then pass them to a method that accepts them as reference variables, place the first value in the lastInt variable, and place the last value in the firstInt variable. In the Main() method, display the three variables again, demonstrating that their positions have been reversed.

- b. Create a program named Reverse4, which contains a method that reverses the positions of four values. Write a Main() method that demonstrates the method works correctly.

- 2. Create a program named IntegerFacts whose Main() method declares an array of 10 integers. Call a method to interact fill the array with any number of values up to 10 until a sentinel value is entered. If an entry is not an integer, prompt the user. Call a second method that outputs parameters for the highest value in the array, lowest value in the array, sum of the values in the array, and arithmetic mean. In the Main() method, display all statistics.

- 3. Create a program for Smalltown Regional Airport Flights that accepts either an integer number or string code from the options in Figure 8-33. Pass the user's entry to one of two overloaded GetFlightInfo() methods, and then display a returned string with all the flight details. The method version that accepts an integer looks up the airport code, name, and time of flight; the version that accepts a string description looks up the flight, airport name, and time. The methods returns an appropriate message if the flight is not found.

| Flight number | Airport code | Airport name | Time |
| :--- | :--- | :--- | :--- |
| 201 | AUS | Austin | 0710 |
| 321 | CRP | Corpus Christi | 0830 |
| 510 | DFW | Dallas Fort Worth | 0915 |
| 633 | HOU | Houston | 1140 |

Figure 8-33 Flight information for Smalltown Regional Airport

- 4. Create a program named Auction that allows a user to enter an amount bid on an online auction item. Include three overloaded methods that accept an int, double, and string bid. Each method should display the bid and indicate whether is over the minimum acceptable bid of $10. If the bid is a string, accept it only if it is numeric prefixed with a dollar sign, or it is numeric and followed by the word dollars. Otherwise, display a message that indicates the format is incorrect.

- 5. Create a program named TipCalculation that includes two overloaded methods—one that accepts a price as double (for example, 30.00 and 0.20, where 0.20 represents a 20 percent tip), and one that accepts a price as a double and a tip as an integer (for example, 30.00 and 5, where 5 represents a $5 tip). Each method should display the price, the tip as a percentage of the price, the tip in dollars, and the total of the plus tip. Include a Main() method that demonstrates each method.

- 6. Write a program named InputMethodDemo2 that eliminates the repetitive code in the InputMethod() in the InputMethodDemo program in Figure 8-5. Rewrite the program so the InputMethod() contains only two statements:
  one = DataEntry("first");
  two = DataEntry("second");

- 7. Write a program named Averages that includes a method that accepts any number of numeric parameters, displays them, and displays their average. Demonstrate that the method works correctly when passed once, two, three numbers, or an array of numbers.

- 8. Write a program named SortWords that includes a method that accepts any number of words and sorts them in alphabetical order. Demonstrate that the method works correctly when called with one, two, five, and ten words.

- 9. Write a program named Movie that contains a method that accepts two parameters: a string name of movie and an integer running time in minutes. Provide a default value for movie so if you call the method without an argument, minutes is set to 90. Write a Main() method that proves you can call the method with only string argument as well as a string and integer.

- 10. In the card game War, a deck of cards is divided between two players, one of which is the computer. Reveal one card for the computer and one card for the player at a time. Award two points for the player whose card has the higher value. (For this game, the king is the highest card, followed by the queen and jack, then the numbers 10 to 2, and finally the ace.) If the computer and player expose cards with equal values in turn, award one point to each. At the end of the game, all 52 cards have been played only once, and the sum of the player's and computer score will be 52.
- Use an array of 52 integers to store unique values for each card. Write a method F11Deck() that places 52 unique values into this array. Another method named SelectCard() that you call twice on each deal to select a unique card for each player, with no repetition of cards in 26 deals. (To pause the play between each deal hand, use a call to ReadLine()).

| Deal # | Computer | Player | Score |
| :--- | :--- | :--- | :--- |
| 1 | King of diamonds | 5 of spades | Computer: 2, Player: 0 |
| 2 | 7 of diamonds | 4 of hearts | Computer: 4, Player: 0 |
| 3 | 5 of diamonds | 6 of spades | Computer: 4, Player: 0 |

The first part of Figure 8-34 shows the start of a typical program execution. (Caution: This is a difficult exercise!)

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_374_0.png)

Figure 8-34 Start of typical execution of console-based and GUI WarCardGame programs
