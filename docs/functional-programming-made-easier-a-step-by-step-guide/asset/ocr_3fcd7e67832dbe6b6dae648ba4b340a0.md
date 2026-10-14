or maybe:

```
```purescript
-- NOT VALID PureScript SYNTAX!!!
newtype Family = Family { | FamilyNamesRow | FamilyAgesRow }
```
```

Unfortunately, none of these work. The way to do accomplish this is to add a Row Parameter to our Row Types, `FamilyAgesRow` and `FamilyNamesRow`. Please do so before reading on.

If you struggled with this, don’t worry. You just haven’t seen the syntax enough. So here it is:

```
```purescript
type FamilyAgesRow r =
  ( fatherAge :: Int, motherAge :: Int, childAge :: Int | r )

type FamilyNamesRow r =
  ( fatherName :: String
  , motherName :: String
  , childName :: String | r )
```
```

+   1. Add the `r` Parameter to both Type Constructors.
+   2. Extend the Row using the `| r` syntax.

Take the time to update your code.

It turns out that when I create Rows, I always create them like this. Then I can combine them to make more complex Rows like:

```
```purescript
FamilyNamesRow (FamilyAgesRow ())
```
```

Here we extend the `FamilyNamesRow` with `FamilyAgesRow`, which is extended with the Empty Row, `()`.

Go ahead and create a `newtype` called `Family` that’s a Record that contains both Row fields, then continue reading.

Here’s the definition:

```
```purescript
newtype Family = Family { | FamilyNamesRow (FamilyAgesRow ()) }
```
```