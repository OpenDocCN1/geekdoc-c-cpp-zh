The tuple introduces an interesting phenomenon. How many parameters are in the function F(1,2,3)? There is the wrong answer. The function F takes only one parameter, whose type is a tuple, and the tuple is of type int*int*int. A function that takes three parameters is defined as F 1 2 3. A tuple can be used to group parameters together to make sure that related parameters are always passed into a function. For example, if you need to pass the first name and last name into a function it is better to declare g like this:

```
// indicate first name and last name provided together
g(firstName, lastName)
```

That way is better than the following approach:

```
// indicate first name and last name can be passed separately
g firstName lastName
```

The tuple supports structural equality. This means that the code shown in Listing 1-62 returns true. This concise syntax can make your code more readable.

# LISTING 1-62 The tuple structural equality

```
(1,2) = (1,2)
(1,2) = (1, 1+1)
(1,2) < (2, 4)
```

Forming a tuple can be as simple as putting all elements between a pair of parentheses, although parentheses are optional if omitting them does not introduce confusion. Retrieving the elements requires two functions: the fst and snd functions are used to retrieve the first and the second elements, respectively, from a tuple. See Listing 1-63.

# LISTING 1-63 The fst and snd functions in a tuple

```
// define tuple without parentheses
let a = 1, 2
let b = 1, "two"

// get first element in a tuple
let isOne = fst a

// get second element in a tuple
let isTwo = snd b
```