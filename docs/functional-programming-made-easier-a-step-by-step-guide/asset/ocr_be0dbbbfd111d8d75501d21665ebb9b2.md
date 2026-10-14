```
import Prelude (Unit, show, discard)

import Data.List (List(..), (:)) ①
import Effect (Effect)
import Effect.Console (log)
```

① This should have a compiler error.

It turns out that we need don’t have the List package. If you search Pursuit for Data.List you’ll find the package that contains this Type:

# M Data.List

This module defines a type of *strict* linked lists, and associated helper functions and type class instances.

*Note:* Depending on your use-case, you may prefer to use `Data.Sequence` instead, which might give better performance for certain use cases. This module is an improvement over `Data.Array` when working with immutable lists of data in a purely-functional setting, but does not have good random-access performance.

P purescript-lists

At the bottom, we see `purescript-lists` is the package name.

To add packages to our build, we need to edit the `spago.dhall` file. When adding a package, we always leave off the `purescript-` prefix. So that means we need to add `lists` to the `dependencies`: