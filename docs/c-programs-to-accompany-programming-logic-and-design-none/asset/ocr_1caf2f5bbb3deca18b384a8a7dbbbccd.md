run correctly. The following code example illustrates how you can verify that a user enters correct numeric data:

```
```cpp
int answer;
const int MIN_NUM = 1;
const int MAX_NUM = 4;
cout << "Please enter a number in the range of " << MIN_NUM <<
        " to " << MAX_NUM << ": ";
cin >> answer;
while(answer < MIN_NUM || answer > MAX_NUM)
{
    cout << "Number must be between " << MIN_NUM << " and " <<
            MAX_NUM << ". Please try again: ";
    cin >> answer;
}
```
```

# EXERCISE 5-9: VALIDATING USER INPUT

In this exercise, you use what you have learned about validating user input to answer the following questions:

+   1. You plan to use the following statement in a C++ program to validate user input:
+   
+      ```cpp
+      while(inputString == "")
+      ```
+   
+      What would your user enter to cause this test to be `true`?
+   
+   2. You plan to use the following statement in a C++ program to validate user input:
+   
+      ```cpp
+      while(userAnswer == "Y" || userAnswer == "y")
+      ```
+   
+      What would a user enter to cause this test to be `true`?
+   
+   3. You plan to use the following statement in a C++ program to validate user input:
+   
+      ```cpp
+      while(userAnswer < 6 || userAnswer > 12)
+      ```
+   
+      What would a user enter to cause this test to be `true`?

# LAB 5-7: VALIDATING USER INPUT

In this lab, you make additions to a C++ program provided with the data files for this book. The program is a guessing game. A random number between 1 and 10 is generated in the program. The user enters a number between 1 and 10, trying to guess the correct number. If the user guesses correctly, the program congratulates the user, and then the loop that controls