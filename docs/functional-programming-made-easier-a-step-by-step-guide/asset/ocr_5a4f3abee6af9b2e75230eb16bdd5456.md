```
```purescript
type FamilyAges = { fatherAge :: Int, motherAge :: Int, childAge :: Int }

type Family =
  { fatherName :: String
  , motherName :: String
  , childName :: String
  , fatherAge :: Int
  , motherAge :: Int
  , childAge :: Int
  }
```
```

Can you think of why this is undesirable?

The most obvious problem here is that we’ve MANUALLY duplicated the fields in `FamilyAges` inside `Family`. Can you think of a way we can eliminate this manually duplication process?

Do you remember when we talked about Row Types? Don’t feel bad if you don’t, there’s been a lot of ground covered since then. Besides we didn’t delve into them deeply. We’ll dive a bit deeper here.

First, a review of what we did talk about. Here’s the example where Row Types were introduced:

```
```purescript
isCalifornia :: ∀ r. { address :: Address | r } -> Boolean
isCalifornia { address: { state } } = state == "CA"
```
```

The salient portion here is the `| r` portion. That tells us that we can have other fields in this Record. Here the only REQUIRED field is `address`.

What we didn’t say back then was how to specify r syntactically in PureScript.

Let’s do that using our family example:

```
```purescript
type FamilyAgesRow
  = ( fatherAge :: Int, motherAge :: Int, childAge :: Int )
```
```

Notice the syntax for a Row is different than for a Record. We use Parentheses instead of Curly Brackets.

Now we can rewrite our definition of `Family` so that we can pass this Row as a Type Parameter, r. The following definition for `Family` is called an *Extensible Record*: