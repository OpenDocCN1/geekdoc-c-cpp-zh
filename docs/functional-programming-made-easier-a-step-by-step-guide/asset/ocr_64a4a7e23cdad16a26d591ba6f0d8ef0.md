① Don’t forget the Just. Also, we don’t name the tail, i.e. _, here because we don’t need it.

# 5.17. Writing tail

After writing head, you should be able to write tail in a flash.

Here is the test code to add to test:

```
log $ show $ tail Nil
log $ show $ tail ("abc" : "123" : Nil)
```

Code it before moving on.

# 5.17.1. Hint for tail

Yes, yes, I know. I set you up. I purposely left off the explicit Type Signature from the test code. But, hopefully, if I did a good enough job explaining why it was needed, you were able to quickly figure out what was wrong and knew how to fix it.

If you weren’t able to, please reread the section on head and pay close attention to the Type Signature to tail (it’s slightly different than head). That should help you figure out what the explicit Type should be. Try again before moving on.

# 5.17.2. Code for tail

Just in case you are still struggling with the explicit Type in the test code:

```
log $ show (tail Nil :: Maybe (List Unit))
```

Unlike head, tail returns Maybe (List a). And since the Type Inference engine cannot determine what Type a is, we need to give it one, viz. Unit.

Here’s the other way to specify the explicit Type for a:

```
log $ show $ tail (Nil :: List Unit)
```

This Function is so close to head, we can pretty much jump right into it:

```
tail :: ∀ a. List a -> Maybe (List a)
tail Nil     = Nothing ①
tail (_ : xs) = Just xs ②
```