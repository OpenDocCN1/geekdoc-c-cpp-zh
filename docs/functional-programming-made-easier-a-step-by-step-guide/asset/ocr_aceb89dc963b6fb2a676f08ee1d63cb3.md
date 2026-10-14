```
```text
{−
Welcome to a Spago project!
You can edit this file as you like.
→}
{ name = "my-project"
, dependencies =
  [ "aff"
  , "console"
  , "css"
  , "effect"
  , "either"
  , "halogen"
  , "halogen-css"
  , "maybe"
  , "prelude"
  , "psci-support"
  , "refs"
  , "routing"
  , "routing-duplex"
  , "transformers"
  , "uuid"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```
```

① Added these.

Now build the app with:

```
```text
npx spago build
```
```

This command installed the new packages into our `.spago` directory, but gives us the following errors:

```
```text
[error] Some of your project files import modules from packages that are not
in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in
your config:
− const
− datetime
− now
```
```