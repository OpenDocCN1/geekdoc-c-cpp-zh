```
type Family r =
  { fatherName :: String
  , motherName :: String
  , childName :: String
  | r
  }
```

① We have to pass r as the Row that will Extend this Record, hence the term Extensible Record.

② We specify that r is a Row Type that extends the Record using this syntax.

This is great since it removes the duplication, but it also gives us another huge benefit. It gives us some flexibility when creating a Family, e.g we could add other fields:

```
Family ( fatherOccupation :: Occupation, motherOccupation :: Occupation )
```

Or we could add NO fields:

```
Family ()
```

Notice that () is the syntax for an Empty Row, i.e. no fields. Be carful not to confuse this with the unit Type and Value from Haskell or Elm.

And now that we can see the benefits of using Rows, let’s start with Rows to define our fields and then put them together to construct a Record called Family. First, add FamilyAgesRow to your code and then code up FamilyNamesRow on your own before continuing further.

Once you’re done coding, you should have something like the following:

```
type FamilyAgesRow
  = ( fatherAge :: Int, motherAge :: Int, childAge :: Int )

type FamilyNamesRow
  = ( fatherName :: String, motherName :: String, childName :: String )
```

Now we’re ready to use these to create Family. How would you create Family from these 2 rows?

You might think that it’s possible to add them to Family like this:

```
-- NOT VALID PureScript SYNTAX!!!
newtype Family = Family { | FamilyNamesRow, FamilyAgesRow }
```