function, which uses a parameter to accumulate the partial factorial. The helper function, which is tail recursive, also takes factorial's parameter. These functions are as follows:

```
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
```

With these functions, the result is computed during the recursive calls, rather than as the recursion unwinds. Because there is nothing useful in the activation record instances, they are not necessary. Regardless of how many recursive calls are requested, only one activation record instance is necessary. This makes the tail-recursive version far more efficient than the non-tail-recursive version.

The Scheme language definition requires that Scheme language processing systems convert all tail-recursive functions to replace that recursion with iteration. Therefore, it is important, at least for efficiency's sake, to define functions that use recursion to specify repetition to be tail recursive. Some optimizing compilers for some functional languages can even perform conversions of some non-tail-recursive functions to equivalent tail-recursive functions and then code these functions to use iteration instead of recursion for repetition.

# ### 15.5.13 Functional Forms

This section describes two common mathematical functional forms that are provided by Scheme: composition and apply-to-all. Both are mathematically defined in Section 15.2.2.

# #### 15.5.13.1 Functional Composition

Functional composition is the only primitive functional form provided by the original Lisp. All subsequent Lisp dialects, including Scheme, also provide it. As stated in Section 15.2.2, function composition is a functional form that takes two functions as parameters and returns a function that first applies the second parameter function to its parameter and then applies the first parameter function to the return value of the second parameter function. In other words, the function h is the composition function of f and g if h (x) = f (g (x)) . For example, consider the following example:

```
```scheme
(DEFINE (g x) (* 3 x))
(DEFINE (f x) (+ 2 x))
```
```