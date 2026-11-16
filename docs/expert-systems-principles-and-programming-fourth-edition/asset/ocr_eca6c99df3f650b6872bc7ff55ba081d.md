9.1 Modify the Sticks program in Chapter 8 so the control rules are separated from the rules of playing the game. Use salience to give the control rules lower priority.

9.2 Add a rule to the Blocks World program in Section 7.23 that would remove a move goal if it has already been satisfied.

9.3 Create rules for implementing the decision procedure for determining whether a syllogism is valid. Test your program on the syllogism from Problem 8.24 on page 492.

9.4 Write a program to determine the prime factors of a number. For example, the prime factors of 15 are 3 and 5.

9.5 Given the following distances between cities in Texas, solve the Traveling Salesman problem (page 52 in Section 1.13) for the cities. Write a program that finds the shortest route that visits all the cities. The input to the program should be the starting city and the list of cities to be visited. To test your program, determine the shortest route, beginning in Houston.

| | Houston | Dallas | Austin | Abilene | Waco |
|---|---|---|---|---|---|
| Houston | — | 241 | 162 | 351 | 183 |
| Dallas | 241 | — | 202 | 186 | 97 |
| Austin | 162 | 202 | — | 216 | 106 |
| Abilene | 351 | 186 | 216 | — | 186 |
| Waco | 183 | 97 | 106 | 186 | — |

9.6 Given the following information, write a program that will ask for the type of clouds visible and the wind direction, and then give a forecast for the chances of rain. Cumulus clouds indicate good weather, but they may change to nimbostratus clouds if the wind blows from the northeast to the south. Cirrocumulus clouds indicate rain within a day if the wind direction is northeast to south. If the wind blows north to west, then overcast skies are predicted. Stratocumulus clouds may change to cumulonimbus clouds if the wind direction is northeast to south. Stratus clouds indicate light drizzle. If the wind blows from the north to the west, stratus clouds may change to nimbostratus clouds and rain within a short time if wind direction is southwest to north. A long rain is indicated if the wind blows from the northeast to the south. Cumulonimbus clouds indicate showers if they are visible before noon. Cirrocumulus clouds indicate rain within 15 to 24 hours if the wind direction is northeast to south. Altostratus clouds indicate rain within a day if winds are northeast to south, otherwise the skies will be overcast. Altocumulus clouds indicate rain within 15 to 20 hours if winds are from northeast to south.

9.7 Write a program to convert a Morse code message to its equivalent series of alphabetic characters. The following is an example of input and output to the program (where the * - and . are dots and dashes and the character / is used to delimit the Morse code characters):

```
Enter a message (<CR to end): * * * / - - - /
* * *.J
```