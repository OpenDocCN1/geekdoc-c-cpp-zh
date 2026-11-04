The ! operator returns true if its single operand is false. For example, if the cafeteria is not closed, you can have lunch there:

```
canHaveLunch = !cafeteriaIsClosed;
```

The conditional operators, which are also called short-circuit operators, work just like the regular ones except they don't evaluate their second operand unless they must. For example, consider the following AND statement:

```
mustBuyLunch = isLunchTime && forgotToBringLunch;
```

Suppose it's only 9:00 a.m. so isLunchTime is false. When the program sees this expression, it evaluates isLunchTime and then encounters the && operator. Because isLunchTime is false, the program already knows that mustBuyLunch must also be false no matter what value follows the && (in this case forgotToBringLunch). In that case, the program doesn't bother to evaluate forgotToBringLunch and that saves a tiny amount of time.

Similarly, consider the following OR statement:

```
canAffordLunch = haveEnoughMoney || haveCreditCard;
```

If you have enough money, haveEnoughMoney is true, so the program doesn't need to evaluate haveCreditCard to know that the result canAffordLunch is also true.

Because the conditional && and || operators are slightly faster, most developers use them whenever they can instead of using & and |.

> NOTE There is one case where the conditional operators may cause problems. If the second operand is not a simple value but the result returned from some sort of method call, then if you use a conditional operator, you cannot always know whether the method was called. This might matter if the method has side effects: consequences that last after the method has finished, like opening a database or creating a file. In that case, you cannot know later whether the database is open or the file is created. This is seldom a problem and you can avoid it completely by avoiding side effects.

# String Operators

The only string operator C# provides is +. This operator concatenates (joins) two strings together. For example, suppose the variable username contains the user's name. Then the following code concatenates the text "Hello " (note the trailing space) with the user's name and displays the result in a message box:

```
MessageBox.Show("Hello " + username);
```

Lesson 14 explains methods that you can use to manipulate strings: find substrings, replace text, check length, and so forth.