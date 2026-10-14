Make sure you code is totally up to date and then rerun your server.

Did you get a compiler error?

That’s because our Top-level Counter isn’t getting it’s new Parameter yet. Change `main` as follows:

```
main :: Effect Unit
main = do
  HA.runHalogenAff do
    body <- HA.awaitBody
    runUI (Counter.component 3) 0 body
```

❶ Pass 3 for `numChildren`.

Try again.

Did you get:

```
[warn] None of your project files import modules from some projects that are
in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following
packages from the list of dependencies in your config:
- const ❶
[error] Some of your project files import modules from packages that are not
in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in
your config:
- arrays ❷
```

❶ No longer needed.

❷ We need this.

Update your `spago.dhall` to add `arrays` and remove `const`.

Now run the server and refresh your browser. You should get:

![](bbox=[0.324, 0.797, 0.678, 0.869])

Currently, we have no way of calling `H.raise` to send `Output` to our Parent. So, let’s add a button under the Counter, whose `Action` will call `H.raise`: