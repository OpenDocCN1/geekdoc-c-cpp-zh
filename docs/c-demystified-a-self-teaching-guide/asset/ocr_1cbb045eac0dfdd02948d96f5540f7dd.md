```
if (choice == 'Y')
    citizen = true;
else
    citizen = false;
    if (age >= 18 && citizen == true)
        cout << "You are eligible to vote";
else
        cout << "You are not eligible to vote";
return 0;
```

The following are several sample runs, separated by ===:

Enter your age: 18
Are you a citizen (Y/N): Y
You are eligible to vote
===
Enter your age: 18
Are you a citizen (Y/N): N
You are not eligible to vote
--===
Enter your age: 17
Are you a citizen (Y/N): Y
You are not eligible to vote
--===
Enter your age: 17
Are you a citizen (Y/N): N
You are not eligible to vote

The part of the program that uses the logical And operator is

```
if (age >= 18 && citizen == true)
    cout << "You are eligible to vote";
else
    cout << "You are not eligible to vote";
```

The comparison age >=18 is referred to as the left part of the expression since it is to the left of the Logical Operator. Similarly, the comparison citizen == true is referred to as the right part of the expression because it is to the right of the Logical Operator.

If the user's age is at least 18 years, the program makes the second comparison, whether the user is a citizen. If the user's age is not at 18 years of age, the second comparison is not made before the first expression is executed. The reason is to avoid waiting CPU time; if the left expression is false, the overall expression is false regardless of the result of the evaluation of the right expression.

Because the second comparison of whether the user is a citizen is made only if the user's age is at least 18, the flowchart in Figure 6-1 of this program using nested statements also applies to this program using the logical operator.

# The || Operator

The || operator is also known as the logical OR operator. Like the Logical operator, the Logical OR operator is also a binary operator, taking two Boolean expressions as operands. It returns true if either expression is true. It returns false if both expressions are false. Of course, if both expressions are true, the overall expression is true. Table 6-3 illustrates this.