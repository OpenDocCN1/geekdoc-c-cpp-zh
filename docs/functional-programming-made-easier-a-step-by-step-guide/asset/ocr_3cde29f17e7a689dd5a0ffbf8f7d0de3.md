① Data Construtor is tag in the JSON.

② Record is contents in JSON.

Update you code to match this if you haven’t already.

The compiler error is because this package is not part of our spago.dhall, so let’s add it:

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "aff"
  , "arrays"
  , "console"
  , "effect"
  , "httpure"
  , "maybe"
  , "prelude"
  , "psci-support"
  , "uuid" ①
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① Keeping the list in alphabetical order.

Then kill the server (if it’s still running) and run:

```
npx spago build
```

We’ll still ignore the warning regarding aff.

Now if you save Logon.purs, the compiler error should disappear.

But there’s one more thing to do. Go look up UUID on Pursuit and then click on the package name in the Search Results.

Read what it says in the package docs, then return here.

Here’s what I found: