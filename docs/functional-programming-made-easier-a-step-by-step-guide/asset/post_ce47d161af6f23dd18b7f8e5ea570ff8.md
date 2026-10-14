
+   1. Derive a Generic Instance.

+   2. Delegate the newtype’s Instance to the contained Type’s Instance.

Now is a good time to remove the unused imports leaving you the following imports:

```
import Prelude

import Affjax as Ajax
import Control.Monad.Except (runExcept)
import Data.Argonaut (class DecodeJson, JsonDecodeError(..), (: :))
import Data.Argonaut.Decode.Decoders (decodeJObject)
import Data.Either (Either(..))
import Data.Generic.Rep (class Generic)
import Data.Show.Generic (genericShow)
import Effect (Effect)
import Effect.Aff (launchAff_)
import Effect.Class.Console (log)
import Foreign.Generic (decodeJSON, defaultOptions, encodeJSON, genericEncode)
import Foreign.Generic.Class (class Decode, class Encode)
import Type.Proxy (Proxy)
```

Now, write the decoder for Personal using the Argonaut library. Use what we’ve done with Grade and TeachingStatus as you guide. You’re going to run into a couple of issues along the way. If you cannot overcome them, don’t worry. Just return here and we’ll go through it together.

Here’s an example JSON to help:

```
{
  "contents": {
    "weight": 20,
    "height": 10,
    "age": 30
  },
  "tag": "Personal"
}
```

When you’re done, return back here.

We’ll start coding with the instance definition:

```
instance decodeJsonPersonal :: DecodeJson Personal where
```

Next we’ll code up the left-hand side:

```
instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = ???
```

Since Personal is a Record, we’re going to have a lot of fields to decode. This is a good case for coding it Monadically using a do block:

```
instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = do
        ???
```

Since it’s a JSON Object, we will use decodeJObject:

```
instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = do
        o <- decodeJObject json
        ???
```

Next, we want to make sure that the tag is correct, i.e. we’re decoding a Personal not just any old Type that happens to have the same fields as Personal, for example:

```
newtype Imposter = Imposter
    { hairColor :: HairColor
    , height :: Centimeters
    , weight :: Kilograms
    , occupation :: Occupation
    , age :: Years
    }
```

Here Imposter will have all of the fields that Personal has. The fact that it has additional fields won’t deter Personal’s decoder since it will simply ignore them.

The only real difference here is that the tag will be Imposter, which is why we want to make sure we check the tag in the decoder.

tag gives our JSON a bit of Type Safety:

```
instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = do
        o <- decodeJObject json
        tag <- o .: "gat" ①
        if tag == "Personal" then do ②
            ???
        else Left $ AtKey "tag" $ UnexpectedValue json ③
```

① Get the tag Value from the JSON Object, o.

② Make sure tag is Personal.

③ Return error. Notice that fail is not used here because its hardcoded error message isn't accurate for this situation.

If you didn’t get this far, please stop reading and finish the code.

The next step is to get the fields. We’ll name the variables the same as the field names to make the construction of the Record simpler, i.e. we won’t have to say { height: height } when { height } will do. But we’re not going to forget that the Echo Server will reverse our keys, so we’ll get the fields with backward names:

```
instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = do
        o <- decodeJObject json
        tag <- o .: "gat"
        if tag == "Personal" then do
            height <- o .: "thgieh"
            weight <- o .: "thgiew"
            age <- o .: "ega"
            ???
        else Left $ AtKey "tag" $ UnexpectedValue json
```

Notice the field name Strings are backwards. That’s because we’re decoding the response from the Echo Server.

And finally, we create a Personal and wrap it in an Either:

```
instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = do
        o <- decodeJObject json
        tag <- o .: "gat"
        if tag == "Personal" then do
            height <- o .: "thgieh" -- COMPILER ERROR!!
            weight <- o .: "thgiew"
            age <- o .: "ega"
            pure $ Personal { height, weight, age } ①
        else Left $ AtKey "tag" $ UnexpectedValue json
```

① We're using a shorthand syntax here, which works when the name of the field and the name of the variable are the same.

And now we have a compiler error:

![](img/8c0e9b687c62642e828ccb5481e11313_1182_0.png)

Looks like we're not going to be able to keep the current decoders for Centimeters since it's using the Foreign library.

Well, technically we could make it work, but then our code would look like:

```
import Data.Bifunctor (lmap) ①

instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = do
        o <- decodeJObject json
        tag <- o .: "gat"
        if tag == "Personal" then do
            height <- do
                x <- o .: "thgieh" ②
                lmap (TypeMismatch <<< show) <$> runExcept $ decodeJSON x ③ ④
            weight <- do
                x <- o .: "thgiew"
                lmap (TypeMismatch <<< show) <$> runExcept $ decodeJSON x
            age <- do
                x <- o .: "ega"
                lmap (TypeMismatch <<< show) <$> runExcept $ decodeJSON x
            pure $ Personal { height, weight, age }
        else Left $ AtKey "tag" $ UnexpectedValue json
```

① Import lmap.

② Extract the JSON data from the Either.

③ Decode the JSON data and run the Except to get an Either and then lmapping to convert the Error to a JsonDecodeError. We are running in the Either JsonDecodeError Monad.

④ Map the Left of the Either from F to JsonDecodeError.

This code looks terrible. But, we could fix that by factoring out the common code into a helper Function:

```
decodeForeign :: ∀ a. Decode a => Either JsonDecodeError String -> Either JsonDecodeError a
decodeForeign fieldData = do ①
    x <- fieldData
    lmap (TypeMismatch <<< show) <$> runExcept $ decodeJSON x
```

① Factored out the common code.

Then our code would clean up a bit:

```
instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = do
        o <- decodeJObject json
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
derive newtype instance decodeJsonCentimeters :: DecodeJson Centimeters ①

newtype Kilograms = Kilograms Number
derive instance genericKilograms :: Generic Kilograms _
derive newtype instance encodeKilograms :: Encode Kilograms
derive newtype instance decodeJsonKilograms :: DecodeJson Kilograms ①

newtype Years = Years Int
derive instance genericYears :: Generic Years _
derive newtype instance encodeYears :: Encode Years
derive newtype instance decodeJsonYears :: DecodeJson Years ①
```

① Replaced the derive from Decode to DecodeJson.

So, go ahead make these changes to your code and watch the compiler error disappear:

```
instance decodeJsonPersonal :: DecodeJson Personal where
    decodeJson json = do
        o <- decodeJObject json
        tag <- o .: "gat"
        if tag == "Personal" then do
            height <- o .: "thgieh"
            weight <- o .: "thgiew"
            age <- o .: "ega"
            pure $ Personal { height, weight, age }
        else Left $ AtKey "tag" $ UnexpectedValue json
```

Next, code up the decoder for Teacher using the above decoder as reference. When you’ve got that done, return here for the solution.

Since, the solution is practically the same as for Personal, I’m going to give it to you already done:

```
instance decodeJsonTeacher :: DecodeJson Teacher where
    decodeJson json = do
        o <- decodeJObject json
        tag <- o .: "gat"
        if tag == "Teacher" then do
            grades <- o .: "sedarg"
            numberOfStudents <- o .: "stnedutSf0rebmun"
            personal <- o .: "lanosrep"
            status <- o .: "sutats"
            pure $ Teacher { grades, numberOfStudents, personal, status } ①
        else Left $ AtKey "tag" $ UnexpectedValue json
```

① Construction of Teacher uses the shorthand syntax for Record field Values.

And now, do the same for Student before reading on.

Here’s Student’s decoder:
