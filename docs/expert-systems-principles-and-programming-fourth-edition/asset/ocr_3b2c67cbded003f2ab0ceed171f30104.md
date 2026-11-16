Notice that the rule asserts the fact (phase continue) regardless of the user's response to the continue question. Asserting this fact will place the appropriate rules on the agenda to continue execution. If the reply to the continue question was not yes, execution will be stopped by the halt function. The user could then examine the rules and facts, later restarting execution where it had left off by issuing a run command.

# 10.3 THE DEFFUNCTION CONSTRUCT

CLIPS allows you to define new functions as you can in other procedural languages. With rules, this can help to reduce repeated expressions in both the LHS and RHS portions. New functions are defined using the deffunction construct. The general format of a deffunction is:

```
(deffunction <deffunction-name> [<optional-comment>]
 (<regular-parameter>* [<wildcard-parameter>])
 <expression>*)
```

where <regular-parameter> is a single-field variable and <wildcard-parameter> is a multifield variable. The name of the deffunction, <deffunction-name>, must be distinct. It cannot be the same as one of the existing predefined CLIPS functions. The body of the deffunction, represented by <expression>*, is a series of expressions similar to the RHS of a rule that are executed in order when the deffunction is called. User-defined deffunctions behave similarly to the predefined functions provided by CLIPS. Wherever you could call a predefined CLIPS system function, you can call a deffunction. Unlike predefined functions, deffunctions can be deleted and the watch command can be used to trace their execution.

The <regular-parameter> and <wildcard-parameter> declarations allow you to specify the arguments that will be passed into the deffunction when it is called. This is somewhat analogous to rules if you consider the variables bound on the LHS of the rule that are used in the RHS to be parameter declarations. Just as you can on the RHS of a rule, you can use the bind command in the body of a deffunction to create local variables.

Just as some predefined functions return values, a deffunction can return values as well. The return value of a deffunction is that value of the last expression evaluated within the body of the deffunction.

As an example, we'll write a deffunction that computes the length of the hypotenuse of a right triangle using the Pythagorean Theorem. If a and b are the sides forming the right angle and c is the hypotenuse, then the theorem states:

```
a^2 + b^2 = c^2
```

Rearranging the terms gives the length of the hypotenuse:

```
c = \sqrt{a^2 + b^2}
```