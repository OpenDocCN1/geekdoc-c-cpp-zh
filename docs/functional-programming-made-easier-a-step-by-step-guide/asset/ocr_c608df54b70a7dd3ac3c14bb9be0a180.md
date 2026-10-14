# 15.12. Writing a Moore Machine that Folds

Instead of writing a Function that takes an Array of Ints and adds them up, simply write a Function that models or defines this operation using Moore. Eventually, we'll write a Function to execute this definition.

Call the Function, addr and give it a try before reading ahead.

# 15.13. Code for addr

As usual, we start with the Type Signature:

```
--     Moore s a b
addr :: Moore Int Int Int
```

Here the first Parameter to Moore, our State, is an Int since it's the Accumulator of our sum.

The second Parameter is an Int, i.e. each element of our Foldable is an Int.

The third Parameter is also an Int, i.e. after adding up all the Ints we expect an Int as our result.

Before, we add the code, let's look at the Moore Data Constructor:

```
data Moore s a b = Moore s (s -> b) (s -> a -> s)
```

So we'll have to write something like:

```
addr :: Moore Int Int Int
addr = Moore ??? ??? ???
```

The first Parameter to the Data Constructor is the Initial State. That will be 0 for our addr.

```
addr :: Moore Int Int Int
addr = Moore 0 ??? ???
```

The second Parameter of the Data Constructor is the output function which converts the Final State to our result. But the Final State is the sum, which is exactly what we want. So we don't need to process it, which means we can use identity here:

```
addr :: Moore Int Int Int
addr = Moore 0 identity ???
```