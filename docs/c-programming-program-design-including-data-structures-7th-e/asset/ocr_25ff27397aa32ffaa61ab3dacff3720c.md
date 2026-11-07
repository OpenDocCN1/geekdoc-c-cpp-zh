+   j. Suppose str = "ABCD";. After the statement str[1] = 'a';, the value
+   of str is "aBCD". (11)

+   k. Suppose str = "abcd". After the statement:
+   str = str + "ABCD";
+   the value of str is "ABCD". (11)

+   2. Write C++ statements that do the following: (1, 2, 3, 4, 5)
+   
+      a. Define an enum type, birdType, with the values PEACOCK, SPARROW,
+         CANARY, PARROT, PENGUIN, OSTRICH, EAGLE, CARDINAL, and
+         HUMMINGBIRD.
+      b. Declare a variable bird of the type birdType.
+      c. Assign CANARY to the variable bird.
+      d. Advance bird to the next value in the list.
+      e. Decrement bird to the previous value in the list.
+      f. Output the value of the variable bird.
+      g. Input value in the variable bird.

+   3. Given:
+   
+      ```
+      enum currencyType {DOLLAR, POUND, FRANK, LIRA, MARK};
+      currencyType currency;
+      ```
+   
+      which of the following statements are valid? (1, 2, 3, 4, 5)
+   
+      a. currency = DOLLAR;
+      b. cin >> currency;
+      c. currency = static_cast<currencyType>(currency + 1);
+      d. for (currency = DOLLAR; currency <= MARK; currency++)
+           cout << "*";

+   4. Consider the following declaration:
+   
+      ```
+      enum fruitType {ORANGE, APPLE, BANANA, GRAPE, STRAWBERRY, MANGO, GUAVA,
+           PINEAPPLE, KIWI};
+      fruitType fruit;
+      ```
+   
+      Answer the following questions. (1, 2, 3, 5)
+   
+      a. What is the value of static_cast<int>(STRAWBERRY)?
+      b. What is the value, if any, of the following expression?
+         static_cast<fruitType>(static_cast<int>(MANGO) - 2)
+      c. What is the value, if any, of the following expression?
+         static_cast<fruitType>(static_cast<int>(GRAPE) + 2)
+      d. What is the value, if any, of the expression: BANANA <= KIWI
+      e. What is the output, if any, of the following code?
+   
+         ```
+         for (fruit = BANANA; fruit < PINEAPPLE; fruit++)
+             cout << static_cast<int>(fruit) << ", ";
+         cout << endl;
+         ```