```
(define procedure-parameter-name
(simple-generic-procedure 'parameter-name 1 (lambda (x) x)))
```

The procedure g:handle-operand allows us to choose how to process an operand based on the declarations of the corresponding formal parameter:

```
(define g:handle-operand
(simple-generic-procedure 'g:handle-operand 3
(lambda (parameter operand environment)
(g:advance g:eval operand environment))))
```

The default way to handle an operand without declarations is to evaluate the operand, as was previously done by eval-operands on page 245.

We need a syntax to allow us to decorate a formal parameter with declarations. Here we need to use a list beginning with the name of the formal parameter:

```
(define-generic-procedure-handler procedure-parameter-name
(match-args pair?))
```

We will start by implementing two kinds of declarations. The first is lazy, which means the operand is evaluated only when its value is needed, for example as the predicate of an if expression. The second is lazy memo, which is like lazy except that the first time the operand is evaluated, the value is remembered so that subsequent uses do not require reevaluation.

If a parameter is specified to be lazy (or lazy memoized) the evaluation of the operand must be postponed. The postponed expression must be packaged with the environment that will be used to give values to the free variables in that expression when its value is required.¹⁵

```
(define-generic-procedure-handler g:handle-operand
(match-args lazy? operand? environment?)
(lambda (parameter operand environment)
(postpone operand environment)))
```

```
(define-generic-procedure-handler g:handle-operand
(match-args lazy-memo? operand? environment?))
```