```
instance decodeJsonPersonal :: DecodeJson Personal where
...
instance decodeJsonGrade :: DecodeJson Grade where
...
instance decodeJsonStudent :: DecodeJson Student where
...
instance decodeJsonTeachingStatus :: DecodeJson TeachingStatus where
...
instance decodeJsonTeacher :: DecodeJson Teacher where
...
```

So delete the implementations.

Now we don’t have decoders for the above Types, since we just deleted them. Create Decode Instance for them using genericDecode.

Once you’re done, return here.

Here are the changes for Personal:

```
import Foreign.Generic (defaultOptions, encodeJSON, genericEncode,
genericDecode) ①

instance decodePersonal :: Decode Personal where
    decode = genericDecode defaultOptions
```

① Added genericDecode to the import list.

The others are similar to this change:

```
instance decodeGrade :: Decode Grade where
    decode = genericDecode defaultOptions

instance decodeStudent :: Decode Student where
    decode = genericDecode defaultOptions

instance decodeTeachingStatus :: Decode TeachingStatus where
    decode = genericDecode defaultOptions

instance decodeTeacher :: Decode Teacher where
    decode = genericDecode defaultOptions
```

Turning our attention to the test Function, we can see that we have a compiler error on decodeJson, i.e.