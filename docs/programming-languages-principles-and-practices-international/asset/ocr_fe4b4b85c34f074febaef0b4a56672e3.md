The operation of looking up the value of an identifier $I$ in an environment $Env$ is then simply described by function evaluation $Env(I)$. The operation of adding a new value binding to $Env$ can also be defined in functional terms. We will use the notation $Env \& \{I = n\}$ to denote the adding of the new value $n$ for $I$ to $Env$. In terms of functions,

$$(Env \& \{I = n\})(J) = \begin{cases} n & \text{if } J = I \\ Env(J) & \text{otherwise} \end{cases}$$

Finally, we also need the notion of the **empty environment**, which we will denote by $Env_0$:

$$Env_0(I) = \text{undef for all } I$$

This notion of environment is particularly simple and differs from what we called the environment in Chapters 7 and 10. Indeed, an environment as defined here incorporates both the symbol table and state functions from Chapter 7. We note that such environments do not allow pointer values, do not include scope information, and do not permit aliases. More complex environments require much greater complexity and will not be studied here.

This view of the semantics of a program as represented by a resulting, final environment has the effect that the consistency and completeness properties stated in the introduction have the following straightforward interpretation: Consistency means that we cannot derive two different final environments for the same program, and completeness means that we must be able to derive a final environment for every correct, terminating program.

The second extension to our sample language will be the addition of “if” and “while” control statements to the first extension. Statements can now be of three kinds, and we extend their definition accordingly; see Figure 12.3.

```
stmt → assign-stmt | if-stmt | while-stmt
assign-stmt → identifier ‘:=’ expr
if-stmt → ‘if’ expr ‘then’ stmt-list ‘else’ stmt-list ‘fi’
while-stmt → ‘while’ expr ‘do’ stmt-list ‘od’
```

**Figure 12.3** Second extension of the sample language

The syntax of the if statement and while statement borrow the Algol68 convention of writing reserved words backward—thus od and fi—to close statement blocks rather than using the begin and end of Pascal and Algol60.

The meaning of an *if-stmt* is that *expr* should be evaluated in the current environment. If it evaluates to an integer greater than 0, then the *stmt-list* after ‘then’ is executed. If not, the *stmt-list* after the ‘else’ is executed. The meaning of a *while-stmt* is similar: As long as *expr* evaluates to a quantity greater than 0, *stmt-list* is repeatedly executed, and *expr* is reevaluated. Note that these semantics are nonstandard!