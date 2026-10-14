```
when :: ∀ m. Applicative m => Boolean -> m Unit -> m Unit ①
when true m = m ②
when false _ = pure unit ③
```

① Notice that it returns an m Unit, i.e. Unit in some Applicative or a Monad since all Monads are Applicatives. This is important since this allows us to have an if with a default else.

② In the if case, the m is a Monadic Value, but it must not have a Pure Computational Value, otherwise, we’d need to provide the else part explicitly. It must be a Unit in the Monadic Context. We can always use void on a Monadic Value to replace its Value with unit so that we can use it with when.

③ In the else case, it does nothing but return a default Value of unit in the Monadic Context.

Since throwError has the Type Signature, e -> m a, void must be used to dispose of the Pure Computation, i.e. change m a to m Unit. However, the Side-effect of Short-circuiting is still preserved:

```
when (n == 0) $ void $ throwError "WE CANNOT HAVE A 0 STATE!"
```

Let’s continue adding to our Application code by adding code after the error checking to modify the State and write to the log once again:

```
app :: AppM String String Int Unit
app = do
  log "Starting App..."
  n <- get
  when (n == 0) $ void $ throwError "WE CANNOT HAVE A 0 STATE!"
  put $ n + 1 ①
  log "Incremented State" ②
  pure unit
```

① Update the State by adding 1 to the old State.

② Log that we incremented State.

Now, it’s time to write a Function that will let us run the AppM Monad Stack:

```
runApp :: Int -> AppM String String Int Unit -> ?x ① ②
```

① runApp takes a State, i.e. an Int and an AppM, i.e. our Application Monad and returns something.

② The return Type is just a Type Hole for now.

If you’re not sure what to put as the return Type, you can put what’s called a Type Hole, in this case, ?x. The compiler will generate an error for you at this spot and tell you what Type it inferred. One caveat to using Type Holes in PureScript is that there must not be any other compiler errors.