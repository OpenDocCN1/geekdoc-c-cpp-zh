That looks simple enough. Let’s get started with the instance definition:

```
import Data.Argonaut.Encode (class EncodeJson) ①

instance encodeJsonDessert :: EncodeJson Dessert where
```

① Import the Typeclass.

Next, we handle each case using Pattern Matching:

```
instance encodeJsonDessert :: EncodeJson Dessert where
  encodeJson IceCream = ???
```

We need to return a Value of Type Json. At this point, you may be wondering what is a Json. Let’s look at its definition from Pursuit:

```
data Json :: Type
```

Well, that’s not helpful at all. All it tells us is that it’s a Type. Let’s look at its implementation by clicking on Source in Pursuit and then searching the code for it:

```
foreign import data Json :: Type
```

That’s even less helpful. What is this even?

Well, this is a way to create a Type of a specific Kind. In this case, the Kind is Type.

This seems to be what I call a Marker Type. If I had to guess, I’d suspect that it’s probably used to identify the return Type for the Javascript Functions that are used by this library.

You’ll learn more if you follow along while we investigate this. Go to Pursuit now and continue reading.

Let’s see by investigating encodeJson for String by searching for EncodeJson in Pursuit and then clicking on Source and then searching the code for EncodeJson String.

You should find:

```
instance encodeJsonJString :: EncodeJson String where
  encodeJson = fromString
```

Okay, now we have to look at fromString. Search on Pursuit for fromString making sure that it’s the