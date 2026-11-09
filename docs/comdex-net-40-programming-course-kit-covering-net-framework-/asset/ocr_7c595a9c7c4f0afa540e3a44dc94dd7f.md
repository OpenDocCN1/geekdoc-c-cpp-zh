```
```csharp
case 'E':
    Console.WriteLine("The entered vowel is: E");
    break;
case 'I':
    Console.WriteLine("The entered vowel is: I");
    break;
case 'O':
    Console.WriteLine("The entered vowel is: O");
    break;
case 'U':
    Console.WriteLine("The entered vowel is: U");
    break;
default:
    Console.WriteLine("The entered character is not a vowel!");
    break;
}
Console.ReadLine();
}
}
}
```
```

In the highlighted code of Listing 1.6, we first prompt a user to enter a vowel. Then, we store the entered vowel in the char type variable, myChar. Next, we convert the entered character into its uppercase version and store the uppercase version in another char type variable, x. After this, we use a switch statement to check which of the vowels in the English alphabet was entered by the user. The value of x is checked against each of the case labels of the case statements. When the control reaches the first case statement, it is checked if x is equal to A. If x is not equal to A, the control passes to the next case statement and checks if x is equal to E. If x is not equal to E, control passes to the next case statement, where it is checked if x is equal to I. If x is not equal to I, control passes to the next case statement, where it is checked if x is equal to O. If x is not equal to O, control passes to the next case statement, where it is checked if x is equal to U.

If there is a match with any of these case statements, the Console.WriteLine() method inside that case statement is called and the break statement is executed. However, if there is no match with any of the case statements, then the default statement is executed. Note that when the break statement is executed, the control breaks out of the switch statement and executes the statement (if any) that follows the switch statement.

+   8. Press the F5 key on the keyboard to run the application. The output of the application appears, prompting you to enter a vowel (Fig.C#-1.21).
+   9. Type i (or I) on the console and press the ENTER key. A message is displayed on the console, indicating that the entered vowel is I (Fig.C#-1.21).
+   10. Close the console displaying the output.
+   11. Press the F5 key on the keyboard to run the application again. The output of the application appears, prompting you to enter a vowel (Fig.C#-1.22).
+   12. Type y on the console and press the ENTER key. A message is displayed on the console, indicating that the entered character is not a vowel (Fig.C#-1.22).

![](bbox=[0.307, 0.726, 0.494, 0.815])

![](bbox=[0.521, 0.726, 0.715, 0.815])

You might have noticed in the previous example that a break statement is used in the case and default statements. The break statement prevents fall through of the case statements. Fall through refers to a