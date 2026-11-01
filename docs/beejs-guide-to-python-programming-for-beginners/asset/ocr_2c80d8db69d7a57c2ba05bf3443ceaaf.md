1 2 3 4
2 4 6 8
3 6 9 12
4 8 12 16

(If you're rusty on your multiplication tables, what you do to multiply 3 × 4 is to look up 3 along the top edge, then look up 4 along the left edge, and then look in the table where they cross. There you'll find 12, the answer.)

How can we do attack this? Let's look at a couple of things.

First, look for patterns. See any?

I'll wait while you look.

There are several in there.

+   - The diagonals read 1, then 2 2, then 3 4 3, then 4 6 6 4... it's symmetric.
+   - The first row is 1 2 3 4, and the second is 2 4 6 8, and the third is 3 6 9 12. The first skips by 1, the second by 2, the third by 3.
+   - Columns do the same as rows in terms of numbers skipped.

Can we use any of those to our advantage? Maybe...!

Second, let's try to simplify the problem.

What if the problem were to print:

1 2 3 4

and that's all. How would you solve that?

What if it were to print only this:

3 6 9 12

How would you solve that?

**Fun Realism Fact:** There are a lot of ways to program this. As I write this, at least four are immediately coming to mind. Remember: *coding is creative* and there're almost always many ways to get the same result. Be creative! It's your sandbox to mess around in! You can't break the computer.

Problem just some simple for loops, right? We could do this with three for loops:

1 2 3 4
2 4 6 8
3 6 9 12

Something like this (pseudocode):

```
for i in range(1, 5, 1): print(...)
for i in range(2, 10, 2): print(...)
for i in range(3, 15, 3): print(...)
```

But of course, we don't just want to print rows three times... the end result is going to have the number of rows that the user input. We need to loop to make it happen. A loop of loops! A nested loop!

# Problem-solving step: Devising a Plan.

Before we jump into this, I'd like you to take the time to think about this. Set a timer and work on it for 3 minutes.

Do it.

Timer. Do it. You will gain valuable experience points for the attempt.

I'll be back in 3 minutes.

[Elevator music—do it now!]