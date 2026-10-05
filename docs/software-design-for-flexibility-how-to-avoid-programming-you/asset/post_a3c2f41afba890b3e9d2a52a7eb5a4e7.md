
```
(term (car terms)) rest2 (cdr terms))
(cond ((and (match:element-var? term)
      (match:vars-equal? var term))
      (succeed dict fail rest1 rest2))
  (match:has-binding? var dict)
  ((unify:dispatch
    (cons (match:get-value var dict) rest1
    terms))
    (succeed dict))
  else
  (let ((dict* (do-substitute var term dict))
    (if dict*
        (succeed dict* fail rest1 rest2)
        (fail)))))
```

In-substitute we first use the old dictionary to clean the incoming term by replacing any previously eliminated variables with their values. Then we check if there are any restrictions on what objects may match. Finally we check for any occurrences of var in the cleaned term (term*). If the cleaned term contains a reference to var, the match cannot proceed.8 If our match passes all tests, we make a new dictionary that includes the new binding of var to the cleaned term. The binding values in the new dictionary must also be cleaned of references to var.

```
(define (do-substitute var term dict)
(let ((term* (match:dict-substitution dict term))
(and (match:satisfies-restriction? var term*))
  (or (and (match:var? term*)
      (match:vars-equal? var term*))
  (not (match:occurs-in? var term*))
  (match:extend-dict var term*))
(match:map-dict-values
(match:single-substitution var term*)))
dict)))))
```

Now that we know how to handle variables we have to install this handler in our generic dispatcher procedure. The only subtlety here is that the variable to be eliminated may appear in either term list. We guarantee that the term list containing the variable is the first argument to maybe-substitute.

```
(define element? term)
(any-object? term))

(define-generic-procedure-handler unify:gdispatch
(match-args car-satisfies match:element-var?)
(car-satisfies element?))
(lambda var-first terms)
(maybe-substitute var-first terms)))

(define-generic-procedure-handler unify:gdispatch
(match-args car-satisfies element?)
(car-satisfies match:element-var?))
(lambda terms var-first)
(maybe-substitute var-first terms))
```

At this point we have a complete, correct, and competent traditional unifier. It is written with generic procedures, so it can easily be extended to work with other kinds of data. And with only a small amount of work we can add semantic attachments, such as the commutativity of lists beginning with the symbols + and *. As we shall see, we can also support for new kinds of syntactic variables, such as segment variables. But before we do that we will look at a real application: type inference.

## Exercise 4.10: Unifying vectors

This unifier can be extended to handle data and patterns that are made of other data types, such as vectors. Make handlers for vectors without transforming the vectors to lists (the easy way out!).

## Exercise 4.11: Unifying strings

Extend the unifier to allow unification of strings. This could be fun, but you need to invent a syntactic mechanism for representing string variables inside a string. This is pretty delicate, because you may have to represent a string variable with a string expression. This gets into quotation problems—please try not to invent a baroque mechanism. Also, make sure that you don't make assumptions that will prevent you from introducing string segment variables later. (See exercise 4.21 on page 209.)

## Exercise 4.12: Variable restrictions

We added support for restrictions on variables as we did in the one-sided matcher: we just put a clause for that into the main conditional in the procedure do-substitute. But there are subtle problems.

- What should happen if a restricted variable is matched against another restricted variable?
- When the variable is first bound to its target, after passing the restriction, it is uniformly eliminated. But the restriction is lost, preventing it from killing an unsuitable later part of the match.

Your task is to understand these problems and determine how to ameliorate them. How important could this be for any applications you might consider? Is there a solution that fits nicely into our implementation strategy?

## Exercise 4.13: Unifying with pattern combinators?

Unlike our earlier one-sided pattern matcher, our unification matcher does not compile the patterns into match procedures that combine to build a match procedure for the pattern. A system of match procedures is potentially more efficient, because it avoids the syntactic analysis of the patterns while matching. Can the unification matcher be broken up in a similar way? If not, why not? Is it a good idea to do so? If not, why not? If so, do it! (This is hard!)

## 4.4.2 Application: Type inference

One classic application of unification matching is type inference: given a program and some type information about parts of the program, deduce type information about other parts of the program. For example, if we know that < is a procedure that takes two numerical arguments and produces a boolean value, then if we analyze the expression (g x y)), we can deduce that f and g are unary procedures; g accepts a boolean argument; f returns a numerical value; and x has a numerical value. If this information is used to deduce properties of the program that the expression is embedded in, we can learn a great deal about the program. Here is an analysis of the expression:

```
pp (infer-program-types '(g (< x y)))
(t type:17)
(t (type:procedure ((boolean-type)) ? type:17)) g)
(t (boolean-type)
(t (type:procedure (numeric-type) (numeric-type))
(boolean-type))
<
(t (numeric-type) x)
(t (numeric-type)
(t (type:procedure (? y:12) (numeric-type)) f)
(t (? y:12) y))))
```

This is the abstract tree of the given expression, annotated with types. Each subexpression x has been expanded into a typed expression of the form (t type x). For example, the reference to g has the type:

```
(type:procedure ((boolean-type)) ? type:17)
```

As expected, g is a procedure that accepts a boolean argument, but we have no information about its value. The unknown value type is represented by the pattern variable (? type:17).
Let's consider a more substantial example:

```
(pp (infer-program-types '(g (< x y)))
(t type:17)
(t (type:procedure ((boolean-type)) ? type:17)) g)
(t (boolean-type)
(t (type:procedure (numeric-type) (numeric-type))
(boolean-type))
<
(t (numeric-type) x)
(t (numeric-type)
(t (type:procedure (? y:12) (numeric-type)) f)
(t (? y:12) y))))
```

The result in foo is rather verbose. So we look at it with a simplifier that puts it into “human readable” form.

```
(define fact
(lambda n)
  begin
    (define iter
      (if (= n 0)
        1
        (* n (iter (- n 1))))
```

Here we see that the type inference program was able to determine the complete type of the factorial program–that it is a procedure that takes one numerical input and produces a numerical output. This is reported in a declaration:

```
(declare-type fact
  (type:procedure ((numeric-type)) (numeric-type)))
```

The type of the internal definition iter has also been determined: it takes numerical arguments and produces a numerical result.

```
(declare-type iter
  (type:procedure ((numeric-type) (numeric-type)) (numeric-type)))
```

Also, the type of each internal variable has been determined, and an appropriate declaration has been posted:

```
(declare-type n (numeric-type))
(declare-type product (numeric-type))
(declare-type counter (numeric-type))
```

## 4.4.3 How type inference works

The process of type inference has four phases.

- 1. The given program is annotated with type variables for all subexpressions of the program.
- 2. Constraints on the type variables are formulated based on the semantic structure of the program.
- 3. The constraints are unified to eliminate as many of the variables as possible.
- 4. The annotated program is specialized using the dictionary produced by unification of the constraints to make a new annotated program whose type annotations incorporate the constraints.

The plan is implemented in this procedure:

```
(define (infer-program-types expr)
  (let ((texpr (annotate-program expr))
    (let ((constraints (program-constraints texpr)))
      (let ((dict (unify-constraints constraints)))
        (if dict
          (match:dict-substitution dict) texpr)
          ***type-error***))))))
```

This procedure complains if the program expression cannot be consistently typed. However, it gives no explanation about why it failed; this could be accomplished by passing information back in the failure continuations.

# Annotation

The annotate-program procedure is implemented in terms of a generic procedure, annotate-expr, to allow easy extension for new language features.
