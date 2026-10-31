```
> # Double-quotes
[1] "one" "two" "three" "four" "five"
> 
> c('one', 'two', 'three', 'four', 'five')
> # Single-quotes
[1] 'one' 'two' 'three' 'four' 'five'
> 
> c("one", "two", "three", "four", "five")
> # Mixed-quotes
[1] "one" 'two' "three" 'four' "five"
```

However, if there is a mixed pair of quotes such as "xxxx," it will not be accepted. For example:

```
> c("one", "two", "three", "four", "five")
```

b) A logical vector, which takes the value TRUE or FALSE (or NA). For inputs, one may use the abbreviations T or F.

These vectors are similarly specified using the c function:

```
> c(T, F, T, F, T)
[1] TRUE FALSE TRUE FALSE TRUE
```

In most cases, there is no need to specify repeated logical vectors. It is acceptable to use a single logical value to provide the needed options, as vectors of more than one value will respond in terms of relational expressions. Observe

```
> weight <- c(73, 59, 97)
> height <- c(1.79, 1.64, 1.73)
> bmi <- weight/height^2
> bmi # Outputting:
[1] 22.78331 21.93635 32.41004
> bmi > 25 # A single logical value will suffice!
[1] FALSE FALSE TRUE
>
```

# 4.3.7 Some Special Functions that Create Vectors

Three functions that create vectors are c, seq, and rep

+   1) c for "concatenate", or the joining of objects end-to-end (this was introduced earlier) – for example

```
> x <- c(1, 2, 3, 4) # x is assigned to be a 4-vector.
```