![](bbox=[0.22, 0.08, 0.88, 0.68])

Fig. 4.8 | switch multiple-selection statement with breaks.

# Ignoring Newline, Tab and Blank Characters in Input

In the switch statement of Fig. 4.7, the lines

```
```c
case '\n': // ignore newlines,
case '\t': // tabs,
case ' ': // and spaces in input
break;
```
```

cause the program to skip newline, tab and blank characters. Reading characters one at a time can cause problems. To have the program read the characters, you must send them to the computer by pressing Enter. This causes the newline character to be placed in the input after the character we wish to process. Often, this newline must be specifically ignored to make the program work correctly. The preceding cases in our switch statement prevent the error message in the default case from being printed each time a newline, tab or space is encountered in the input. So each input causes two iterations of the loop—the first for the letter grade and the second for '\n'. Listing several case labels together (such as case 'D'; case 'd' : in Fig. 4.7) simply means that the same set of actions is to occur for each of the cases.

# Error-Prevention Tip 4.7

Remember to provide processing capabilities for newline (and possibly other white-space) characters in the input when processing characters one at a time.