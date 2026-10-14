```
instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = do
        o <- decodeJSONObject json
        tag <- o .: "gat"
        if tag == "Personal" then do
            height <- decodeForeign $ o .: "thgieh"
            weight <- decodeForeign $ o .: "thgiew"
            age <- decodeForeign $ o .: "ega"
            pure $ Personal { height, weight, age }
        else Left $ AtKey "tag" $ UnexpectedValue json
```

This solution is better but still we have a bit of clutter having to call our helper, decodeForeign. And it’s a fine solution if we MUST keep decoding Centimeters, Kilograms and Years using the Foreign library.

But, we don’t have that requirement and, instead, we going to just derive a decoder using Argonaut for these Types:

```
newtype Centimeters = Centimeters Number
derive instance genericCentimeters :: Generic Centimeters _
derive newtype instance encodeCentimeters :: Encode Centimeters
drive newtype instance decodeJsonCentimeters :: DecodeJson Centimeters ①

newtype Kilograms = Kilograms Number
derive instance genericKilograms :: Generic Kilograms _
derive newtype instance encodeKilograms :: Encode Kilograms
drive newtype instance decodeJsonKilograms :: DecodeJson Kilograms ①

newtype Years = Years Int
derive instance genericYears :: Generic Years _
derive newtype instance encodeYears :: Encode Years
drive newtype instance decodeJsonYears :: DecodeJson Years ①
```

① Replaced the derive from Decode to DecodeJson.

So, go ahead make these changes to your code and watch the compiler error disappear: