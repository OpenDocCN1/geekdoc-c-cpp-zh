the CAR of the first parameter list is CONSED onto the result returned by the recursive call, which passes the CDR of the first list as its first parameter.

Consider the following Scheme function, named `guess`, which uses the `member` function described in this section. Try to determine what it does before reading the description that follows it. Assume the parameters are simple lists.

```
```scheme
(DEFINE (guess list1 list2)
  (COND
    ((NULL? list1) '())
    ((member (CAR list1) list2)
        (CONS (CAR list1) (guess (CDR list1) list2)))
    (ELSE (guess (CDR list1) list2))
  )
)
```
```

`guess` yields a simple list that contains the common elements of its two parameter lists. So, if the parameter lists represent sets, `guess` computes a list that represents the intersection of those two sets.

# 15.5.11 LET

LET is a function (initially described in Chapter 5) that creates a local scope in which names are temporarily bound to the values of expressions. It is often used to factor out the common subexpressions from more complicated expressions. These names can then be used in the evaluation of another expression, but they cannot be rebound to new values in LET. The following example illustrates the use of LET. It computes the roots of a given quadratic equation, assuming the roots are real. The mathematical definitions of the real (as opposed to complex) roots of the quadratic equation ax² + bx + c are as follows: root1 = (−b + sqrt(b² − 4ac))/2a and root2 = (−b − sqrt(b² − 4ac))/2a

```
```scheme
(DEFINE (quadratic_roots a b c)
  (LET (
    (root_part_over_2a
      (/ (SQRT (- (* b b) (* 4 a c))) (* 2 a)))
    (minus_b_over_2a (/ (- 0 b) (* 2 a)))
  )
  (LIST (+ minus_b_over_2a root_part_over_2a)
        (- minus_b_over_2a root_part_over_2a))
))
```
```

This example uses LIST to create the list of the two values that make up the result.

Because the names bound in the first part of a LET construct cannot be changed in the following expression, they are not the same as local variables in

7. Some versions of Scheme include "complex" as a data type and will compute the roots of the equation, regardless of whether they are real or complex.