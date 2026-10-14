```
```haskell
module Data.Route where

import Prelude hiding ((/))
```
```

> We're hiding the Divide Operator since `Routing.Duplex.Generic.Syntax` has a similar operator for defining URL Paths that we're going to want to use.

Next, go to `Pursuit` and look up `RouteDuplex` and read the description and note the one and only Data Constructor then return here.

Let’s look carefully at `RouteDuplex` definition, in particular, its Data Constructor:

```
```haskell
data RouteDuplex i o = RouteDuplex (i -> RoutePrinter) (RouteParser o)
```
```

Its first Parameter is a Function that takes an `i` and produces a `RoutePrinter`, whatever that is. And the second Parameter is a parser for `o`.

In the docs, it says that we’ll want to use `RouteDuplex'` since the inputs and the outputs are the same Type with that definition:

```
```haskell
type RouteDuplex' a = RouteDuplex a a
```
```

> Input and Outputs are the same Type.

The `Duplex` part of the name of this Type represents the fact that we can parse a URL from a `String` to some output Type, the second `a`, and then take that output Type, the first `a`, as an input and create a `RoutePrinter`, which can produce a `String`.

This library will give us the ability to define a Type for Routing and a Duplex Parser/Printer for our `Route` Type.

Let’s return to `RouteDuplex`’s Data Constructor:

```
```haskell
RouteDuplex (i -> RoutePrinter) (RouteParser o)
```
```

At this point, we’re pretty familiar with parsers. But what is exactly is a `RoutePrinter`. Return to `Pursuit` and click on the `RoutePrinter` to investigate. Then keep reading.

When I do this I find that `RoutePrinter` contains a Function from `RouteState` to `RouteState`. Now click on `RouteState` in `Pursuit` and see what you find. Then continue reading.

This is what I found looking directly at the source code: