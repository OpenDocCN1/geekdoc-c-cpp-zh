counting loops because the for loop format enables you to place all the relevant information—initial value, terminating value, and method of updating the counter—in one place. Programmers most often use while loops when they don’t know in advance precisely how many times a loop will execute.

# Tip

Keep in mind the following guidelines when you design a loop:

+   - Identify the condition that terminates loop execution.
+   - Initialize that condition before the first test.
+   - Update the condition in each loop cycle before the condition is tested again.

One nice thing about for loops is that their structure provides a place to implement these three guidelines, thus helping you to remember to do so. But these guidelines apply to a while loop, too.

# Bad Punctuation

Both for loops and while loops have bodies that consist of a single statement following the parenthesized expressions. As you’ve seen, that single statement can be a block, which can contain several statements. Keep in mind that braces, not indentation, define a block. Consider the following loop, for example:

```
i = 0;
while (name[i] != '\0')
    cout << name[i] << endl;
    i++;
cout << "Done\n";
```

The indentation tells you that the program author intended the i++; statement to be part of the loop body. The absence of braces, however, tells the compiler that the body consists solely of the first cout statement. Thus, the loop keeps printing the first character of the array indefinitely. The program never reaches the i++; statement because it is outside the loop.

The following example shows another potential pitfall:

```
i = 0;
while (name[i] != '\0');    // problem semicolon
{
    cout << name[i] << endl;
    i++;
}
cout << "Done\n";
```

This time the code gets the braces right, but it also inserts an extra semicolon. Remember, a semicolon terminates a statement, so this semicolon terminates the while loop. In other words, the body of the loop is a null statement—that is, nothing followed by a semicolon. All the material in braces now comes after the loop and is never reached. Instead, the loop cycles, doing nothing forever. Beware the straggling semicolon.