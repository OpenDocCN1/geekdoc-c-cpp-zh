❶ A Lambda that takes 2 Parameters and returns a record populated with the values from those Parameters.

❷ This is the Wildcard equivalent of the previous line. It’s very important that the order of Parameters is maintained, i.e. the first Wildcard encountered from Left to Right is the first Parameter, the second Wildcard is the second Parameter and so on.

Record updates can also have Wildcards:

```
\name age -> person { name = name, age = age } ❶
person { name = _, age = _ } ❷
```

❶ Here’s a Lambda that takes a person and updates 2 of it’s fields (person could have more than just 2 fields) and returns a new Record with just those 2 fields modified. Remember, there are no mutations, so person is unchanged.

❷ The same can be accomplished with Wildcards using this syntax.

Another Wildcard example for updates:

```
\person -> person { age = 18 } ❶
_ { age = 18 } ❷
```

❶ The Lambda takes a person and updates the age returning a new Record.

❷ The Wildcard equivalent. This syntax looks odd at first.

# 3.6. Bindings

We have 2 ways to bind Values to variables. (Don’t forget, Functions are also Values in Functional Programming.)

# 3.6.1. Where

The keyword where allows us to define things after the fact in a Function definition:

```
multSum :: Int -> Int -> Tuple Int Int ❶
multSum x y = Tuple mult sum ❷
  where
    mult = x * y ❸ ❺
    sum = x + y ❹ ❺
```

❶ multSum takes 2 Ints and returns a Tuple of Ints.

❷ Variables mult and sum are used here but have not been defined yet.