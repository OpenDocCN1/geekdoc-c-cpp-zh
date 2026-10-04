(I left off the `year = year + 1;`) Without the increment, `year` is always 1 and the program loops forever. The only way to exit this *infinite loop* is to terminate the program or reboot. (So nothing is truly infinite, with the possible exception of a particle passing through the event horizon of a black hole.)

Make sure that the terminating condition can be satisfied. Usually, this means your counting variable is being incremented properly. Otherwise, you’re looking at an infinite loop, an angry user, bad press, and 50 years of drought.

Infinite loops are a common mistake, so don’t be embarrassed when you get caught in one.

# Doing the do . . . while loop

A variation of the `while` loop is the `do . . . while` loop. In this example, the condition isn’t checked until the *end* of the loop:

```
int year = 1;
do
{
    // . . . some calculation . . .
    year = year + 1;
} while (year < duration);
```

In contrast to the `while` loop, the `do . . . while` loop is executed at least once, regardless of the value of `duration`.

# Breaking up is easy to do

You can use two special commands to bail out of a loop: `break` and `continue`. Executing the `break` command causes control to pass to the first expression immediately following the loop. The similar `continue` command passes control straight back up to the conditional expression at the top of the loop to start over and get it right this time.

I have rarely used `continue` in my programming career, and I doubt that many programmers even remember that it exists. Don’t forget about it completely because it may be a trick question in an interview or a crossword puzzle.

Suppose that you want to take your money out of the bank as soon as the principal exceeds a certain number of times the original amount, irrespective of the duration in years. (After all, how much money do you really need?) You could easily accommodate this amount by adding the following code within the loop:

```
if (principal > (maxPower * originalPrincipal))
{
    break;
}
```