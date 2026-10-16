# 3.4 Delayed Evaluation

An important problem that arises in the design and use of functional languages is the distinction between ordinary function applications and special forms. As we have already noted, in a language with an applicative order evaluation rule, such as Scheme and ML, all parameters to user-defined functions are evaluated at the time of a call, even though it may not be necessary to do so—or even wrong to do so.

Typical examples that do not use applicative order evaluation are the Boolean special forms and and or, as well as the if special form. In the case of the and special form, the Scheme expression (and a b) need not evaluate the parameter b if a evaluates to false. This is called short-circuit evaluation of Boolean expressions, and it is an example of the usefulness of delayed evaluation. In the case of the if special form, it is not a case of just usefulness, but of necessity; for the expression (if a b c) in Scheme to have the proper semantics, the evaluation of b and c must be delayed until the result of a is known, and based on that, either b or c is evaluated, but never both. For this reason, an if special form cannot be defined as a standard function in Scheme or ML. It also means that Scheme and ML must distinguish between two kinds of forms, those that use standard evaluation (function applications) and those that do not (the special forms).

A possible argument for restricting function evaluation to applicative order evaluation is that the semantics (and the implementation) are simpler. Consider the case of an expression in which one subexpression may have an undefined value, such as in the Scheme expression (and (< = 1 0) (= 1 (/ 1 0))) or its C equivalent (1 == 0) && (1 == 1 / 0). In this case, delayed evaluation can lead to a well-defined result, even though subexpressions or parameters may be undefined. Functions with this property are called **nonstrict**, and languages with the property that functions are strict are easier to implement. In essence, strict languages satisfy a strong form of the GIGO principle (garbage in, garbage out), in that they will consistently fail to produce results when given incomplete or malformed input. Strictness also has an important simplifying effect on formal semantics (as discussed in Chapter 12).

Nevertheless, as you have seen, nonstrictness can be a desirable property. Indeed, the argument in favor of nonstrictness is essentially identical to the argument against it. Nonstrict functions can produce results even in the presence of incomplete or malformed input—as long as there is enough information to make the result reasonable. It is interesting to note that the language Algol60 included delayed evaluation in its pass by name parameter passing convention, as will be discussed in detail in Chapter 10. According to pass by name evaluation, a parameter is evaluated only when it is actually used in the code of the called procedure. Thus, the function:

```
function p(x: boolean; y: integer): integer;
begin
  if x then p := 1
  else p := y;
end;
```

will, using pass by name evaluation, return the value 1 when called as p(true, 1 div 0), since y is never reached in the code of p, and so the value of y—the undefined expression 1 div 0—will never be computed.