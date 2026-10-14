```
type AppStack e w s a = ExceptT e (WriterT w (StateT s Identity)) a

type AppM = AppStack String String Int Unit

type StackResult = Tuple (Tuple (Either String Unit) String) Int ①

type AppEffects =
  { log :: String
  , state :: Int
  , result :: Maybe Unit
  }

type AppResult = Tuple (Maybe String) AppEffects ②

results :: StackResult -> AppResult ③
results (Tuple (Tuple (Left err) l) s)
  = Tuple (Just err) { log: l, state: s, result: Nothing }
results (Tuple (Tuple (Right _) l) s)
  = Tuple Nothing { log: l, state: s, result: Just unit }

runApp :: Int -> AppM -> AppResult ③
runApp s = results
  <<< unwrap
  <<< flip runStateT s
  <<< runWriterT
  <<< runExceptT
```

① Renamed AppResult to StackResult since it’s more accurate and I really wanted to free up AppResult for what the true result is.

② Repurposing AppResult here, which reflects the true results for running the Application.

③ Changed the Types here to reflect the above changes.

Now, not only are the names better, but the Type Signatures are simpler.

Here’s a test Function to run our Application: