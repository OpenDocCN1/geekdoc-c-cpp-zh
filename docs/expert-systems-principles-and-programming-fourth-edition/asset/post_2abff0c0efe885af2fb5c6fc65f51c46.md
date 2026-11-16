
6
CLIPS> (/ 2 3)
0.66666667
CLIPS>

Note that the answer for division will probably show a round-off error in the last digit. This result may vary from machine to machine.

The return value of the +, -, and * functions is an integer if all of the arguments to the function are integers. If one of the arguments to the function is a floating-point number, then the return value is a floating-point number. The first argument to the / function is always converted to a float, so the return value of this function is always a float. For example,

```
CLIPS> (+ 2 3.0)
5.0
CLIPS> (+ 2.0 3)
5.0
CLIPS> (+ 2 3)
5
CLIPS>
```

## Variable Numbers of Arguments

Prefix notation allows variable numbers of arguments to be represented quite simply. Many CLIPS functions accept a variable number of arguments. The arguments in a numeric expression can be extended beyond two for the +, -, /, and * functions. The same sequence of arithmetic calculations is performed for more than two arguments. The following examples, entered at the top level, show how three arguments are used. Evaluation proceeds from left to right:

```
CLIPS> (+ 2 3 4)
9
CLIPS> (- 2 3 4)
-5
CLIPS> (* 2 3 4)
24
CLIPS> (/ 2 3 4)
0.16666667
CLIPS>
```

Once again note that the answer for division may vary slightly depending on the machine being used.

## Precedence and Nesting Expressions

One important fact about CLIPS and LISP calculations is that there is no built-in precedence of arithmetic operations. In other computer languages, multiplication and division rank higher than addition and subtraction and the computer does the higher-ranked operations first. In LISP and CLIPS everything is simply evaluated from left to right, with parentheses determining precedence.

Mixed calculations can be done in prefix notation. For example, suppose the following infix expression is to be evaluated:

```
2 + 3 * 4
```

The customary evaluation is to multiply 3 by 4 and then add the result to 2. However, in CLIPS the precedence must be explicitly written. The expression could be evaluated by entering the following at the top level:

```
CLIPS> (+ 2 (* 3 4))
14
CLIPS>
```

In this rule the expression in the innermost parentheses is evaluated first, so 3 is multiplied by 4. The result is then added to 2. If the desired evaluation is (2 + 3) * 4, where addition is done first, the top-level expression would be:

```
CLIPS> (* (+ 2 3) 4)
20
CLIPS>
```

In general, expressions may be freely embedded within other expressions. Thus it is possible to place an expression within an assert command, as the following example shows:

```
CLIPS> (clear)
CLIPS> (assert (answer (+ 2 2)))
<Fact-0>
CLIPS> (facts)
f-0     (answer 4)
For a total of 1 fact.
CLIPS>
```

Also, since function names are also symbols, you can use them as you would other symbols. For example, you could use them as fields in a fact:

```
CLIPS> (clear)
CLIPS> (assert (expression 2 + 3 * 4))
<Fact-0>
CLIPS> (facts)
f-0     (expression 2 + 3 * 4)
For a total of 1 fact.
CLIPS>
```

However, parentheses are used by CLIPS as delimiters, so it's not possible to use them as you would other symbols. In order to use them in facts or as an argument to a function, enclose them in quotation marks to make them strings.

## 8.4 SUMMING VALUES USING RULES

As a simple example of using functions to perform calculations, consider the problem of summing up the area of a group of rectangles. The heights and widths of the rectangles can be specified using the following deftemplate:

```
(deftemplate rectangle (slot height) (slot width))
```

and the sum of rectangle areas could be specified using an ordered fact such as the following:

```
(sum 20)
```

A deffacts containing sample information is:

```
(deffacts initial-information
(rectangle (height 10) (width 6))
(rectangle (height 7) (width 5))
(rectangle (height 6) (width 8))
(rectangle (height 2) (width 5))
(sum 0))
```

An initial attempt to produce a rule to sum the rectangle might be:

```
(defrule sum-rectangles
(rectangle (height ?height) (width ?width))
?sum <- (sum ?total)
=>
(retract ?sum)
(assert (sum (+ ?total (* ?height ?width)))))
```

This rule, however, will loop endlessly. Retracting the sum fact and then re-asserting it will produce a loop with a single rectangle fact. One solution to solve the problem would be to retract the rectangle fact after its area was added to the sum fact. This would prevent the rule from firing after the same rectangle fact with a different sum fact. If the rectangle fact needs to be preserved, a different approach is required. A temporary fact containing the area to be added to the sum is created for each rectangle fact. This temporary fact can then be retracted, preventing an endless loop. The modified program is as follows:

```
(defrule sum-rectangles
  (rectangle (height ?height) (width ?width))
  =>
  (assert (add-to-sum (* ?height ?width))))
```

