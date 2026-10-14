```
instance decodeJsonStudent :: DecodeJson Student where
    decodeJson json = do
        o <- decodeJObject json
        tag <- o .: "gat"
        if tag == "Student" then do
            grade <- o .: "edarg"
            teacher <- o .: "rehcaet"
            gpa <- o .: "apg" -- COMPILER ERROR!!
            personal <- o .: "lanosrep"
            pure $ Student { grade, teacher, gpa, personal }
        else Left $ AtKey "tag" $ UnexpectedValue json
```

Without looking at the editor pop-up, can you see why we get a compiler error?

We have the same problem we had with Centimeters, Kilograms and Years, i.e. GPA has a decoder that uses the wrong library, i.e. Foreign and not Argonaut.

Apply the same fix to GPA that we did to Centimeters, Kilograms and `Years before reading further.

Here’s the fix:

```
newtype GPA = GPA Number
derive instance genericGPA :: Generic GPA _
derive newtype instance encodeGPA :: Encode GPA
d derive newtype instance decodeJsonGPA :: DecodeJson GPA ①
```

① Replaced the derive from Decode to DecodeJson.

Now, you may have noticed that we got a Shadow variable warning:

```
instance decodeJsonStudent :: DecodeJson Student where
    decodeJson json = do
        o <- decodeJObject json
        tag <- o .: "gat"
        if tag == "Student" then do
            grade <- o .: "edarg"
            teacher <- o .: "rehcaet" -- COMPILER WARNING!!
            gpa <- o .: "apg"
            personal <- o .: "lanosrep"
            pure $ Student { grade, teacher, gpa, personal }
        else Left $ AtKey "tag" $ UnexpectedValue json
```