# Table 9-1 (continued)

| Error | Example | Most Likely Messages or Results |
|---|---|---|
| Missing semicolon after a statement that's inside the if clause or the else clause | if (randomNumber > 5) { System.out.println("Y") } | ';' expected Syntax error, insert " ;" to complete BlockStatements |
| Semicolon immediately after the condition | if (randomNumber > 5); { System.out.println("Y"); } else { | 'else' without 'if' Syntax error on token "else", delete this token |
| Semicolon immediately after the word else | } else; { | The program compiles without errors, but the statement after the word else is always executed, whether the condition is true or false. |
| Missing curly braces | if (randomNumber > 5) System.out.println("Y"); else System.out.println("N"); | The program sometimes compiles without errors, but the program's run may not do what you expect it to do. (So the bottom line is, don't omit the curly braces.) |

As you compose your code, it helps to think of an if statement as one indivisible unit. Instead of typing the whole first line (condition and all), try typing the if statement's skeletal outline.

```
if () {    //To do: Fill in the condition.
            //To do: Fill in SomeStatements.
} else {
            //To do: Fill in OtherStatements.
}
```

With the entire outline in place, you can start working on the items on your to-do list. When you apply this kind of thinking to a compound statement, it's harder to make a mistake.