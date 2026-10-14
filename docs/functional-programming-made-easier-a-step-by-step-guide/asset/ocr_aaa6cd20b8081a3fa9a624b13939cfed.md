```
test :: Effect Unit
test = launchAff_ do
  ttAVar <- AVar.empty ①
  -- COMPILER WARNING!!
  clockFiber <- forkAff $ clock ttAVar
  -- COMPILER WARNING!!
  bombFiber <- forkAff $ bomb ttAVar 3
  AVar.put Tick ttAVar
```

We’ll ignore the warning that reminds us that we created clockFiber and bombFiber but we’re not using them. Yet.

Now, run your program with:

```
npx spago run
```

And we get spago errors:

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- datetime
```

Fix this by adding the missing package to spago.dhall and rerun.

It should produce the following output:

```
Tick
Tock
Tick
Tock
Tick
Tock
BOOM!!
```

The only problem is that the program NEVER exits. Hit Ctrl-C to kill it. How should we solve this problem?

There are 2 ways we can handle this. First approach we could take is to have the Bomb Fiber communicate to the Clock Fiber to let it know that it exited. Then the Clock Fiber will exit.