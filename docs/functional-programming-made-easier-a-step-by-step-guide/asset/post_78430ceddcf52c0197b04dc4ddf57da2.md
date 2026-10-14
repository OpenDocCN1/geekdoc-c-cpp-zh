
```
```text
[error] Some of your project files import modules from packages that are not
in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in
your config:
– js-date
```
```

Fix this error and run it again.

Then go to **Postman** and send a **LogonRequest** again.

When I this, everything still works. Hopefully, yours does too.

## 28.9. Server Logging

Logging is the life blood of any Server. This is because they run unattended in a server room somewhere. We aren’t going to be around when a problem rears its ugly head.

Logs lets us know what happened.

Granted in a real-world server, we’d spend far more time on Logging than we are going to do here, but this will still give you the basic idea.

Let’s log each **Request** as it comes in. Take a look at the codebase and figure out the best place to do this before you read any further.

My first reaction was to modify the `router`, but then I realized making a Logging Router is so much better. This way we don’t pollute our `router’s` complex logic with logging.

A Logging Router will log the **Request** then call our current `router` and then log the **Response** before returning it. It’s just a simple functional wrapper on `router`.

It also has to be a stand-in for our current `router` meaning that it’ll have the same or, at least, a similar Type Signature.

Write as much of this as you can. Call it `loggingRouter` and put it in `Main`, then return when you’re done or hit a brick wall.

Here’s what I wrote:

```
```haskell
loggingRouter :: HandlerEnv -> Request -> ResponseM
loggingRouter env req = do
  log $ "REQUEST: " <> show req
  res <- router env req
  log $ "RESPONSE: " <> show res
  pure res
```
```

- 1. Log the `Request`.
- 2. Delegate to `router` capturing the `Response` in `res`.
- 3. Log the `Response` (has compiler errors).
- 4. Return `Response`.

Here’s the compiler’s complaint:

![](img/8c0e9b687c62642e828ccb5481e11313_1438_0.png)

What do you think about this error? What should we do next?

When I see this, I ask the question, what Type is `Response`. When I look on Pursuit I find:

```
```haskell
type Response =
  { status :: Status.Status
  , headers :: Headers.Headers
  , writeBody :: HTTP.Response -> Aff.Aff Unit
  }
```
```

This is our problem child.

That Function is NOT showable. What we’d like is a way to remove that field and then show the rest of the Record.

We can do this manually, but there’s a pretty cool library that’ll do this for any Record. It’s called `purescript-record`. It has a module called `Record`. And there’s a Function in that module called `delete` that’ll create a new Record without the specified field.

This library can delete fields from a Record in a Type Safe manner. But it requires a bit of magic.

The first thing we’re going to have to be able to do is specify the field name in the Types. We accomplish this by using a Symbol with Proxy.

Let’s look at the kind Symbol:

![](img/8c0e9b687c62642e828ccb5481e11313_1439_0.png)

Symbol lets us to use String literals in Type Definitions.

Let’s first see how we use Proxy with delete:

```
log $ "RESPONSE: " <> (show $ delete (Proxy :: _ "writeBody") res) ① ②
```

- ① delete field named "writeBody" from the Response, i.e. res.
- ② The _ is figured out by the compiler to be the Type Proxy.

Here’s a change to our logging using delete to pull out the non-existent field writeBody__. Since we specify the field name in the Type System, and that field doesn’t exist, the following won’t compile:

```
-- COMPILER ERROR!!
log $ "RESPONSE: " <> (show $ delete (Proxy :: _ "writeBody__") res)
```

It causes the following error:

![](img/8c0e9b687c62642e828ccb5481e11313_1439_1.png)

This is because of the Constraints on delete:

```
```purescript
delete
  :: ∀ proxy r1 r2 l a
  . IsSymbol l
  => Lacks l r1
  => Cons l a r1 r2
  => proxy l
  -> Record r2
  -> Record r1
```
```

> These Constraints are built into the compiler.

To understand this, first look at `proxy`’s Type Parameter `l`, which stand for the `label` in Row `r2` that we’re going to delete. It has an `IsSymbol` constraint, which means it must be a Literal String. You cannot use a Variable of Type `String` here.

The next 2 Constraints is where the Type-level magic happens.

First is `Lacks l r1`. This Constraint says that Row `r1`, which is the Row of the returned Record, must not contain the `Symbol`, `l`. This make sense since `delete` is supposed to remove that field and `Record r1` is returned. Remember, we can construct Records from Rows using the Data Constructor `Record`.

Second is `Cons l a r1 r2`. The `l` is our `Symbol` and represents a Label. The `a` is a Type and represents the Label’s Type. Remember that Rows consists of Pairs of Labels and their corresponding Types:

```
```purescript
type SomeRow = ( someLabel :: String, someOtherLable :: Int )
```
```

So, `Cons` is a Constraint that will make sure that Row `r1`, i.e. the labels after the deletion, cons’d with the Label, `l`, of Type `a` is equal to the Row, `r2`, i.e. the labels that we started with.

In other words, `Lacks` makes sure that the final returned Row, `r1`, doesn’t already have the label we’re going to delete and `Cons` makes sure that the only difference between the Rows `r1` and `r2` is that one label.

All this checking is done at the Type level, which is why it’s Type Safe and why `writeBody__` fails to compile.

If you look at the implementation of `delete`, it simply calls Javascript to delete a field from a Javascript Object, which is the underlying representation of PureScript Records. This can be safely done because it’s already been Type Checked by the compiler, so we know the key must be in the Object before Javascript tries to `delete` it.

For now, modify you `loggingRouter` to look like:

```
```haskell
import Record (delete) ❶

loggingRouter :: HandlerEnv -> Request -> ResponseM
loggingRouter env req = do
  log $ "REQUEST: " <> show req
  res <- router env req
  log $ "RESPONSE: " <> (show $ delete (Proxy :: _ "writeBody") res) ❷
  pure res
```
```

- ❶ Add this import.
- ❷ This is the new line of code to log the `Response`.

Now, we could add lots of things to this Function. For example, we could add timestamps. When running in production with a Log Aggregator like Logify or DataDog, then you don’t need to do this since those tools automatically timestamp your log lines for you.

In case you’re not familiar with Log Aggregators, they typically collect the output your program writes to the console, i.e. `stdout` and `stderr` in Linux, and aggregate them along with the logs from other servers in your Enterprise into an online Data Store. Part of collecting the logs is to timestamp them upon collection. This allows them to present the logs in the proper order.

Another thing we could do is add a way to tie the `Request` to the `Response` so when we’re digging though a huge log, with many simultaneous `Requests`, we’ll be able to quickly find a `Request’s` corresponding `Response`. We can do this pretty easily. So let’s do it.

Generate a UUID and display it with both the `Request` and the `Response` log line. Look at the Session Manager where we generate a UUID and steal that code for this Function.

Return to reading when you’ve completed this task.

Here are the changes:

```
```haskell
import Data.UUID (genUUID) ❶

loggingRouter :: HandlerEnv -> Request -> ResponseM
loggingRouter env req = do
  id <- liftEffect genUUID ❷
  let idStr = " (" <> show id <> ")" ❸
  log $ "REQUEST: " <> show req <> idStr ❹
  res <- router env req
  log $ "RESPONSE: "
      <> (show $ delete (Proxy :: _ "writeBody") res) <> idStr ❹
  pure res
```
```

- 1. Added this import.
- 2. `genUUID` runs in `Effect`, so we use `liftEffect`.
- 3. We compute the identifying `String` once.
- 4. Append identifying `String` to both log lines.

And the final thing that’s useful is to know is how responsive your server is by timing how long it takes us to process the request. This is also very easy. We simply get the current time in milliseconds from the Epoch as soon as we get the request and right before we respond. We then calculate the difference and display the number of milliseconds in the `Response` log line.

Look to see how we got the current time in milliseconds in the Session Manager to help you add this feature to `loggingRouter`. Once you’ve done that, continue here.

Here are those changes:

```
import Data.JSDate (now, getTime)

loggingRouter :: HandlerEnv -> Request -> ResponseM
loggingRouter env req = do
  start <- getTime <$> liftEffect now
  id <- liftEffect genUUID
  let idStr = " (" <> show id <> ")"
  log $ "REQUEST: " <> show req <> idStr
  res <- router env req
  end <- getTime <$> liftEffect now
  log $ "RESPONSE: "
    <> (show $ delete (Proxy :: _ "writeBody") res)
    <> " [" <> show (end - start) <> " ms]"
    <> idStr
  pure res
```

- 1. Import time Functions.
- 2. Get the start time as soon as possible.
- 3. Get the end time as late as possible.
- 4. Add the duration for the `Request` to be serviced to the `Response` log line.

Take a good look at our `loggingRouter`. Aren’t you glad we wrote it as a separate Function?

Now, change `main` to use `loggingRouter` instead of `router` and rerun the server and test it with Postman.

Well, when I do this, I get the error:
