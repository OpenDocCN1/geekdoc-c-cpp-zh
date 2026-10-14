We're going to ignore the warning for now but we should add these new direct dependencies to our spago.dhall to address the error:

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "aff" ①
  , "console"
  , "effect"
  , "either" ①
  , "maybe" ①
  , "prelude"
  , "psci-support"
  , "refs" ①
  , "routing-duplex"
  , "routing"
  , "transformers" ①
  , "uuid"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① These were added in these locations to keep the list in alphabetical order.

Now we can try to build again:

```
npx spago build
```

Now that we can build with a warning, we should turn our attention back to our Application Monad. Before advancing any further, use derive newtype to derive Monad for AppM. Don't forget that you'll need to derive a few Typeclasses before Monad.

Then return here.

Here are those changes: