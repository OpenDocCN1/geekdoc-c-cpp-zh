```
12      // print all 52 Cards in the order in which they are dealt
13      for ( int i = 1; i <= 52; i++ )
14      {
15          // deal and display a Card
16          System.out.printf( "%-19s", myDeckOfCards.dealCard() );
17
18          if ( i % 4 == 0 ) // output a newline after every fourth card
19              System.out.println();
20      } // end for
21      } // end main
22  } // end class DeckOfCardsTest
```

| Six of Spades | Eight of Spades | Six of Clubs | Nine of Hearts |
| Queen of Hearts | Seven of Clubs | Nine of Spades | King of Hearts |
| Three of Diamonds | Deuce of Clubs | Ace of Hearts | Ten of Spades |
| Four of Spades | Ace of Clubs | Seven of Diamonds | Four of Hearts |
| Three of Clubs | Deuce of Hearts | Five of Spades | Jack of Diamonds |
| King of Clubs | Ten of Hearts | Three of Hearts | Six of Diamonds |
| Queen of Clubs | Eight of Diamonds | Deuce of Diamonds | Ten of Diamonds |
| Three of Spades | King of Diamonds | Nine of Clubs | Six of Hearts |
| Ace of Spades | Four of Diamonds | Seven of Hearts | Eight of Clubs |
| Deuce of Spades | Eight of Hearts | Five of Hearts | Queen of Spades |
| Jack of Hearts | Seven of Spades | Four of Clubs | Nine of Diamonds |
| Ace of Diamonds | Queen of Diamonds | Five of Clubs | King of Spades |
| Five of Diamonds | Ten of Clubs | Jack of Spades | Jack of Clubs |

Fig. 7.11 | Card shuffling and dealing. (Part 2 of 2.)

# 7.6 Enhanced for Statement

The enhanced for statement iterates through the elements of an array without using a counter, thus avoiding the possibility of “stepping outside” the array. We show how to use the enhanced for statement with the Java API’s prebuilt data structures (called collections) in Section 7.14. The syntax of an enhanced for statement is:

```
for ( parameter : arrayName )
    statement
```

where parameter has a type and an identifier (e.g., int number), and arrayName is the array through which to iterate. The type of the parameter must be consistent with the type of the elements in the array. As the next example illustrates, the identifier represents successive element values in the array on successive iterations of the loop.

Figure 7.12 uses the enhanced for statement (lines 12–13) to sum the integers in an array of student grades. The enhanced for’s parameter is of type int, because array contains int values—the loop selects one int value from the array during each iteration. The enhanced for statement iterates through successive values in the array one by one. The statement’s header can be read as “for each iteration, assign the next element of array to int variable number, then execute the following statement.” Thus, for each iteration, identifier number represents an int value in array. Lines 12–13 are equivalent to the following counter-controlled repetition used in lines 12–13 of Fig. 7.5 to total the integers in array, except that counter cannot be accessed in the enhanced for statement:

```
for ( int counter = 0; counter < array.length; counter++ )
    total += array[ counter ];
```