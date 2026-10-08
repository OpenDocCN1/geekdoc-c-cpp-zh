+   6.1 A problem
6.2 Thinking about the problem
    6.2.1 Stages of development
    6.2.2 Strategy
6.3 Back to the calculator!
    6.3.1 First attempt
    6.3.2 Tokens
    6.3.3 Implementing tokens
    6.3.4 Using tokens
    6.3.5 Back to the drawing board
6.4 Grammars
    6.4.1 A detour: English grammar
    6.4.2 Writing a grammar

+   6.5 Turning a grammar into code
    6.5.1 Implementing grammar rules
    6.5.2 Expressions
    6.5.3 Terms
    6.5.4 Primary expressions
6.6 Trying the first version
6.7 Trying the second version
6.8 Token streams
    6.8.1 Implementing *Token stream*
    6.8.2 Reading tokens
    6.8.3 Reading numbers
6.9 Program structure

# # 6.1 A problem

Writing a program starts with a problem; that is, you have a problem that you’d like a program to help solve. Understanding that problem is key to a good program. After all, a program that solves the wrong problem is likely to be of little use to you, however elegant it may be. There are happy accidents when a program just happens to be useful for something for which it was never intended, but let’s not rely on such rare luck. What we want is a program that simply and cleanly solves the problem we decided to solve.

At this stage, what would be a good program to look at? A program that

+   - Illustrates design and programming techniques
- Gives us a chance to explore the kinds of decisions that a programmer must make and the considerations that go into such decisions
- Doesn’t require too many new programming language constructs
- Is complicated enough to require thought about its design
- Allows for many variations in its solution
- Solves an easily understood problem
- Solves a problem that’s worth solving
- Has a solution that is small enough to completely present and completely comprehend

We chose “Get the computer to do ordinary arithmetic on expressions we type in”; that is, we want to write a simple calculator. Such programs are clearly useful; every desktop computer comes with such a program, and you can even buy computers specially built to run nothing but such programs: pocket calculators.