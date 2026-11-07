As noted earlier, this program needs the break statements to confine execution to a particular portion of a switch statement. To see that this is so, you can remove the break statements from Listing 6.10 and see how it works afterward. You’ll find, for example, that entering 2 causes the program to execute all the statements associated with case labels 2, 3, 4, and the default. C++ works this way because that sort of behavior can be useful. For one thing, it makes it simple to use multiple labels. For example, suppose you write Listing 6.10 using characters instead of integers as menu choices and switch labels. In that case, you could use both an uppercase and a lowercase label for the same statements:

```
```cpp
char choice;
cin >> choice;
while (choice != 'Q' && choice != 'q')
{
    switch(choice)
    {
        case 'a':
        case 'A': cout << "*\a\n";
                  break;

        case 'r':
        case 'R': report();
                  break;

        case 'l':
        case 'L': cout << "The boss was in all day.\n";
                  break;

        case 'c':
        case 'C': comfort();
                  break;
        default : cout << "That's not a choice.\n";
    }
    showmenu();
    cin >> choice;
}
```
```

Because there is no break immediately following case 'a', program execution passes on to the next line, which is the statement following case 'A'.

# Using Enumerators as Labels

Listing 6.11 illustrates using enum to define a set of related constants and then using the constants in a switch statement. In general, cin doesn’t recognize enumerated types (it can’t know how you will define them), so the program reads the choice as an int. When the switch statement compares the int value to an enumerator case label, it promotes the enumerator to int. Also the enumerators are promoted to type int in the while loop test condition.