You will need to write your own class, Hand, which will contain member functions that manipulate the poker hand (check for pair, check for flush, deal hand, return cards to the end of each hand, etc.) Note that the private data members of the Hand class will contain the cards in the hand (i.e., an array of Card objects). This class should reside in its own source files, hand.h and hand.cpp. Hint: There is no need for a declaration of a Deck in the Hand class. However, a Deck object could be passed to a member function of the Hand class. Be sure to comment all functions in your code.

Each trial you run should gather statistics on 10,000 hands dealt and output in tabular format the following:

+   * trial number
* number of hands dealt
* number of hands with at least a pair
* number of hands with a flush
* percentage of hands with at least a pair (to two decimal places)
* percentage of hands with a flush (to two decimal places)

Your program should run a total of 10 trials and at the end of the 10 trials should output the average percentage of pairs and average percentage of flushes (to two decimal places).

Once again, don't worry if it's not completely clear to you how the Card and Deck classes work. You should not need to change them to make the program work. Note carefully that class declarations always end with a semicolon, but function definitions don't need them. The program that you create should make use of these predefined classes and each class should be contained within its own source code files. Don't forget to modularize your code and link together all cpp files.

Be sure to include a call (only once) to the randomize function:

```
srand((unsigned)time(NULL));
```

in main() to properly seed the random number generator used in the Deck::shuffle() member function. You will need to include both the stdlib.h and time.h header files.