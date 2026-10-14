```
import Type.Proxy (Proxy(..)) ①

test :: Effect Unit
test = launchAff_ do
  result <- Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String $ encodeJSON testTeacher
    -- COMPILER ERROR!!
  log $ processAjaxResult (Proxy :: _ Teacher) result
```

① Added (..) to get the Proxy Data Constructor.

And now a different error:

![](bbox=[0.28, 0.347, 0.72, 0.565])

We're missing a Show Instance for Teacher. But wait. Why didn't we need this before?

Well, if you remember correctly, it's because we were using ReversedTeacher and we didn't need a Show Instance because it was a Type Alias.

But now, Teacher is a newtype. Go ahead and add an instance for Show for Teacher before reading any more.

Here's that instance:

```
instance showTeacher :: Show Teacher where
  show = genericShow -- COMPILER ERROR!!
```

And now this error: