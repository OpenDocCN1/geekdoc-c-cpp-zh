Here’s a test program to see what we get by default:

```
test :: Effect Unit
test = log $ encodeJSON $ Single true ①
```

① Prints {"contents":true,"tag":"Single"}

Notice the use of tag. This is common and is also the way Haskell’s Aeson library does it. Fun Fact: Aeson was Jason’s father in Greek Mythology.

By why tag?

That’s because Sum Types are also called Tagged Unions. Here tags are the Data Constructor names. It’s these tags that help the compiler do Pattern Matching.

Now, let’s change unwrapSingleConstructors from the default of false to true:

```
instance decodeSingle :: Decode a => Decode (Single a) where
    decode = genericDecode defaultOptions
        { unwrapSingleConstructors = true } ①

instance encodeSingle :: Encode a => Encode (Single a) where
    encode = genericEncode defaultOptions
        { unwrapSingleConstructors = true } ①

test :: Effect Unit
test = log $ encodeJSON $ Single true ②
```

① This is using the Record Update syntax. Notice the use of = instead of :. So, we want all the defaults but we want to override unwrapSingleConstructors.

② Prints true.

This program simply prints true since Single has a Single Data Constructor.

Next, we’ll change unwrapSingleArguments from true to false: