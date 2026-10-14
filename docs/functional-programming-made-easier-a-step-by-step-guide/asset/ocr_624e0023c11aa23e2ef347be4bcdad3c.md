```
exports.fromBoolean = id;
exports.fromNumber = id;
exports.fromString = id;
exports.fromArray = id;
exports.fromObject = id;
```

All of these JSON primitives, e.g. Boolean, Number, Object, Array, etc., have the same representation as a Json.

Let’s look at Boolean’s encodeJson implementations:

```
instance encodeJsonBoolean :: EncodeJson Boolean where
  encodeJson = fromBoolean
```

We can see that encoding a Boolean doesn’t really change it’s form, but it does change its Type. We saw this with unsafeCoerse when we were looking at undefined.

In this case, its not unsafe. In fact, it’s here to make it safe.

So, we can look at Json as a Type that lets us know that the data is represented as a Javascript JSON element. We can look at stringify to see that it expects a Json:

```
stringify :: Json -> String
```

And if we look at the implementation we find:

```
foreign import stringify :: Json -> String
```

We can see that this definition is in Core.purs, which means we’ll have to look back at Core.js for the real implementation:

```
exports.stringify = function (j) {
  return JSON.stringify(j);
};
```

And we can see why stringify wants to make sure that it has a valid JSON element. We can safely pass a String to this but ONLY after we’ve passed it through encodeJson, which does nothing other than change it’s Type.

And since there are only a handful of these coercing encoding Functions, viz. all of the JSON elements, we