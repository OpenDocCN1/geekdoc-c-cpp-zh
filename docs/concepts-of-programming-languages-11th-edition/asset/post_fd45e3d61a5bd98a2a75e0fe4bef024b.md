
function, which uses a parameter to accumulate the partial factorial. The helper function, which is tail recursive, also takes factorial's parameter. These functions are as follows:

```scheme
(DEFINE (facthelper n factpartial)
  (IF (<= n 1)
      factpartial
      (facthelper (- n 1) (* n factpartial))
  )
)
(DEFINE (factorial n)
  (facthelper n 1)
)
```

With these functions, the result is computed during the recursive calls, rather than as the recursion unwinds. Because there is nothing useful in the activation record instances, they are not necessary. Regardless of how many recursive calls are requested, only one activation record instance is necessary. This makes the tail-recursive version far more efficient than the non-tail-recursive version.

The Scheme language definition requires that Scheme language processing systems convert all tail-recursive functions to replace that recursion with iteration. Therefore, it is important, at least for efficiency's sake, to define functions that use recursion to specify repetition to be tail recursive. Some optimizing compilers for some functional languages can even perform conversions of some non-tail-recursive functions to equivalent tail-recursive functions and then code these functions to use iteration instead of recursion for repetition.

### 15.5.13 Functional Forms

This section describes two common mathematical functional forms that are provided by Scheme: composition and apply-to-all. Both are mathematically defined in Section 15.2.2.

#### 15.5.13.1 Functional Composition

Functional composition is the only primitive functional form provided by the original Lisp. All subsequent Lisp dialects, including Scheme, also provide it. As stated in Section 15.2.2, function composition is a functional form that takes two functions as parameters and returns a function that first applies the second parameter function to its parameter and then applies the first parameter function to the return value of the second parameter function. In other words, the function h is the composition function of f and g if h(x) = f(g(x)). For example, consider the following example:

```scheme
(DEFINE (g x) (* 3 x))
(DEFINE (f x) (+ 2 x))
```

Now the functional composition of f and g can be written as follows:

```scheme
(DEFINE (h x) (+ 2 (* 3 x)))
```

In Scheme, the functional composition function compose can be written as follows:

```scheme
(DEFINE (compose f g) (LAMBDA (x) (f (g x))))
```

For example, we could have the following:

```scheme
((compose CAR CDR) '((a b) c d))
```

This call would yield c. This is an alternative, though less efficient, form of CADR. Now consider another call to compose:

```scheme
((compose CDR CAR) '((a b) c d))
```

This call would yield (b). This is an alternative to CDAR.

As yet another example of the use of compose, consider the following:

```scheme
(DEFINE (third a_list)
  ((compose CAR (compose CDR CDR)) a_list))
```

This is an alternative to CADDR.

#### 15.5.13.2 An Apply-to-All Functional Form

The most common functional forms provided in functional programming languages are variations of mathematical apply-to-all functional forms. The simplest of these is map, which has two parameters: a function and a list. map applies the given function to each element of the given list and returns a list of the results of these applications. A Scheme definition of map follows:<sup>8</sup>

```scheme
(DEFINE (map fun a_list)
  (COND
    ((NULL? a_list) '())
    (ELSE (CONS (fun (CAR a_list)) (map fun (CDR a_list))))
  )
)
```

Note the simple form of map, which expresses a complex functional form.

As an example of the use of map, suppose we want all of the elements of a list cubed. We can accomplish this with the following:

```scheme
(map (LAMBDA (num) (* num num num)) '(3 4 2 6))
```

8. As was the case with member, map is a predefined function that cannot be redefined by users.

This call returns `(27 64 8 216)`. Note that in this example, the first parameter to `map` is a LAMBDA expression. When EVAL evaluates the LAMBDA expression, it constructs a function that has the same form as any predefined function except that it is nameless. In the example expression, this nameless function is immediately applied to each element of the parameter list and the results are returned in a list.

### 15.5.14 Functions That Build Code

The fact that programs and data have the same structure can be exploited in constructing programs. Recall that the Scheme interpreter uses a function named EVAL. The Scheme system applies EVAL to every expression typed, whether it is at the Scheme prompt in the interactive interpreter or is part of a program being interpreted. The EVAL function can also be called directly by Scheme programs. This provides the possibility of a Scheme program creating expressions and calling EVAL to evaluate them. This is not something that is unique to Scheme, but the simple forms of its expressions make it easy to create them during execution.

One of the simplest examples of this process involves numeric atoms. Recall that Scheme includes a function named `+`, which takes any number of numeric atoms as arguments and returns their sum. For example, `(+ 3 7 10 2)` returns 22.

Our problem is the following: Suppose that in a program we have a list of numeric atoms and need the sum. We cannot apply `+` directly on the list, because `+` can take only atomic parameters, not a list of numeric atoms. We could, of course, write a function that repeatedly adds the CAR of the list to the sum of its CDR, using recursion to go through the list. Such a function follows:

```lisp
(DEFINE (adder a_list)
  (COND
    ((NULL? a_list) 0)
    (ELSE (+ (CAR a_list) (adder (CDR a_list))))
  ))
```

Following is an example call to adder, along with the recursive calls and returns:

```lisp
(adder '(3 4 5))
(+ 3 (adder (4 5)))
(+ 3 (+ 4 (adder (5))))
(+ 3 (+ 4 (+ 5 (adder ()))))
(+ 3 (+ 4 (+ 5 0)))
(+ 3 (+ 4 5))
(+ 3 9)
12
```

An alternative solution to the problem is to write a function that builds a call to `+` with the proper parameter forms. This can be done by using CONS to build a new list that is identical to the parameter list except it has the atom + inserted at its beginning. This new list can then be submitted to EVAL for evaluation, as in the following:

```lisp
(DEFINE (adder a_list)
  (COND
    ((NULL? a_list) 0)
    (ELSE (EVAL (CONS '+ a_list)))
  )
)
```

Note that the + function's name is quoted to prevent EVAL from evaluating it in the evaluation of CONS. Following is an example call to this new version of adder, along with the call to EVAL and the return value:

```lisp
(adder '(3 4 5))
(EVAL (+ 3 4 5))
12
```

In all earlier versions of Scheme, the EVAL function evaluated its expression in the outermost scope of the program. The later versions of Scheme, beginning with Scheme 4, require a second parameter to EVAL that specifies the scope in which the expression is to be evaluated. For simplicity's sake, we left the scope parameter out of our example, and we do not discuss scope names here.

## 15.6 Common Lisp

Common Lisp (Steele, 1990) was created in an effort to combine the features of several early 1980s dialects of Lisp, including Scheme, into a single language. Being something of a union of languages, it is quite large and complex, similar in these regards to C++ and C#. Its basis, however, is the original Lisp, so its syntax, primitive functions, and fundamental nature come from that language. Following is the factorial function written in Common Lisp:

```lisp
(DEFUN factorial (n)
  (IF (<= n 1)
      1
      (* n (factorial (- n 1))))
)
```

Only the first line of this function differs syntactically from the Scheme version of the same function.

The list of features of Common Lisp is long: a large number of data types and structures, including records, arrays, complex numbers, and character strings; powerful input and output operations; and a form of packages for modularizing collections of functions and data, and also for providing access control. Common Lisp includes several imperative constructs, as well as some mutable types.
