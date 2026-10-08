# 5.2 Algorithms

Any computing problem can be solved by executing a series of actions in a specific order.
A procedure for solving a problem in terms of

+   1. the actions to execute and
2. the order in which these actions execute

is called an algorithm. The following example demonstrates that correctly specifying the
order in which these actions execute is important.
Consider the "rise-and-shine algorithm" one execute follows for getting out of bed
and going to work: (1) Get out of bed; (2) take off pajamas; (3) take a shower; (4)
dressed; (5) eat breakfast; (6) carpool to work. This routine gets the execute work well
make critical decisions. Suppose that the same are performed in a slightly
different order: (1) Get out of bed; (2) take off pajamas; (3) get dressed; (4) take a shower;
(5) eat breakfast; (6) carpool to work. In this case, our execute shows up for work soaking
ifying the order in which statements (actions) execute in a program is called pro-
gram control control statements.

# 5.3 Pseudocode

Pseudocode is an informal language that helps develop algorithms without having to
worry about the strict details of C# language syntax. The pseudocode we present is partic-
early useful for developing algorithms that will be converted to structured programs of C#napps. Pseudocode is similar to everyday (or other natural language)—it's conve-
ient and friendly, but not an actual computer programming language. You'll see
an algorithm written in pseudocode in Fig. 5.1. You may use, or use your native
language(s) to develop your own pseudocode style.

Pseudocode does not execute on computers. Rather, it helps "think out" an
before attempting to write it in a programming language, as C#. This chapter pro-
views several examples of using pseudocode to develop C# apps.

The style of pseudocode we presents mostly of characters, so you can type
conveniently, using any text editor. Carefully prepared pseudocode can be
converted to a corresponding C# app.

Pseudocode normally describes statements representing the actions that occur
after you convert from pseudocode to a C# app and run the app on a computer. Such
actions might include input, output, assignments or calculations. In our pseudocode, we typ-
ell not include any variable declarations, but some choose to list variables
and mention their purposes.

# Addition-Program Pseudocode

Let's look at an example of pseudocode that may be written to help a programmer create
the addition program of Fig. 3.14. corresponds to the algo-
rith that inputs two integers from the user, adds these integers and displays their sum.
We show the complete pseudocode listing here—we'll show how to create pseudocode
from a problem statement in the chapter.

Notice that the pseudocode statements are simple English statements that convey
what task is to be performed in C#. Lines 1–2 correspond to the C# statements in lines 14