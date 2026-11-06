The preceding item in parentheses is *not a comparison*. It's simply a variable. You can also put more complex expressions inside the parentheses, but they must *evaluate* to either an integer or a character. For example, if `x` is an integer, you can test

```
switch (x + 5) {
```

because `x + 5` is still an integer.

After the header line for the `switch` statement, you list the items you want to compare the expression to. These have a rather strange format. They start with the word `case`, and then have the value to compare the expression against, and then a colon, as in

```
case 1:
```

Next is the code to run in the event that the expression matches this case (here, 1).

```
cout << "It's 1" << endl;
```

Finally (here's where it gets really strange), you have the word `break`. Every case in the `switch` statement usually has a `break` line, which means *get out of the switch statement now!* And here's the exceedingly strange part: If you forget the `break` statement, when the computer runs this case, it continues running the code for the *next* case! Yes, C++ can seem stupid at times. And this is one of those rare and less-than-beautiful moments.

Note something peculiar at the end of the `switch` block: The final case is `default`. It applies to the situation when none of the preceding cases applies.

![](bbox=[0.17, 0.56, 0.26, 0.62])

The `default` case isn't required; you can leave it off if you don't need it. However, if you do include it, we recommend putting it at the end of the `switch` block because that's where most people expect to find it.

In the sample code we give at the beginning of this section, you can enter a number, which gets put in the `x` variable. The code then tests the value `x` against `1`; if it matches, it performs the line after the `case 1:` line. If it doesn't match, it tests it against `2` and performs its lines if it matches. But if none of those matches, it executes the code after the `default` line.

When the computer encounters the `break` line, it exits the `switch` statement altogether. So you may be wondering: Why did those goofball authors include a `break` line at the end? Our answer: Tradition. That's all. It's consistent with the other blocks of code. But you certainly don't need it. *However*, if you leave it off, you must remember that if you decide to add any other cases, you will probably want to put it back in. On the other hand, people typically put the `default` at the end. (You don't have to, but most people expect to see it at the end and not in the middle.)