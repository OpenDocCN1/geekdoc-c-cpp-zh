```
node src/echo-server.js
```

Then edit Main.purs to call Ch27b instead of Ch27a.

Then run the program and see what you get.

So, it looks like we need to add foreign back to our spago.dhall:

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- foreign
```

Now when I fix this and rerun the code, I get:

```
(Left "(NonEmptyList (NonEmpty (ErrorAtProperty \"tag\" (TypeMismatch \"String\" \"Undefined\")) Nil))")

(Left "(NonEmptyList (NonEmpty (ErrorAtProperty \"tag\" (TypeMismatch \"String\" \"Undefined\")) Nil))")
```

First off, it doesn’t work.

Second, do you notice the \" all over the place? That usually means we have an extra show. If you show a String, it’ll add double quotes around that String.

Let’s remove the lmap show from processJSON and see if it cleans up the embedded quotes: