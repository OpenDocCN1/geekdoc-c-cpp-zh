# Programming Projects

# 611

![](bbox=[0.237, 0.105, 0.762, 0.345])

The DFA works by starting in the oval labeled IsMoney. This is the initial state. If the first character of the string is $, then we advance to the second character and move to state 0. Otherwise we conclude the string is not a proper money. In state 0, if the second character is a digit between 1 and 9, then we advance to the third character and move to state 1. Otherwise we conclude the string is not a proper amount. In state 1, if we have no characters left in the string, then we conclude that the string is a money amount. This is called a final state and is indicated by a bold oval. If the third character is a digit between 0 and 9, then we advance to the fourth character and move to state 2. Otherwise if the third character is a comma then we advance to the fourth character and move to state 4. Otherwise we conclude the string is not a proper amount. The rest of the DFA behaves in a similar manner.

Write a program that uses recursion to implement the DFA. Your program should have a separate function for each state in the DFA. Each function should invoke the function corresponding to the next state indicated by the arrows in the diagram. Mutual recursion is because of the loop from state 7 to state 4. Test your solution with several strings and output whether each string is a properly formatted money amount.

This solution calls a function for every character in the string. The solution may be written in a tail-recursive manner, so it is possible that long strings will not exhaust the stack if your compiler is efficient.

+   13. A popular word game involves finding words from a grid of randomly generated letters. Words must be at least three letters long and formed from adjoining letters. Letters may not be reused and it is valid to move across diagonals. As an example, consider the following 4×4 grid of letters.