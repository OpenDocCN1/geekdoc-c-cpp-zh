![](bbox=[0.279, 0.059, 0.721, 0.281])

Here go returns a List but init returns a Maybe. We need to add the Data Constructor for Maybe, i.e we need to add Just to our call to go turning a List into a Maybe List:

```
init :: ∀ a. List a -> Maybe (List a)
init Nil = Nothing
init l = Just $ go l where      -- COMPILER ERROR!! ①
  go (_ : Nil) = Nil
  go (x : xs) = x : go xs
```

① Now init l returns a Maybe List. Note the use of $ instead of Parentheses.

And once again, we have a different error:

![](bbox=[0.279, 0.56, 0.721, 0.727])

This error says that we're missing a case for go when the List is empty, i.e. Nil.

This may seems wrong at first since we know that go will never get an empty List. Why? Because we will never initially call it with an empty List and we'll terminate our recursion when the list has only 1 element in it.

But the problem is that the compiler doesn't know any of this. There is a non-empty List Type in PureScript that we haven't learned about yet, but that would unnecessarily complicate this particular Function.

So the easiest thing to do is just add that case to appease the compiler, even though we know it will never be executed.