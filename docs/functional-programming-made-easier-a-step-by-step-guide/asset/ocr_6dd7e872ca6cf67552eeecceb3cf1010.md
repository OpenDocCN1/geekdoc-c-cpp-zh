```
data SumEncoding
  = TaggedObject
    { tagFieldName :: String ①
    , contentsFieldName :: String ②
    , constructorTagTransform :: String -> String ③
    }
```

① This is the name of the tag field name. In defaultOptions (see above), it’s set to "tag".

② This is the contents field name. In defaultOptions (see above), it’s set to "contents".

③ This is a transformer Function to change Data Constructor tag names, which is defaulted to identity.

# 24.2. Argonaut JSON Encoding and Decoding

The Argonaut library give you complete control over the encoding and decoding process. If you remember what we did when we wrote our Parser, this is a far simpler, yet similar process.

Let’s create a simple Type and see how we’d manually write encoders and decoders.

Here’s a simple Type for Desserts:

```
data Dessert = IceCream | Cake | Pie
```

Now we’ll want to print this Type out for testing purposes:

```
data Dessert = IceCream | Cake | Pie
derive instance genericDessert :: Generic Dessert _

instance showDessert :: Show Dessert where
  show = genericShow
```

Now we need to decide how this Type is to be represented in JSON. With the Foreign.Generic library, it would be represented as:

```
{"tag":"IceCream"}
{"tag":"Cake"}
{"tag":"Pie"}
```

The tag would be the Data Constructor name.

But we would like this to be a String. We know we can accomplish this by overriding the defaultOptions