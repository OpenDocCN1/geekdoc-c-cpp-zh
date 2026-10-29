# Display 2.5 Example of a do-while Statement (part 2 of 2)

# SAMPLE DIALOGUE 2

```
How many greetings do you want? 0
Hello
That's all!
```

The loop body is always executed at least once.

The important difference between the while and do-while loops involves when the controlling Boolean expression is checked. With a while statement, the Boolean expression is checked before the loop body is executed. If the Boolean expression evaluates to false, the body is not executed at all. With a do-while statement, the body of the loop is executed first and the Boolean expression is checked after the loop body is executed. Thus, the do-while statement always executes the loop body at least once. After this start-up, the while loop and the do-while loop behave the same. After each iteration of the loop body, the Boolean expression is again checked; if it is true, the loop is iterated again. If it has changed from true to false, the loop statement ends.

The first thing that happens when a while loop is executed is that the controlling Boolean expression is evaluated. If the Boolean expression evaluates to false at that point, the body of the loop is never executed. It may seem pointless to execute the body of a loop zero times, but that is sometimes the desired action. For example, a while loop is often used to sum a list of numbers, but the list could be empty. To be more specific, a checkbook balancing program might use a while loop to sum the values of all the checks you have written in a month—but you might take a month's vacation and write no checks at all. In that case, there are zero numbers to sum and so the loop is iterated zero times.

executing the body zero times

# INCREMENT AND DECREMENT OPERATORS REVISITED

In general, we discourage the use of the increment and decrement operators in expressions. However, many programmers like to use them in the controlling Boolean expression of a while or do-while statement. If done with care, this can work out satisfactorily. An example is given in Display 2.6. Be sure to notice that in count++ <= numberOfItems, the value returned by count++ is the value of count before it is incremented.