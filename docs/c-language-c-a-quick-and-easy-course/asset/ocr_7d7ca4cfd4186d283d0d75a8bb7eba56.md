# CHAPTER 4

# CONDITIONAL EXECUTION

# The if-else statement

When Ada Byron, Countess of Lovelace, at the nineteenth century, invented computer programming, to be used in the unfinished Analytical Engine of his friend and mathematical instructor Charles Babbage, she created even in that period what would be the soul of programming, which is running on cycles which require a stopping condition, which, in turn, leads to the need of the conditional execution today mostly used in the form of an if statement, introduced by Grace Murray hopper a century later. With the use of cycles and recursion, Ada realized that the Analytical Engine, unlike the previous Difference Engine, could solve any problem with coded instructions previously granted, which was made by punched cards, created by Joseph Marie Jacquard in 1805, which we used until 1975, a little More than that. She wrote a problem that required 330 cards could be solved with only three, if she used the cycles. Concerning to the scope of the machine, she said in 1843 that if properly we transformed notes and durations in abstract algebraic codes, the machine would be able to “compose elaborate and scientific pieces of music of any degree of complexity or extent”, as Stephen Wolfram.

In the most of the high-level languages, the appearance of a simple if statement is as follows:

```
if(condition)
statement 1
[else
statement 2].
```

In Pascal we have a line with the following statement: if x>0 then write ('Positive!')
else n := x. In C language there is no word then and the condition lies within parentheses. An example is the following mini-program:

```
main(){ int n; char c; puts("nN/Y?"); c=getchar();
```