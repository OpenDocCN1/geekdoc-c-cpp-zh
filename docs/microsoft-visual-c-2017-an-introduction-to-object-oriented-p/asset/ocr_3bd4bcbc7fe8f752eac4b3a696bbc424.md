```
switch(year)
{
    case 1:
        WriteLine("Freshman");
        break;
    case 2:
        WriteLine("Sophomore");
        break;
    case 3:
        WriteLine("Junior");
        break;
    case 4:
        WriteLine("Senior");
        break;
    default:
        WriteLine("Invalid year");
        break;
}
```

**Figure 4-21** Executing multiple alternatives using a switch statement

The switch structure uses four new keywords:

+   - The keyword switch starts the structure and is followed immediately by a test expression (called the *switch expression*) enclosed in parentheses.

+   - The keyword case is followed by one of the possible values that might equal the switch expression. A colon follows the value. The entire expression—for example, case 1—is a case label. A case label identifies a course of action in a switch structure. Most switch structures contain several case labels. The value that follows the governing type of the switch statement. Prior to C# 7.0, there were restrictions on the governing type in a switch statement, but with the newest version, the governing type can be any data type.

+   - The keyword break usually terminates a switch structure at the end of each case. Although others can end a case, break is the most commonly used.

+   - The keyword default is optionally used prior to any action that should occur if the test expression does not match any case.

Instead of break, you can use a return statement or a throw statement to end a case. You learn about return statements in the chapter "Introduction to Methods" and throw statements in the chapter "Exception Handling."