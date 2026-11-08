
conversion routine, `tolower()`, and uses the result to select a case. Converting to lowercase avoids the need to have case labels for uppercase and lowercase letters. All of the cases that identify a vowel cause the same statements to be executed. You can see that you can just write each of the cases in a series, followed by the statements any of these cases is to select. If the input is not a vowel, it must be a consonant and the default case deals with this.

If `isalpha()` returns 0, which converts to false, the switch doesn’t execute because the else clause is selected; this outputs a message indicating that the character entered was not a letter.

In Ex4_09.cpp, we put all case labels with vowel values on a single line. This is not required. You are allowed to add one line break (or any form of whitespace for that matter) in between the case labels as well. Here’s an example:

```cpp
switch (std::tolower(letter))
{
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        std::cout << "You entered a vowel." << std::endl;
        break;
    ...
}
```

A break statement is not the only way to move control out of a switch statement. If the code following a case label contains a return statement, control instantly exits not only the switch statement but the surrounding function as well. So, in principle, you could rewrite the switch statement in Ex4_09 as follows:

```cpp
switch (std::tolower(letter))
{
case 'a': case 'e': case 'i': case 'o': case 'u':
    std::cout << "You entered a vowel." << std::endl;
    return 0;                         // Ends the program
}

// We did not exit main() in the above switch, so letter is not a vowel:
std::cout << "You entered a consonant" << std::endl;
```

With this particular variant, we also see that a default case is optional. If you enter a vowel, the output will reflect this, and the return statement in the switch statement will terminate the program. Note that after a return statement you should never put a break statement anymore. If you enter a consonant, the switch statement does nothing. None of these cases apply, and there is no default case. Execution therefore continues after the switch statement and outputs that you have in fact entered a consonant—remember, if you would’ve entered a vowel, the program would’ve terminated already because of the return statement.

The code for this variant is available as Ex4_09A. We created it to show a few points, though, not because it necessarily reflects good programming style. The use of a default case is surely recommended over continuing after a switch statement after none of the cases executed a return.

**Tip** You will often use switch statements to decide on which action to take based on some enumeration value (see Chapter 3). With switches on enumeration values, you should avoid default cases. In other words: you should normally include as many cases as there are possible values of the corresponding enumeration type. That way, if you ever add a new value to the enumeration type, most compilers will issue warnings for every switch statement that is then no longer exhaustive.

## Fallthrough

The break statement at the end of each group of case statements transfers execution to the statement after the switch. You could demonstrate the essential nature of the break statements by removing them from the switch statements of earlier example Ex4_08 or Ex4_09 and seeing what happens. You'll find that the code beneath the case label directly following the case without a break statement then gets executed as well. This phenomenon is called fallthrough because in a way we "fall through" into the next case.

More often than not, a missing break statement signals an oversight and therefore a bug. To illustrate this, let's return to an earlier example—the one with the lottery numbers:

```cpp
switch (ticket_number)
{
  case 147:
    std::cout << "You win first prize!" << std::endl;
  case 387:
    std::cout << "You win second prize!" << std::endl;
    break;
  case 29:
    std::cout << "You win third prize!" << std::endl;
    break;
  default:
    std::cout << "Sorry, you lose." << std::endl;
    break;
}
```

You'll notice that this time, we have “accidentally” omitted the break statement after the first case. If you executed this switch statement now with ticket_number equal to 147, the output would be as follows:

```
You win first prize!
You win second prize!
```

Because ticket_number equals 147, the switch statement jumps to the corresponding case, and you win first prize. But because there is no break statement, execution simply goes on with the code underneath the next case label, and you win second prize as well—huzzah! Clearly, this omission of break must be an accidental oversight. In fact, because more often than not fallthrough signals a bug, many compilers issue a warning if a nonempty switch case is not followed by either a break or a return statement. Empty switch cases, such as those used in Ex4_09 (to check for vowels), are common enough not to warrant a compiler warning.

Fallthrough does not always mean a mistake was made, though. It can at times be quite useful to purposely write a switch statement that employs fallthrough. Suppose that in our lottery multiple numbers win second and third prize (two and three numbers, respectively) and that one of the numbers winning third prize gets a special bonus prize. Then we could write this logic as follows:

```
switch (ticket_number)
{
case 147:
    std::cout << "You win first prize!" << std::endl;
    break;
case 387:
case 123:
    std::cout << "You win second prize!" << std::endl;
    break;
case 929:
    std::cout << "You win a special bonus prize!" << std::endl;
case 29:
case 78:
    std::cout << "You win third prize!" << std::endl;
    break;
default:
    std::cout << "Sorry, you lose." << std::endl;
    break;
}
```

The idea is that if your ticket_number equals 929, the outcome should be the following:

```
You win a special bonus prize!
You win third prize!
```

If your number is either 29 or 78, however, you'd only win third prize. The slight annoyance with these atypical cases (pun intended) is that compilers may issue a fallthrough warning, even though you know for a fact that this time it is not a mistake. And of course, as a self-respecting programmer, you want to compile all your programs free of warnings. You could always rewrite the code and duplicate the statement to output that you won third prize. But in general, duplication is something you'd like to avoid as well. So, what to do?

Luckily, C++17 added a language feature to signal to both the compiler and the person reading your code that you are intentionally using fallthrough: you can add a `[[fallthrough]]` statement in the same place where you would otherwise add a break statement:

```
switch (ticket_number)
{
...
case 929:
    std::cout << "You win a special bonus prize!" << std::endl;
    [[fallthrough]];
case 29:
case 78:
    std::cout << "You win third prize!" << std::endl;
    break;
...
}
```

For empty cases, such as the one for number 29, a `[[fallthrough]]` statement is allowed but not required. Compilers already do not issue warnings for this.

## Statement Blocks and Variable Scope

A switch statement has its own block between braces that encloses the case statements. An if statement also often has braces enclosing the statements to be executed if the condition is true, and the else part may have such braces too. These statement blocks are no different from any other blocks when it comes to variable scope. Any variable declared within a block ceases to exist at the end of the block, so you cannot reference it outside the block.

Here, consider the following rather arbitrary calculation:

```cpp
if (value > 0)
{
  int savit {value - 1};    // This only exists in this block
  value += 10;
}
else
{
  int savit {value + 1};    // This only exists in this block
  value -= 10;
}
std::cout << savit;         // This will not compile! savit does not exist
```

The output statement at the end causes a compiler error message because the savit variable is undefined at this point. Any variable defined within a block can be used only within that block, so if you want to access data that originates inside a block from outside it, you must define the variable storing that information in an outer block.

Variable definitions within a switch statement block must be reachable in the course of execution, and it must not be possible to bypass them by jumping to a case after the declaration and within the same scope; otherwise, the code will not compile. Most likely you don’t understand at all yet what we mean. It’ll be much easier to explain, though, by means of an example. The following code illustrates how illegal declarations can arise in a switch:

```cpp
int test {3};
switch (test)
{
  int i {1};          // ILLEGAL - cannot be reached

  case 1:
    int j {2};        // ILLEGAL - can be reached but can be bypassed
    std::cout << test + j << std::endl;
    break;

  int k {3};          // ILLEGAL - cannot be reached

  case 3:
  {
    int m {4};        // OK - can be reached and cannot be bypassed
    std::cout << test + m << std::endl;
    break;
  }
}
```
