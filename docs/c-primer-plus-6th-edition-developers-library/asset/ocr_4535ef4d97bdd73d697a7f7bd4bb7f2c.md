Here you have combined the incrementing process and the while comparison into one expression. This type of construction is so common in C that it merits a closer look.

First, how does this construction work? Simply. The value of shoe is increased by 1 and then compared to 18.5. If it is less than 18.5, the statements between the braces are executed once. Then shoe is increased by 1 again, and the cycle is repeated until shoe gets too big. We changed the initial value of shoe from 3.0 to 2.0 to compensate for shoe being incremented before the first evaluation of foot (see Figure 5.4).

![](bbox=[0.18, 0.36, 0.78, 0.52])

Figure 5.4 Through the loop once.

Second, what’s so good about this approach? It is more compact. More important, it gathers in one place the two processes that control the loop. The primary process is the test: Do you continue or not? In this case, the test is checking to see whether the shoe size is less than 18.5. The secondary process changes an element of the test; in this case, the shoe size is increased.

Suppose you forgot to change the shoe size. Then shoe would always be less than 18.5, and the loop would never end. The computer would churn out line after identical line, caught in a dreaded infinite loop. Eventually, you would lose interest in the output and have to kill the program somehow. Having the loop test and the loop change at one place, instead of at separate locations, helps you to remember to update the loop.

A disadvantage is that combining two operations in a single expression can make the code harder to follow and can make it easier to make counting errors.

Another advantage of the increment operator is that it usually produces slightly more efficient machine language code because it is similar to actual machine language instructions. However, as vendors produce better C compilers, this advantage may disappear. A smart compiler can recognize that x = x + 1 can be treated the same as ++x.

Finally, these operators have an additional feature that can be useful in certain delicate situations. To find out what this feature is, try running the program in Listing 5.11.