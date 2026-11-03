```
• puts(“This is the most common choice: “);
• break;
• case ‘3’:

• puts(“I question your judgement.”);
• break;
• default:

• puts(“That’s not a valid choice.”); 23 }
24
25 return(0);
26 }
27
28
```

The bulk of this code is a structure. It starts with a *switch* at line 10. This is followed by a series of *case* statements, each of which has its own statements. The final piece is the default. It is followed by its own statements as well, and then a closing curly bracket. These are the elements of the structure.

The structure also makes use of the *break* keyword. So all in all, this structure contains four C language keywords: and Build and run the code above to see what it does. Run it a few times to try out various options. The code accepts character input, although it could have easily accepted integers.

Here’s how it works: Switch handles a single value, not a comparison. It can be a mathematical equation, but the result must be a single value. That value, specified by is then compared to the values of each *case* statement. If the comparison is true, then the statements belonging to the *case* statement that is flagged as true is executed. If not, they’re skipped.