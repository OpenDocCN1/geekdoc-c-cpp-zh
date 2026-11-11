In this case, however, because of Haskell’s support for polymorphism, this function can take a parameter of any numeric type. As with ML, lists are written in brackets in Haskell, as in

```
colors = ["blue", "green", "red", "yellow"]
```

Haskell includes a collection of list operators. For example, lists can be concatenated with ++, : serves as an infix version of CONS, and .. is used to specify an arithmetic series in a list. For example,

```
5:[2, 7, 9] results in [5, 2, 7, 9]
[1, 3..11] results in [1, 3, 5, 7, 9, 11]
[1, 3, 5] ++ [2, 4, 6] results in [1, 3, 5, 2, 4, 6]
```

Notice that the : operator is just like ML’s :: operator. Using : and pattern matching, we can define a simple function to compute the product of a given list of numbers:

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
            sqrt (b ^ 2 - 4.0 * a * c) / (2.0 * a)
    in
        minus_b_over_2a - root_part_over_2a,
        minus_b_over_2a + root_part_over_2a
```

Haskell’s list comprehensions were introduced in Chapter 6. For example, consider the following:

```
[n * n * n | n <- [1..50]]
```

This defines a list of the cubes of the numbers from 1 to 50. It is read as “a list of all n*n*n such that n is taken from the range of 1 to 50.” In this case, the qualifier is in the form of a generator. It generates the numbers from 1 to 50. In other