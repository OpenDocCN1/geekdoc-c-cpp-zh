characters in >>=, but, instead, is the mirror image of that operator, i.e. <=.

Okay, now let’s do the same for postResult:

```
test :: Effect Unit
test = launchAff_ do
    processAjaxResult <<< Ajax.get ResponseFormat.string
        "https://jsonplaceholder.typicode.com/posts/1"
    processAjaxResult <<< Ajax.post ResponseFormat.string
        "https://jsonplaceholder.typicode.com/posts"
        (Just $ RequestBody.String $
            encodeJSON { userId:1, title:"title", completed:false })
```

And this compiles. When we run this, we get:

```
{ body: "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto", id: 1, title: "sunt aut facere repellat provident occaecati excepturi optio reprehenderit", userId: 1 }
ERROR: (NonEmptyList (NonEmpty (ErrorAtProperty "userId" (TypeMismatch "Int" "Undefined")) Nil)) ({
  "id": 101
})
```

We can see that the POST failed. Notice the actual response, which is at the end of the error:

```
({
  "id": 101
})
```

It seems as if the API has changed but the docs have not. So let’s change our model:

```
type CreateBlogPostRes =
  { id :: Int
  }
```

Now when we run with our updated model we get: