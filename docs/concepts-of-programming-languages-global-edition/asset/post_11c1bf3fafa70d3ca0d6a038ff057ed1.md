
arrays). Both nonstrict semantics and function overloading are further discussed later in this section.

The code in this section is written in version 1.4 of Haskell.

Consider the following definition of the factorial function, which uses pattern matching on its parameters:

```
fact 0 = 1
fact 1 = 1
fact n = n * fact (n - 1)
```

Note the differences in syntax between this definition and its ML version in Section 15.7. First, there is no reserved word to introduce the function definition (fun in ML). Second, alternative definitions of functions (with different formal parameters) all have the same appearance.

Using pattern matching, we can define a function for computing the nth Fibonacci number with the following:

```
fib 0 = 1
fib 1 = 1
fib (n + 2) = fib (n + 1) + fib n
```

Guards can be added to lines of a function definition to specify the circumstances under which the definition can be applied. For example,

```
fact n
  | n == 0 = 1
  | n == 1 = 1
  | n > 1 = n * fact(n - 1)
```

This definition of factorial is more precise than the previous one, for it restricts the range of actual parameter values to those for which it works. This form of a function definition is called a conditional expression, after the mathematical expressions on which it is based.

An otherwise can appear as the last condition in a conditional expression, with the obvious semantics. For example,

```
sub n
  | n < 10    = 0
  | n > 100   = 2
  | otherwise = 1
```

Notice the similarity between the guards here and the guarded commands discussed in Chapter 8.

Consider the following function definition, whose purpose is the same as the corresponding ML function in Section 15.7:

```
square x = x * x
```

In this case, however, because of Haskell’s support for polymorphism, this function can take a parameter of any numeric type.
As with ML, lists are written in brackets in Haskell, as in

```
colors = ["blue", "green", "red", "yellow"]
```

Haskell includes a collection of list operators. For example, lists can be catenated with ++, : serves as an infix version of CONS, and .. is used to specify an arithmetic series in a list. For example,

```
5:[2, 7, 9] results in [5, 2, 7, 9]
[1, 3..11] results in [1, 3, 5, 7, 9, 11]
[1, 3, 5] ++ [2, 4, 6] results in [1, 3, 5, 2, 4, 6]
```

Notice that the : operator is just like ML’s :: operator.11 Using : and pattern matching, we can define a simple function to compute the product of a given list of numbers:

```
product [] = 1
product (a:x) = a * product x
```

Using product, we can write a factorial function in the simpler form

```
fact n = product [1..n]
```

Haskell includes a let construct that is similar to ML’s let and val. For example, we could write

```
quadratic_root a b c =
    let minus_b_over_2a = - b / (2.0 * a)
        root_part_over_2a =
            sqrt(b ^ 2 - 4.0 * a * c) / (2.0 * a)
    in
        minus_b_over_2a - root_part_over_2a,
        minus_b_over_2a + root_part_over_2a
```

Haskell’s list comprehensions were introduced in Chapter 6. For example, consider the following:

```
[n * n * n | n <- [1..50]]
```

This defines a list of the cubes of the numbers from 1 to 50. It is read as “a list of all n*n*n such that n is taken from the range of 1 to 50.” In this case, the qualifier is in the form of a generator. It generates the numbers from 1 to 50. In other

> 11. It is interesting that ML uses : for attaching a type name to a name and :: for CONS, while Haskell uses these two operators in exactly opposite ways.

cases, the qualifiers are in the form of Boolean expressions and they are called tests. This notation can be used to describe algorithms for doing many things, such as finding permutations of lists and sorting lists. For example, consider the following function, which when given a number n returns a list of all its factors:

```
factors n = [ i | i <- [1..n `div` 2], n `mod` i == 0]
```

The list comprehension in factors creates a list of numbers, each temporarily bound to the name i, ranging from 1 to n/2, such that n `mod` i is zero. This is indeed a very exacting and short definition of the factors of a given number. The backticks (backward apostrophes) surrounding div and mod are used to specify the infix use of these functions. When they are called in functional notation, as in div n 2, the backticks are not used.

Next, consider the concision of Haskell illustrated in the following implementation of the quicksort algorithm:

```
sort [] = []
sort (h:t) = sort [b | b <- t, b <= h]
            ++ [h] ++
               sort [b | b <- t, b > h]
```

In this program, the set of list elements that are smaller or equal to the list head are sorted and catenated with the head element, then the set of elements that are greater than the list head are sorted and catenated onto the previous result. This definition of quicksort is significantly shorter and simpler than the same algorithm coded in an imperative language.

A programming language is strict if it requires all actual parameters to be fully evaluated, which ensures that the value of a function does not depend on the order in which the parameters are evaluated. A language is nonstrict if it does not have the strict requirement. Nonstrict languages can have several distinct advantages over strict languages. First, nonstrict languages are generally more efficient, because some evaluation is avoided.12 Second, some interesting capabilities are possible with nonstrict languages that are not possible with strict languages. Among these are infinite lists. Nonstrict languages can use an evaluation form called lazy evaluation, which means that expressions are evaluated only if and when their values are needed.

Recall that in Scheme the parameters to a function are fully evaluated before the function is called, so it has strict semantics. Lazy evaluation means that an actual parameter is evaluated only when its value is necessary to evaluate the function. So, if a function has two parameters, but on a particular execution of the function the first parameter is not used, the actual parameter passed for that execution will not be evaluated. Furthermore, if only a part of an actual parameter must be evaluated for an execution of the function, the rest is left

unevaluated. Finally, actual parameters are evaluated only once, if at all, even if the same actual parameter appears more than once in a function call.

As stated previously, lazy evaluation allows one to define infinite data structures. For example, consider the following:

```
positives = [0..]
evens = [2, 4..]
squares = [n * n | n <- [0..]]
```

Of course, no computer can actually represent all of the numbers of these lists, but that does not prevent their use if lazy evaluation is used. For example, if we wanted to know if a particular number was a perfect square, we could check the squares list with a membership function. Suppose we had a predicate function named member that determined whether a given atom is contained a given list. Then we could use it as in...

```
member 16 squares
```

which would return True. The squares definition would be evaluated until the 16 was found. The member function would need to be carefully written. Specifically, suppose it were defined as follows:

```
member b [] = False
member b (a:x) = (a == b) || member b x
```

The second line of this definition breaks the first parameter into its head and tail. Its return value is true if either the head matches the element for which it is searching (b) or if the recursive call with the tail of the list returns True.

This definition of member would work correctly with squares only if the given number were a perfect square. If not, squares would keep generating squares forever, or until some memory limitation was reached, looking for the given number in the list. The following function performs the membership test of an ordered list, abandoning the search and returning False if a number greater than the searched-for number is found.13

```
member2 n (m:x)
  | m < n     = member2 n x
  | m == n    = True
  | otherwise = False
```

Lazy evaluation sometimes provides a modularization tool. Suppose that in a program there is a call to function f and the parameter to f is the return value of a function g.14 So, we have f(g(x)). Further suppose that g produces a large amount of data, a little at a time, and that f must then process this data,

13. This assumes that the list is in ascending order.

14. This example appears in Hughes (1989).
