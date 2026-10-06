If the third or fourth element is needed, the functions defined in Listing 1-64 can be used. The underscore (_) stands for a placeholder where the value can be ignored. You'll find the underscore used in other places as well. It's a way to tell the F# compiler that this is something you don't care about.

# LISTING 1-64 The third and fourth functions in a tuple

```
// get the third value of the triple
let third (_,c) = c

// get the fourth value of the quadruple
let fourth (_,_,d) = d

third (1,2,3) // return 3
fourth (1,2,3,4) // return 4
```

There is another way to retrieve the embedded elements without using these functions.
Listing 1-65 shows how the F# compiler figured out that the element in l is a triple. The variables a, and c are used to hold the element values in the triple.

# LISTING 1-65 Use let and iterating through a triple list

```
let tripleVariable = 1, "two", "three"
let a, b, c = tripleVariable

let l = [(1,2,3), (2,3,4), (3,4,5)]
for a,b,c in l
printf "triple is (%%%d,%d,%d)" a b c
```

# Functions

If you want to refactor the F# code in the conversion task, one way is to define a function that checks whether a given number is odd. Defining a function is a simple task for an experienced C# developer. Most likely, you already figured out how to write out an F# function. One thing you want to point out is that F# does not have a return keyword. As a result, the value from the last expression is always the returned value. The following defining operation increments a generic integer by

```
let increaseOne x = x + 1
```

If you run the code in FSI, the result shows that the function takes an integer as input and returns an integer as output. The result might look strange, but it's still understandable:

```
val increaseOne : int -> int
```