```
(defrule sum-areas
  ?sum <- (sum ?total)
  ?new-area <- (add-to-sum ?area)
  =>
  (retract ?sum (+ ?total ?area))))
```

The following output shows how these two rules interact to sum the areas of the rectangles:

```
CLIPS> (unwatch all)
CLIPS> (watch rules)
CLIPS> (watch facts)
CLIPS> (watch activations)
CLIPS> (reset)
==> f-0   (initial-fact)
==> f-1   (rectangle (height 10) (width 6))
==> Activation 0   sum-rectangles: f-1
==> f-2   (rectangle (height 7) (width 5))
==> Activation 0   sum-rectangles: f-2
==> f-3   (rectangle (height 6) (width 8))
==> Activation 0   sum-rectangles: f-3
==> f-4   (rectangle (height 2) (width 5))
==> Activation 0   sum-rectangles: f-4
==> f-5   (sum 0)
CLIPS> (run)
FIRE  1 sum-rectangles: f-4
==> f-6   (add-to-sum 10)
==> Activation 0   sum-areas: f-5,f-6
FIRE  2 sum-areas: f-5,f-6
==> f-5   (sum 0)
==> f-6   (add-to-sum 10)
==> f-7   (sum 10)
FIRE  3 sum-rectangles: f-3
==> f-8   (add-to-sum 48)
==> Activation 0   sum-areas: f-7,f-8
FIRE  4 sum-areas: f-7,f-8
==> f-7   (sum 10)
==> f-8   (add-to-sum 48)
==> f-9   (sum 58)
FIRE  5 sum-rectangles: f-2
==> f-10         (add-to-sum 35)
==> Activation 0   sum-areas: f-9,f-10
FIRE   6 sum-areas: f-9,f-10
<=> f-9          (sum 58)
<=> f-10         (add-to-sum 35)
<=> f-11         (sum 93)
FIRE   7 sum-rectangles: f-1
<=> f-12         (add-to-sum 60)
==> Activation 0   sum-areas: f-11,f-12
FIRE   8 sum-areas: f-11,f-12
<=> f-11         (sum 93)
<=> f-12         (add-to-sum 60)
<=> f-13         (sum 153)
CLIPS> (unwatch all)
CLIPS>
```

The sum-rectangles rule is activated four times when the rectangle facts are asserted as a result of the reset command. Each time the sum-rectangles rule is fired it asserts a fact that activates the sum-areas rule. The sum-areas rule adds the area to the running total and removes the add-to-sum fact. Since the sum-rectangles rule does not pattern match against the sum fact, it is not reactivated when a new sum fact is asserted.

## 8.5 THE BIND FUNCTION

It is often useful to store a value in a temporary variable to avoid recalculation, which is crucial when functions produce side effects. The bind function can be used to bind the value of a variable to the value of an expression. The syntax of the bind function is:

```
(bind <variable> <value>)
```

The bound variable, <variable>, uses the syntax of a single-field variable. The new value, <value>, should be an expression that evaluates to either a single-field or a multifield value. For example, the sum-areas rule could print out the total sum and the area being added to it for each rectangle:

```
(defrule sum-areas
  ?sum <- (sum ?total)
  ?new-area <- (add-to-sum ?area)
  =>
  (retract ?sum ?new-area)
  (printout t "Adding ? area " to " ?total crlf)
  (printout t "New sum is " (+ ?total ?area) crlf)
  (assert (sum (+ ?total ?area))))
```

Notice that the expression (+ ?total ?area) is used twice in the RHS of the rule. Replacing the two separate evaluations with one bind function would eliminate unnecessary calculations. The rule rewritten with the bind function is:

```
(defrule sum-areas
  ?sum <- (sum ?total)
  ?new-area <- (add-to-sum ?area)
  =>
  (retract ?sum ?new-area)
  (printout t "Adding ? area" to " ?total crlf)
  (bind ?new-total (+ ?total ?area))
  (printout t "New sum is " ?new-total crlf)
  (assert (sum ?new-total)))
```

In addition to creating new variables for use on the RHS of a rule, the bind function can be used to rebind the value of a variable used in the LHS of a rule.

## 8.6 I/O FUNCTIONS

### The Read Function

Expert systems often require input from the user of the program. CLIPS allows information to be read from the keyboard using the read function. The basic syntax of the read function requires no arguments and the following example shows how it is used to input data:

```
CLIPS> (clear)
CLIPS>
(defrule get-first-name
  =>
  (printout t "What is your first name? ")
  (bind ?response (read))
  (assert (user's-name ?response)))
CLIPS> (reset)
CLIPS> (run)
What is your first name? Gary
CLIPS> (facts)
f-0 (initial-fact)
f-1 (user's-name Gary)
For a total of 2 facts.
CLIPS>
```

Notice that the read function requires a carriage return before it will read the token entered. The read function can be used to input only a single field at a time. All extra characters entered after the first field, up to the carriage return, are discarded. For example, if the get-first-name rule tried to read both the first name and the last name with the following input,
