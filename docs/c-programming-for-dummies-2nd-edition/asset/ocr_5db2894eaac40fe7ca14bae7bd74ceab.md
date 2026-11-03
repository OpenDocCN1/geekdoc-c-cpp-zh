A triple nested loop contains three for statements, which continues the cascade shown in Listing 9-5. As long as you can match up the curly brackets with each for statement (and that's easy, thanks to modern text editors), it's something you can accomplish quite readily.

Exercise 9-12: Write a 3-letter acronym-generating program. The program's output lists all 3-letter combinations from AAA through ZZZ, spewed out each on a line by itself.

![](bbox=[0.13, 0.35, 0.22, 0.5])

I wrote a program similar to the solution to Exercise 9-12 as one of my first programming projects. The computers in those days were so slow that the output took about ten seconds to run. On today's computers, the output is nearly instantaneous.

# The Joy of the while Loop

Another popular looping keyword in C is while. It has a companion, do, so programmers refer to this type of loop as either while or do while. The C language is missing the do-whacka-do type of loop.

# Structuring a while loop

The C language while loop is a lot easier to look at than a for loop, but it involves more careful setup and preparation. Basically, it goes like this:

```
while(expression)
{
    statement(s);
}
```

The expression is a value or a comparison or any of a number of other things that results in a true/false condition, just like you'd find in an if statement. The expression is evaluated each time the loop repeats. As long as it's true ("while" it's true), the loop spins and its statements continue to execute.

![](bbox=[0.13, 0.92, 0.22, 0.98])

Because the expression is evaluated at the start of the loop, the loop must be initialized before the while statement, as shown in Listing 9-6.

So how does a while loop end? The termination must be triggered within the loop's statements. Usually, one of the statements affects the expression that's evaluated, causing it to be false.