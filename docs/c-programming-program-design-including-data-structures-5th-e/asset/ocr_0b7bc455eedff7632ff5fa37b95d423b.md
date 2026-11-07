+   j. Suppose `str = "ABCD"`. After the statement `str[1] = 'a';`, the value of `str` is `"ABCD"`.
+   
+   k. Suppose `str = "abcd"`. After the statement:
+   
+   ```cpp
+   str = str + "ABCD";
+   ```
+   
+   the value of `str` is `"ABCD"`.

+   2. Write C++ statements that do the following:
+   
+      a. Define an `enum` type, `bookType`, with the values `MATH`, `CSC`, `ENGLISH`, `HISTORY`, `PHYSICS`, and `PHILOSOPHY`.
+      
+      b. Declare a variable `book` of type `bookType`.
+      
+      c. Assign `MATH` to the variable `book`.
+      
+      d. Advance `book` to the next value in the list.
+      
+      e. Output the value of the variable `book`.

3. Given:

```
enum currencyType {DOLLAR, POUND, FRANK, LIRA, MARK};
currencyType currency;
```

which of the following statements are valid?

+   a. `currency = DOLLAR;`
+   
+   b. `cin >> currency;`
+   
+   c. `currency = static_cast<currencyType>(currency + 1);`
+   
+   d.
+   ```cpp
+   for (currency = DOLLAR; currency <= MARK; currency++)
+       cout << "*";
+   ```

4. Given:

```
enum cropType {WHEAT, CORN, RYE, BARLEY, OATS};
cropType crop;
```

circle the correct answer.

+   a. `static_cast<int>(WHEAT) is 0`
+      (i) true    (ii) false
+   
+   b. `static_cast<cropType>(static_cast<int>(WHEAT) − 1) is WHEAT`
+      (i) true    (ii) false
+   
+   c. `RYE > WHEAT`
+      (i) true    (ii) false
+   
+   d.
+   ```cpp
+   for (crop = wheat; crop <= oats; ++crop)
+       cout << "*";
+   cout << endl;
+   ```
+   outputs: `*****`
+      (i) true    (ii) false