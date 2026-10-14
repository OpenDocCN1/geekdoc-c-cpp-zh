I'm going to add that qualifier:

```
processAjaxResult
  :: ∀ t129
    . Either Ajax.Error { body :: String | t129 } ①
    -> String
```

① Added Ajax. prefix to qualify which Error.

Now the compiler is happy, but we're not. What does t129 stand for. By the way, your number may or may not be 94. It doesn't matter since your number is equally unhelpful.

We can see by how t129 is used that its a Row Type. Tradition dictates that we call this r:

```
processAjaxResult
  :: ∀ r
    . Either Ajax.Error { body :: String | r }
    -> String
```

But wait. We know that the Record is simply a Response a where a is a String:

```
processAjaxResult ①
  :: Either Ajax.Error (Ajax.Response String) ②
    -> String
```

① Removed the ∀ since we’re not using r anymore.

② Fully qualified Response since Affjax is imported qualified.

Now, this is great but it’s not as general as I would like. Take a look at both the Type Signature and the code for processAjaxResult and see if you can find all the places where we could generalize before reading my take.

Here’s my take doing the analysis: