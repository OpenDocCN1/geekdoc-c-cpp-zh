![](bbox=[0.235, 0.06, 0.765, 0.215])

The compiler say that it *Cannot derive a type class for Data.Show.Show*. And it says below that it cannot do so because *instances of this type class are not derivable*.

In the previous Chapter, we talked about using `genericShow`. But to do this, our Type must have an Internal Representation of the Type so that `genericShow` can use that representation to display the value.

This is done with the following imports:

```
import Data.Generic.Rep (class Generic)
import Data.Show.Generic (genericShow)
```

Next, we want to build using:

```
npx spago build
```

And we get the following error:

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- maybe
- tuples
```

We need to add these packages to `spago.dhall` as Direct Dependencies of our project: