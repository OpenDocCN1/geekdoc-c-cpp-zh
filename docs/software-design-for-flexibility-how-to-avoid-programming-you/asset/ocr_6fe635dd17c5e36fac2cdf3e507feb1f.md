procedure (using eval) in an environment in which the formal parameters of the procedure are bound to the arguments. This is the central computational loop of the interpreter.

What we just described is the traditional applicative-order interpreter plan. In our interpreter we will pass the unvaluated operands and the environment for their evaluation to apply to make it possible to implement a variety of evaluation strategies, as normal order as well as applic order.

The language we will be implementing is a Lisp variant. This implies that the code is expressed as list structures. In Lisp all compound expressions are lists, some of which start with distinguished keywords. Compound expressions that have distinguished keywords are called special forms. The compound expressions that are not special forms are interpreted as applications of procedures to arguments. The implementation will be organized as a set of rules for each expression type, with the exception of applications, which are distinguished by not being special forms. With each rule we give the syntactic definition of the expression type. This strategy can be used to implement any language, though a new parser would be needed. With Lisp the reader converts the character-string input into list structures, which are natural representations of the abstract syntax tree (AST) of the language. With other languages the AST is more elaborate and the parser is much more complicated.

# 5.1.1 eval

We define g:eval as a generic procedure with two arguments.

```
(define g:eval
(simple-generic-procedure `eval 2 default-eval))
```

The default case for eval is an application (sometimes described as a combination).

```
(define (default-eval expression environment)
  (cond ((application? expression))
    (g:apply (g:advance)
           (g:eval (operator expression)
            environment))
          (operands expression)))
```