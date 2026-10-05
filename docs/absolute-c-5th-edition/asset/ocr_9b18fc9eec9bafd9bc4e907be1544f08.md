# CHAPTER 9 Strings

Display 9.5 Program Using the Class string (part 2 of 2)

```
return 0;
}
//Uses iostream:
void newline() {
    char nextChar;
    do {
        cin.get(nextChar);
    } while (nextChar != '\n');
}
```

Sample Dialogue
Enter your first and last names:
B'Elanna Torres
Your name in our records is: Torres, B'Elanna
Our motto is
Your records are our records.
Please suggest a better (one-line) motto:
Our records go where no records dared to go before.
Our new motto will be:
Our records go where no records dared to go before.

# Self-Test Exercises

+   22. Consider the following code (and assume that it is embedded in a complete and correct program and then run):
string s1, s2;
cout << "Enter a line of input:\n";ncout >> s1 >> s2;
cout << s1 << " " << << s2 << "<END OF OUTPUT";
If the dialogue begins as follows, what will be the next line of output:
A string is a joy forever!

+   23. Consider the following code (and assume that it is embedded in a complete and correct program and then run):
string s;
cout << "Enter a line of input:\n";ngetline(cin, s);
cout << s << "<END OF OUTPUT";