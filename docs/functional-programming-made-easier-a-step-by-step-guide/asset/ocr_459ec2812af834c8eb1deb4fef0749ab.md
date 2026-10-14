Now can you see any improvements?

I see a lot of duplicate code. So go ahead and factor the duplicate code before reading any further.

We’re going to factor our the call to Ajax.post and all of it’s common Parameters. We’ll use a Lambda:

```
test :: Effect Unit
test = launchAff_ do
  parSequence $ (\o -> Ajax.post ResponseFormat.json
    "http://localhost:3000/"
    $ Just $ RequestBody.String $ encodeJSON o) ①
  <$> [ -- COMPILER ERROR!!
    testTeacher
  , testStudent
  ]
```

① This Lambda is mapped over our Array. Here o is the object to encode.

The compiler error is:

![](bbox=[0.367, 0.455, 0.633, 0.688])

Can you see where I went wrong?

The compiler is saying that it cannot match Student with Teacher. I’ve made the mistake of placing Teacher and Student in the same Array. Arrays are Homogeneous, i.e. all elements must be of the same Type.

We need a way to convert them both to the same Type. Can you think of a way?

Looking at the Lambda may provide a clue. How about now?

Turns out that we can call encodeJSON on each of them and then the Array will contain elements of Type Json: