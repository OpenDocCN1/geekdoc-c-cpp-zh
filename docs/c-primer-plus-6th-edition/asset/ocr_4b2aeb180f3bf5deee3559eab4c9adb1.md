```
cout << "It's been an excellent week for business.\\n"
      "Sales are up 120%% Expenses are down 35%%\n";

void comfort() {
  cout << "Your employees think you are the finest CEO\\n"
      "in the industry. The board of directors think\n"
      "you are the finest CEO in the industry.\n";
}
```

Here is a sample run of the executive menu program in Listing 6.10:

Please enter 1, 2, 3, 4, or 5:

+   1) alarm
2) report
3) alibi
4) comfort
5) quit

Your employees think you are the finest CEO
in the industry. The board of directors think
you are the finest CEO in the industry.

Please enter 1, 2, 3, 4, or 5:

+   1) alarm
2) report
3) alibi
4) comfort
5) quit

It's been an excellent week for business.
Sales are up 120%% Expenses are down 35%%.

Please enter 1, 2, 3, 4, or 5:

+   1) alarm
2) report
3) alibi
4) comfort
5) quit

That's not a choice.

Please enter 1, 2, 3, 4, or 5:

+   1) alarm
2) report
3) alibi
4) comfort
5) quit

Bye!

The loop terminates when the user enters 5. Entering 1 through 4 activates the corresponding choice from the switch list, and entering 6 triggers the default statements.

Note that input has to be an integer for the program to work correctly. If, for example, you enter a letter, the input statement will fail, and the loop will cycle endlessly until you kill the program. To deal with those who do not follow instructions, it's better to use character input.