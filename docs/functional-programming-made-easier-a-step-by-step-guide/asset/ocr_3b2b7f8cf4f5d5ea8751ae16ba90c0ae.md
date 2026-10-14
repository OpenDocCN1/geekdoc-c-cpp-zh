```
type AppM = StateT Int (ExceptT String (WriterT String Effect)) Unit

runApp
  :: Int
  -> AppM
  -> Effect (Tuple (Either String (Tuple Unit Int)) String)
runApp s = runWriterT <<< runExceptT <<< flip runStateT s
```

If you’d like to following along with this code, you can create a file called Ch21a.purs and copy all the code from Ch21.purs making sure you change the module name to Ch21a. Then replace AppM and runApp with the above code.

And now we’ll replace our validation Function:

```
import Debug (spy) ①

-- COMPILER WARNING!! ②
validate :: Int -> AppM
validate n = do
  s <- get
  let x = spy "s in validate" s
  log "HEY!!!!!!!!!!!!!!!!!" -- This will NOT be lost on the error case
  put 10 -- This will be lost on the error case but kept on success
  when (n == 0) $ void $ throwError "WE CANNOT HAVE A 0 STATE!"
```

① Added to import spy. Don’t forget to add debug to your spago.dhall.

② The compiler has a warning since you’re using spy.

First thing to notice about validation is that it will throw an error if n is zero.

Second, is that it has 2 Side-Effects. It writes to the log and it puts 10 to the State.

And finally, it outputs the Value of the State to the console upon calling this Function, via spy.

Next, let’s look at a slightly different version of app that calls this validation routine: