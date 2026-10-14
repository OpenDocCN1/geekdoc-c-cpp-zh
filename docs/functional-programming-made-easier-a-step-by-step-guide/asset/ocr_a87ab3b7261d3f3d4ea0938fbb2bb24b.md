① Added this import for our Type Signature.

② Make sure you use the Aff version of AVars. There’s another set of Functions for using AVars in the Effect Monad by importing Data.AVar. This API is far more complex, so I always aviod it when possible.

Make a plan for what you think the Tick Fiber should do before coding it. Then write the code and return here once you’re done or hit a brick wall.

Here’s my plan:

+   - Read the ttAVar
+   - Delay 1 second
+   - If it’s Tock then change it to Tick otherwise leave it alone
+   - Recurse

Since we have the Type Signature, we’ll start with left-hand side of the implementation:

```
tick :: AVar TickTock -> Aff Unit
tick ttAVar = do ①
  ???
```

① Start with a do block since we’re operating in Aff.

Next, read the AVar:

```
import Effect.Aff.AVar as AVar ①

tick :: AVar TickTock -> Aff Unit
tick ttAVar = do
  tt <- AVar.take ttAVar ②
  ???
```

① Add this import with the alias so that instead writing take which is ambiguous to anyone read my code, I prefix it with AVar. to qualify which take I’m using.

② We take the AVar since we’ll probably change it.

Next, we’ll delay for 1 second: