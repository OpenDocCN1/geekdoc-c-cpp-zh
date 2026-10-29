In reviewing Program 4.6, notice the break statement in the last case statement. Although it's not necessary, terminating the last case in a switch statement with a break is a good programming practice. It prevents a possible program error later if another case statement is added to the switch statement. With the addition of a new case, the break keyword between cases ensures that you won't forget to include the break at the time of the modification.

Because character data types are always converted to integers in an expression, a switch statement can also be used to "switch" based on the value of a character expression. For example, assuming choice is a character variable, the following switch statement is valid:

```
switch(choice)
{
    case 'a': case 'e': case 'i': case 'o': case 'u':
        cout << "The character in choice is a vowel\n";
        break;
    default:
        cout << "The character in choice is not a vowel\n";
        break;    // this break is optional
}    // end of switch statement
```

# EXERCISES 4.4

+   1. (Modify) Rewrite the following if-else chain by using a switch statement:
+       if (letterGrade == 'A')
+           cout << "The numerical grade is between 90 and 100\n";
+       else if (letterGrade == 'B')
+           cout << "The numerical grade is between 80 and 89.9\n";
+       else if (letterGrade == 'C')
+           cout << "The numerical grade is between 70 and 79.9\n";
+       else if (letterGrade == 'D')
+           cout << "How are you going to explain this one?\n";
+       else
+       {
+           cout << "Of course I had nothing to do with my grade.\n";
+           cout << "It must have been the professor's fault.\n";
+       }

+   2. (Modify) Rewrite the following if-else chain by using a switch statement:
+       if (bondType == 1)
+       {
+           inData();
+           check();
+       }
+       else if (bondType == 2)