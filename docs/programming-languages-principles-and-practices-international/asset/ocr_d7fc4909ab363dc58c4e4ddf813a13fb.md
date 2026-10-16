To give the flavor of this idea, let’s examine how a Scheme programmer might process a **let** expression if Scheme did not include **let** as a built-in special form. Recall that **let** allows the interpreter to evaluate an expression within a new environment created by binding a set of temporary variables to their values. A close inspection, however, shows that the **let** form is actually just syntactic sugar for the application of a **lambda** form to its arguments. Figure 3.9 shows examples of a **let** expression and a **lambda** application that have the same semantics.

```
```scheme
(let ((a 3) (b 4))
  (* a b))

((lambda (a b) (* a b)) 3 4)
```
```

**Figure 3.9** **let** as syntactic sugar for the application of **lambda**

As you can see, the temporary variables of the **let** become the formal parameters of the **lambda**, and their initial values become the arguments of the **lambda**’s application. The body of the **let** becomes the body of the lambda.

The process of interpreting a **let** form that is not built-in involves two steps. First, we treat the **let** form as a datum (a list) to be transformed into another datum (another list) that represents the equivalent **lambda** application. Second, we evaluate the new representation. If we assume that there exists a function, **let-to-app**, that performs the required syntactic transformation, then we can apply the Scheme function **eval** to the result to evaluate it, as follows:

```
```scheme
> (eval (let-to-app ‘(let ((a 3) (b 4))(* a b))))
```
```

Note that we quote the argument of **let-to-app**, the **let** expression, to treat it as data (a list of elements). We then use **eval** to force evaluation of the result of **let-to-app**, which is another list of elements representing the application of the **lambda**.

The remaining task is to define the function **let-to-app**, which transforms any **let** expression to the corresponding **lambda** application. Our implementation makes use of several list-processing functions and the quote of a symbol. The comments indicate the phrases of code extracted from the **let** form and added to the list representing the application under construction:

```
```scheme
(define let-to-app (lambda (let-form)
  (append (list                         ; begin the app
             (list ‘lambda               ; begin the lambda
                   (map car (cdr let-form)) ; formal parameters
                   (caddr let-form)))     ; lambda body
        (map cadr let-form))))          ; argument expressions
```
```

Alternatively, we could define the syntactic forms of our new language if they are not already built in) using a macro facility as mentioned in Chapter 2. Then the programmer using the new forms would not have to quote them and explicitly evaluate them with **eval**. Upon encountering the new forms, the Scheme compiler would automatically perform the required syntactic transformations and generate code that is evaluated in the usual manner at runtime.