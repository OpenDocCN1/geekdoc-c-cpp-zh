+   - You write another line or two of production code that makes the test compile.
+   - You write another line or two of test code that compiles but fails an assertion.
+   - You write another line or two of production code that passes the assertion.

And this is going to be your life from now on.

Once again, the experienced programmer will likely consider this to be absurd. The three laws lock you into a cycle that is just a few seconds long. Each time around that cycle, you are switching between test code and production code. You’ll never be able to just write an `if` statement or a `while` loop. You’ll never be able to just write a function. You will be forever trapped in this tiny little loop of switching contexts between test code and production code.

You may think that this will be tedious, boring, and slow. You might think that it will impede your progress and interrupt your chain of thought. You might even think that it’s just plain silly. You may think that this approach will lead you to produce spaghetti code or code with little or no design—a haphazard conglomeration of tests and the code that makes those tests pass.

Hold all those thoughts and consider what follows.

# *Losing the Debug-foo*

I want you to imagine a room full of people following these three laws—a team of developers all working toward the deployment of a major system. Pick any one of those programmers you like, at any time you like. Everything that programmer is working on executed and passed all its tests within the last minute or so. And this is always true. It doesn’t matter who you pick. It doesn’t matter when you pick them. Everything worked a minute or so ago.

What would your life be like if everything worked a minute or so ago? How much debugging do you think you would do? The fact is that there’s not likely much to debug if everything worked a minute or so ago.