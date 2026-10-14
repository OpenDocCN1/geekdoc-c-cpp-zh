Change the router in Main, using Guards, to make sure that method from the Request is a Post. Use the code we commented out in main as a reference. Give this a go before reading any further.

Here’s that fix:

```
router :: HandlerEnv -> Request -> ResponseM
router env { body, method } ① ②
  | method == HTTPure.Post = ③
    case hush <=<
      (head $ oneOf $ (handle body (Proxy :: _ Logon)) :| [] ) of
        Nothing -> HTTPure.badRequest body
        Just reader -> runReaderT reader env
  | otherwise = HTTPure.methodNotAllowed ④
```

+   ① Destructure method also.

+   ② Removed the equals sign since we’re using Guards.

+   ③ Only respond to POST requests.

+   ④ Everything else is 405, i.e. Method Not Allowed.

Rerun the server and then go to Postman and change POST to GET and send it and see if it returns an error status.

I get the following when I do that:

![](bbox=[0.103, 0.553, 0.897, 0.663])

So our new code works. Now change Postman back to use POST.

Next, lets test our code for the invalid logon case by changing the userName in Postman to "invalid" and sending again. What do you get?

I got: