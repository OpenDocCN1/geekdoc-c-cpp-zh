
assignment to particular sensitive locations in the address space). In Scheme we allow a program to assign to a variable in the lexical environment of the assignment statement:

```
(define-generic-procedure-handler g:eval
 (match-args assignment? environment?)
  (lambda (expression environment)
    (set-variable-value! (assignment-variable expression)
      (g:eval (assignment-value expression)
        environment))))
```

The syntax for assignment is:

```
(define (assignment? exp) (tagged-list? exp 'set!))
(define (assignment-variable assn) (cadr assn))
(define (assignment-value assn) (caddr assn))
```

We also allow definition, the creation of a new variable with a given value. A definition creates a new variable in the most local lexical environment frame of the definition statement.

```
(define-generic-procedure-handler g:eval
 (match-args definition? environment?)
  (lambda (expression environment)
    (define-variable! (definition-variable expression)
      (g:eval (definition-value expression)
        environment))
    (definition-variable expression)))
```

The syntax for definitions is more complicated than the syntax for assignment, because we allow multiple ways to define a procedure:

```
(define (definition? exp) (tagged-list? exp 'define))
```

```
(define (definition-variable defn)
 (if variable? (cadr defn)                ; (DEFINE foo ...)
  (cadr defn))
  (caddr defn))                             ; (DEFINE (foo ...)))
```

```
(define (definition-value defn)
 (if variable? (cadr defn)                ; (DEFINE foo ...)
  (caddr defn))
  (cons 'lambda                             ; (DEFINE (foo p...) b...)))
```

```
(cons (cdadr defn) ; =(DEFINE foo
(cddr defn))); ; (LAMBDA (p...) b...))
```

This completes the usual list of special forms that define the syntax of the language. Of course, the generic procedure implementation enables creation of new special forms easily, allowing the language to grow to make it more convenient to express computational ideas that were not well supported in the base language. A language with many different syntactic constructs may be difficult to learn, document, and use; this is a classic engineering tradeoff (remember Alan Perlis's maxim on page 159).

## 5.1.2 apply

The traditional Scheme apply takes two arguments, the procedure to be applied and the evaluated arguments to be passed to the procedure. This is sufficient for Scheme, because Scheme is a strict applicative-order language with only lexically scoped variables.

By generalizing apply to take three arguments—the unevaluated operands and the calling environment—we make possible to include procedures that require normal-order evaluation for some parameters (e.g., call by need) or procedures that make declarations on parameters, such as types and units. We will make some extensions like these in section 5.2. The environment argument also makes it possible to accommodate non-lexically scoped variables, but we will not do so; it is generally a bad idea. We will start out with Scheme applicative-order, with generic hooks for extension.

Our apply is a generic procedure with three arguments:

```
(define g:apply)
(simple-generic-procedure 'apply 3 default-apply))

(define (default-apply procedure operands calling-environment)
(error "Unknown procedure type"))
```

We need handlers for the various kinds of procedures. Some procedures, like arithmetic addition (usually named by the + operator), are strict: they need all of their arguments evaluated before they can compute a value. In Scheme all procedures are strict, including primitive procedures (implemented in the system or hardware below the level of the language). So we need a generic handler for strict primitives:

```
(define-generic-procedure-handler g:apply
(match-args strict-primitive-procedure?)
  operands?
  environment?)
  (lambda operands calling-environment)
  (apply-primitive-procedure procedure
    (eval-operands operands calling-environment)))
```

The application of a primitive procedure is "magic" at this level of detail. The operands evaluator, like if on page 238, must call g:advance on the result of evaluation to ensure a value.

```
(define (eval-operands operands calling-environment)
  (map (lambda g:eval calling-environment)
    (g:advance g:eval calling-environment))
  operands))
```

Note that the order of evaluation of the operands is determined by the behavior of map.

Procedures constructed by evaluating lambda expressions are not primitive. Here we can take apart the procedure. We can grab the formal parameter specifications, which are the names of the formal parameters. We also can extract the body of the procedure, which we pass to eval with an environment that includes the formal parameter bindings. For lexical scoping, that extended environment is built on the environment packaged with the procedure by the evaluation of the lambda expression that constructed the procedure.

```
(define-generic-procedure-handler g:apply
(match-args strict-compound-procedure?)
  operands?
  environment?)
  (lambda operands calling-environment)
  (if (not (= (length (procedure-parameters procedure))
      (length operands)))
    "Wrong number of operands supplied")
    (g:eval (procedure-body procedure)
      (extend-environment)
      (procedure-parameters procedure)
      (eval-operands operands calling-environment)
      (procedure-environment procedure))))
```

Here strict-compound-procedure? is true of all compound procedures that have no declarations on any of their parameters.

## Driver loop

To interact with this evaluator we need a read-eval-print loop:

```
(define repl)
  (check-repl-initialized)
  (let ((input (g:read))
    (write-line g:eval input the-global-environment)
    (repl)))
```

Here g:read issues a prompt, eval, on the terminal. It accepts characters and parses them, converting what it gets into an s-expression. That s-expression is then evaluated with g:eval with respect to the-global-environment and the result is written back to the terminal. The procedure repl calls itself recursively. For this to work, the global environment must be initialized:

```
(define the-global-environment)
  'not-initialized)
```

```
(define initialize-repl!)
  (set! the-global-environment (make-global-environment))
  'done
```

```
(define check-repl-initialized)
  (if eq? the-global-environment 'not-initialized)
    error
    "Interpreter not initialized. Run (init) first."))
```

This completes the elementary evaluator.

# Exercise 5.1: Unbound-variable handling

In Lisps, including Scheme, attempting to evaluate an unbound symbol is an unbound-variable error. However, in some algebraic processes it is often sensible to allow an unbound symbol to be self-evaluating. For example, if we generically extend arithmetic to build expressions with symbolic values, as we did in chapter 3, it is sometimes useful to allow the following:

```
(+ * 2 3) (* 4 5))
(+ * a 3) (* 4 5))
(+ * a 3) 20
```

Our generic arithmetic supported symbolic extensions: the operators * and + were extended to build expressions when the arguments were not reducible to numbers. But it did not allow the use of unbound variables as literal numbers. Here the symbol a is unbound. We may want it to be self-evaluating.

- a. Make a generic extension to eval to allow this kind of behavior. To make this work with the numerical primitives (+ *, /) it is necessary to extend their behavior as well. Note that these operators should be changed in the underlying Scheme environment. As in chapter 3, the generic operator mechanism may be given handlers that work in the underlying Scheme system.

- b. Also augment apply to allow unbound symbols in the operator position to be interpreted as literal functions, known only by their names: (+ f 3) (* 4 5) => (+ f 3) 20

These extensions to eval and apply are generally dangerous, because they hide real unbound-variable errors. Make them contingent on the value of a user-settable variable: allow-self-evaluating-symbols.

# Exercise 5.2: n-ary procedures

Footnote 10 on page 246 points out a nasty assumption that we put into the g:apply handler that implies a restriction on the future expansion of this evaluator. In Scheme, if the procedure-
