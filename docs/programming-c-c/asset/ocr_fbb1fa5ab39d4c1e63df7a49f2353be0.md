# SWITCH STATEMENT IN C

The switch statement in C is an alternate to if-else-if ladder statement which allows us to execute multiple operations for the different possible values of a single variable called switch variable. Here, we can define various statements in the multiple cases for the different values of a single variable.

A switch statement tests the value of a variable and compares it with multiple cases. When the case match is found, a block of statements associated with that particular case is executed.

Each case in a block of switch has a different name/number which is referred to as an identifier. The value provided by the user is compared with all the cases inside the switch block is found.

If a case match is found, then the default statement is executed, and the control goes out of the switch block.

# Rules for switch Statement in C Language

+   1. The switch expression must be of an integer or character type.
2. The case value must be an integer or character constant.
3. The case value can be used only inside the switch statement.
4. The break statement in switch case is not must. It is optional. If there is no break statement found in the case, all the cases will be executed after the matched case. It is known as fall through the state of C switch statement.
5. Case value must be constants and unique.
6. Case labels must end with a colon (:).
7. There can be only one default label.
8. A break keyword must be present in each case.
9. We can nest multiple switch statements.

Let's try to understand it by the examples. We are assuming that there are following variables:

```
int x,y,z;
char a,b;
float f;
```