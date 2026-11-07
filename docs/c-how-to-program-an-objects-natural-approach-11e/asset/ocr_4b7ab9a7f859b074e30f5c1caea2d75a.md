```
c) int sum(int n) {
       if (0 == n) {
           return 0;
       }
       else {
           return n + sum(n);
       }
   }
```

**5.35** *(Craps Game Modification)* Modify the craps program of Fig. 5.5 to allow wagering. Package as a function the portion of the program that runs one game of craps. Initialize variable bankBalance to 1000. Prompt the player to enter a wager. Use a while loop to check that wager is less than or equal to bankBalance and, if not, prompt the user to re-enter wager until a valid wager is entered. After a correct wager is entered, run one game of craps. If the player wins, increase bankBalance by wager and print the new bankBalance. If the player loses, decrease bankBalance by wager, print the new bankBalance, check on whether bankBalance has become zero and, if so, print the message "Sorry. You busted!" As the game progresses, print various messages to create some "chatter" such as "Oh, you're going for broke, huh?", "Aw c'mon, take a chance!" or "You're up big. Now's the time to cash in your chips!".

**5.36** *(Circle Area)* Write a C++ program that prompts the user for the radius of a circle, then calls inline function `circleArea` to calculate the area of that circle.

**5.37** *(Pass-by-Value vs. Pass-by-Reference)* Write a complete C++ program with the two alternate functions specified below, each of which simply triples the variable `count` defined in `main`. Then compare and contrast the two approaches. These two functions are

+   a) function `tripleByValue` that passes a copy of `count` by value, triples the copy and returns the new value and
+   b) function `tripleByReference` that passes `count` by reference via a reference parameter and triples the original value of `count` through its alias (i.e., the reference parameter).

**5.38** *(Unary Scope Resolution Operator)* What’s the purpose of the unary scope resolution operator?

**5.39** *(Function Template minimum)* Write a program that uses a function template called `minimum` to determine the smaller of two arguments. Test the program using integer, character and floating-point number arguments.

**5.40** *(Function Template maximum)* Write a program that uses a function template called `maximum` to determine the larger of two arguments. Test the program using integer, character and floating-point number arguments.

**5.41** *(Find the Error)* Determine whether the following program segments contain errors. For each error, explain how it can be corrected. [*Note:* For a particular program segment, it’s possible that no errors are present.]

```
a) template <typename A>
   int sum(int num1, int num2, int num3) {
       return num1 + num2 + num3;
   }
```