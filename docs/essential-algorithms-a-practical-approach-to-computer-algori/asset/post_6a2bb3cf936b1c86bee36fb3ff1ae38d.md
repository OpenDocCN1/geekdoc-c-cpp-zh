
## Appendix B = Solutions to Exercises

walls. (It doesn't matter how the marbles between the walls are ordered, because you can't tell the blue marbles apart.)

One way to think about this is to imagine eight slots where you put either a blue marble or an a. Now you pick slots for the marbles and fill in the remaining with blue marbles. The number of ways you can do that is as follows:

```
$$\frac{8!}{4!(2!4!)} = \frac{8! \ 40,320}{24 \times 24} = 70$$
```

The number of "good" arrangements is 70, and the total number of possible arrangements is 330, so that a random arrangement is "good" is $70/330 = 7/33 \approx 21\%$.

This problem is pretty interesting, but it's quite difficult. This kind of problem is fairly common in probability and statistics courses, so a candidate who has taken such a course will probably know the basic approach. Even it would be a tough calculation, and if the candidate hasn't taken that kind of course, this problem will be extremely hard.

All that the interviewer will learn from this question is whether the candidate has seen a problem like this or has taken...

- 5. The most obvious approach is to use a linked list. You could also do this in an array with a For loop. You get bonus points if you mention both methods and say that the better method depends on how the list is already stored for use in performing operations.

This is actually a relevant question! You may never need to reverse a list of customers in this way, but answering this question shows that you know about at least one type of data structure. Mentioning both the linked list and array solutions shows you about at least two data structures and that you can look for more solutions until you find one.

- 6. This problem has a couple approaches. For the algebraic approach, let M be my current age, and let B be my brother's current age. Then:

```
$M = x \times B$$
```

```
$$(M + 2) \times B = 2 \times (B + 2)$$
```

Plugging the first equation into the second gives you this:

```
$$(3 \times B) + 2 = 2 \times (B + 2)$$
```

Rearranging and solving for B gives you this:

```
$$3 \times B + 2 = 2 \times B + 4$$
```

```
$$3 \times B - 2 \times B = 4 - 2$$
```

```
$$B = 2$$
```

Inserting this value into the first equation gives M = 3 × 2 = 6, so I am 6 right now.

A second approach is to make a table similar to the starting, with a guess of 30 for yourself:

| BROTHER'S AGE | MY AGE | BROTHER + 2 | MY AGE + 2 | 2 × {BROTHER + 2} |
|---|---|---|---|---|
| 10 | 12 | 12 | 14 | 24 |

After filling the first row, you compare the last two columns. In this case, My Age + 2 is too big, so you guess with smaller ages:

| BROTHER'S AGE | MY AGE | BROTHER + 2 | MY AGE + 2 | 2 × {BROTHER + 2} |
|---|---|---|---|---|
| 10 | 12 | 12 | 14 | 24 |
| 5 | 15 | 7 | 17 | 14 |

In the second row, the difference between the last two columns is closer but still too big, so you guess with even smaller ages:

| BROTHER'S AGE | MY AGE | BROTHER + 2 | MY AGE + 2 | 2 × {BROTHER + 2} |
|---|---|---|---|---|
| 10 | 12 | 12 | 14 | 24 |
| 5 | 15 | 7 | 17 | 14 |
| 2 | 6 | 4 | 8 | 8 |

In this example, the third row finds the solution. (If you overshoot and My Age + 2 turns out too small, larger ages.)

This problem is worth asking because it lets you see whether the candidate is more comfortable using algebra or a table. I'm not sure how useful that information will be, though. Many problems like this are more involved, so a table won't work well, but just because the candidate used a table doesn't mean he or she can't use algebra if it's required.

If you use a problem, it's probably best to ask the candidate why or she chose a particular approach and what other approaches might also work.

- 7. This problem is somewhat relevant for programmers it involves a 'fencepost problem.' 'Suppose you're building a fence with rails between posts. There will be one more than rails, because you need a post on each end of the fence. A fencepost (or off-by-1) occurs when a programmer accidentally counts one object too many times or one few times.

For this problem, the minute hand passes the hour hand a bit after 1:05, a bit longer after 2:10, and so up to some time after 10:50. The next time the hands meet 11:00 is 12:00 midnight. That means the hands cross between 2:00 and 3:00, and so on up to a time between 10:00 and 11:00. (At this point, perhaps you can see the fencepost problem.)

If you only count times strictly between noon and midnight, the hands cross 10 times. If you also count the times they cross at noon and midnight, the hands cross 12 times.

How the candidate approaches this question may tell you a bit about how he is, but that may be all it tells you. At least a capable candidate can come up with some solution either right or without knowing a sneaky trick.

- (Microsoft) has used this question in interviews. The following paragraphs describe three ways to look at this:

- a. A short, off-the-cuff answer is “50%, because boys and girls are equally likely, so in any population of children, 50% are girls.” That’s a “big picture” but it’s not necessarily intuitive, so the interviewer might ask you to prove it. (That actually does prove it, by digging at it.)

- b. Another intuitive way to look at this is to consider first, second, third, and so on.

- c. For another way to look at this, consider the probability of having a girl.
