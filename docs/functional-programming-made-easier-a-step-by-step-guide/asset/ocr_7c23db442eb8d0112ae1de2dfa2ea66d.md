Next, we can derive Generic for our Type:

```
data Portion = Bit | Chunk | Part
derive instance genericPortion :: Generic Portion _
```

Now, we can leverage the Generic JSON encode and decoder for our Type to create an Encode and Decode Instance:

```
import Foreign.Generic (genericEncode, genericDecode, defaultOptions)

instance encodePortion :: Encode Portion where
    encode = genericEncode defaultOptions ①

instance decodePortion :: Decode Portion where
    decode = genericDecode defaultOptions ①
```

① We're using the default Options. More on this later.

Let's encode our Sum Type, Portion:

```
test :: Effect Unit
test = log $ encodeJSON Part ①
```

① Prints {"tag":"Part"}.

Notice the key, tag. This tagging let's the decoder know which Data Constructor to call.

There is another important element in this module and that's the Options Type and defaultOptions. You can see that we've used defaultOptions in encodePortion and decodePortion.

Let's look at them in detail. First, let's look at the Options Type:

```
type Options =
    { sumEncoding :: SumEncoding ①
    , unwrapSingleConstructors :: Boolean ②
    , unwrapSingleArguments :: Boolean ③
    , fieldTransform :: String -> String ④
    }
```

① This controls the way Sum Types are encoded. We delve into this later.

② If true then a Type that has a single Data Constructor will not be tagged.

③ If false, then a Type that has a single Type Parameter for it Data Constructor will have it's Parameters