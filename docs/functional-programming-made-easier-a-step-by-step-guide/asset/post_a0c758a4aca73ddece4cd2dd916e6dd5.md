
`params` are Query Parameters in the URL.

And finally, the `hash` is printed with a preceding `#`, which lets us know that it’s URI Fragment or what’s commonly referred to as the Hash.

So, I suspect that `RouteParser` takes a `String` and produces a `RouteState`. Doing a little investigation work, I find `runRouteParser` in `Routing.Duplex.Parser`:

```
runRouteParser :: ∀ a. RouteState → RouteParser a → RouteResult a
```

We can see that it returns `RouteResult`, which is:

```
data RouteResult a
  = Fail RouteError
  | Success RouteState a
```

This contains a `RouteState` on the success case.

So it looks like `RouteParser` will parse the segments of the URL Path, the Query Parameters and the URI Fragment (Hash).

But, the nice thing about URI Fragments, is that they too can have path segments, since the `/` character is allowed in a Fragment. It can also have the equivalent of Query Strings or Query Parameters since `=`, `&` and `?` are also allowed in Fragments.

So, if we use `Routing.Duplex` for just parsing URI Fragments, then we’ll be able to parse both `segments` and `params`. We cannot parse `hash` from a URI Fragment since `#` is not allowed in a URI Fragment.

## 30.2.1. Defining Routes

Before we define our Routes, let’s install `purescript-routing-duplex` and `purescript-routing` by running:

```
npx spago install routing-duplex routing
npx spago build
```

You will get the following warning:

```
[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- routing
- routing-duplex
```

That's because we aren't using the library anywhere in our code. Not yet that is.

Now, let's define a Route Type that corresponds with our backend server API. But let's start simply by just including logon and logoff:

```
data Route
  = Logon
  | Logoff
```

Next, we'll need to make our Route Type have a Generic Instance so `Routing.Duplex` can use it:

```
import Data.Generic.Rep (class Generic) ①

data Route
  = Logon
  | Logoff
derive instance genericRoute :: Generic Route _ ②
```

- ① Added this import.
- ② Derive Generic.

Now, we'll build our Codec, i.e. Coder-Decoder. Here it is in full:

```
import Routing.Duplex (RouteDuplex', root, path) ①
import Routing.Duplex.Generic (sum, noArgs)

routeCodec :: RouteDuplex' Route
routeCodec = root $ sum ② ③
  { "Logon": path "logon" noArgs ④ ⑤ ⑥
  , "Logoff": path "logoff" noArgs
  }
```

- ① Added these imports.
- ② root represents the root of the URL path, i.e. /.
- ③ sum is to represent Sum Types. We’re using it here since our Route Type is a Sum Type.
- ④ Each field name String must match exactly the name of the Data Constructor, hence the use of double quotes to use uppercase characters in the Record field names.
- ⑤ path defines a Path of a particular Value, e.g. logon.
- ⑥ noArgs is when the particular route has no Parameters.

The Record passed to sum defines routes that have field names that must match EXACTLY the Data Constructors in the `a` of `RouteDuplex' a`. In our case, the field names match the Data Constructors of Route.

There is also a product Function that can be used for Product Types.

So far, we’ve defined the following valid Path Segments:

```
/logon
/logoff
```

These are Static Segments. We’ll see Variable Segments in a moment.

Next, install the purescript-uuid package with:

```
npx spago install uuid
npx spago build
```

Once again, we can ignore the following warning:

```
[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- routing
- uuid
```

Next, create a File under src/Data called UserId.purs. Add the following code:

```
module Data.UserId where

import Data.UUID (UUID)

newtype UserId = UserId UUID
```

This is a UserId that we’ll use in a URL when we want to view User information.

Now, let’s add a route for the users page. To do this, we’ll first need to update our Route Type:

```
import Data.Maybe (Maybe) ①
import Data.UserId (UserId(..))

data Route
  = Logon
  | Logoff
  | Users (Maybe UserId) ②
derive instance genericRoute :: Generic Route _
```

- ① Added these imports.
- ② We’ve added the UserId as a Maybe so we can see all users when it’s missing.

Notice the compiler error on sum when we make this change:

![](img/8c0e9b687c62642e828ccb5481e11313_1660_0.png)

This is because our definition is made Type safe by `Routing.Duplex` library’s use of Generics. The compiler will catch when we’re missing a field.

Notice here that it’s complaining about a Row with Users in it not matching the Row with only Logon and Logoff in it.

The compiler will, however, NOT complain if we have an EXTRA field in the Record we pass to sum.

We’ll need to add a route definition to our Record. But before we do we should look at how we can define a Path Segment using segment:

```
-- Allows you to capture a variable segment. For example, the path
-- /user/5 has one static segment and one variable segment. This always
-- reads and writes a string, but when used with other combinators, it
-- can transform that string into a type of your choice. For example:
-- `path "user" (int segment)` parses to `User Int`.
segment :: RouteDuplex' String
```

Notice how segment defines Variable Segments. This can be seen in the documented example of /user/5. user is a Static Path Segment, whereas, 5 is a Variable Path Segment.

We can use the following modifiers to change the String Type that segment gives us to other Types:

```
int :: RouteDuplex' String -> RouteDuplex' Int
boolean :: RouteDuplex' String -> RouteDuplex' Boolean
string :: RouteDuplex' String -> RouteDuplex' String ①
```

- ① Just identity.

While these combinators convert to standard Types, we’ll need to convert our Path Segment into a UserId. This can be accomplished with another more powerful combinator:

```
as
  :: ∀ s a b
  . (a -> s) ①
  -> (String -> Either String b) ②
  -> RouteDuplex s String
  -> RouteDuplex a b
```

- ① This is the custom Printer.
- ② This is the custom Parser.

as is written here in the more general form where the input and output Types could be different. But they’re not for us, so here’s what it looks like in that case:

```
as
  :: ∀ a
  . (a -> String)
  -> (String -> Either String a)
  -> RouteDuplex' String
  -> RouteDuplex' a
```

We’ll need to write a Function to convert a `RouteDuplex' String` to `RouteDuplex' UserId`. Write just the Type Signature of a Function called userId that does this before reading on.

Here’s just that portion of userId:

```
userId :: RouteDuplex' String -> RouteDuplex' UserId
```

Next, finish the code leveraging as to provide a custom printer and parser. Then return here.

We’re going to call as with yet undetermined printer and parser:

```
import Routing.Duplex (RouteDuplex', root, path, as) ①

userId :: RouteDuplex' String -> RouteDuplex' UserId
userId = as printer parser where ②
  printer :: UserId -> String ③
  printer = ???
  parser :: String -> Either String UserId ③
  parser = ???
```

- ① Added as to the import list.
- ② Written Point-free where the `RouteDuplex' String` is unnamed.
- ③ These Type Signatures are here to help us write these Functions. We’ll remove them at the end.

If you didn’t finish, but think that you can now, stop reading here and give a try.

The next part is the code for the custom printer:

```
import Data.UUID as UUID ①

userId :: RouteDuplex' String -> RouteDuplex' UserId
userId = as printer parser where
  printer :: UserId -> String
  printer (UserId uuid) = UUID.toString uuid ②
  parser :: String -> Either String UserId
  parser = ???
```

- ① Added this import.
- ② Destructure UserId to get the underlying UUID then convert it to a String. Note, we’re not using show here since it includes the UUID prefix, e.g. (UUID dc64cf80-f663-436a-a290-3cac4acf279f).

And finally, we’ll write the custom parser:
