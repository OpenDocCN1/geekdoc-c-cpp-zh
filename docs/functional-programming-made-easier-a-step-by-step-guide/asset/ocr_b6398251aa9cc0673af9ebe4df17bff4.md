```
```haskell
staticFiles :: Request -> ResponseM
staticFiles { path } =
  let fileName =
        if null path then "index.html"
        else intercalate "/" path in
  mimeType fileName # maybe HTTPure.forbidden \\mime -> do
    fileData <- try $ readTextFile ASCII $ staticRoot <> "/" <> fileName
    fileData # either (const HTTPure.notFound) \\fileData ->
      let headers = HTTPure.headers
            [ Tuple "Content-Length" (show $ length fileData)
            , Tuple "Content-Type" $ unwrap mime
            ] in
      HTTPure.ok' headers fileData
```
```

❶ `Ok'` takes our `headers`, whereas `ok` does not.

The last thing we’ll need to do is call this function. So go change `router` to handle the HTTP `GET` and call `staticFiles`. Then return here.

Here’s that code change:

```
```haskell
router :: HandlerEnv -> Request -> ResponseM
router env req@{ body, method } 
  | method == HTTPure.Post =
      let handlers = apiHandlers <#> (_ $ body) in
      case hush $ oneOf handlers of
        Nothing -> HTTPure.badRequest body
        Just reader -> runReaderT reader env
  | method == HTTPure.Get = staticFiles req
  | otherwise = HTTPure.methodNotAllowed
```
```

❶ Aliased the full `Request` to be `req`.

❷ Added this Guard.

Now, we’re ready to run our server and test it:

```
```shell
npx spago run
```
```

Now, go to Postman and create a new Tab and enter in the URL, `localhost:3000`, leave the method as `GET` and see if you get `index.html` returned when you click Send.

Click on the Headers tab in the Response area and check that `Content-Type` and `Content-Length` are