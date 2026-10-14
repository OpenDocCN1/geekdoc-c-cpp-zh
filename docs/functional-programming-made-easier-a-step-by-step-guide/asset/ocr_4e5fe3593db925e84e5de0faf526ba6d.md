```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "console"
  , "effect"
  , "lists" ①
  , "prelude"
  , "psci-support"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① This will add the package that has the module we need, Data.List.

Once you do this, rebuild your program:

```
npx spago build
```

This will install the purescript-lists package and compile it.

You will get a bunch of warnings. These are because of 2 reasons.

First, we aren’t using Data.List yet and hence the following warning:

```
Warning 9 of 9:

    in module Ch5
    at src/Ch5.purs:5:1 - 5:33 (line 5, column 1 - line 5, column 33)

    The import of Data.List is redundant

    See
https://github.com/purescript/documentation/blob/master/errors/UnusedImport.md
for more information,
    or to contribute content related to this warning.
```

All of the other 8 warnings are because there are things in the PureScript libraries that haven’t caught up