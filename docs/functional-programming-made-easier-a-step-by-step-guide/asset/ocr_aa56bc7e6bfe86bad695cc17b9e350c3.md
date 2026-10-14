wraps something more complicated than a String or if we want our newtype to be an instance of something not derivable, e.g. HasAddress.

Let’s revisit Person and HasAddress:

```
newtype Person = Person ①
  { name :: String
  , age :: Int
  , address :: Address
  }

instance hasAddressPerson :: HasAddress Person where ②
  getAddress (Person p) = p.address

newtype Ceo = Ceo Person ③

newtype Janitor = Janitor Person ③
```

① Notice this is a newtype whereas previously we defined this with data.

② Here’s the same HasAddress instance implementation from before.

③ We have a newtype for Ceo and Janitor, presumably to make sure we don’t call Ceo functions with a Janitor.

Go ahead and write HasAddress for both Ceo and Janitor. Try not to look ahead, but please, by all means, look back at what we’ve done so far.

There are multiple ways to implement HasAddress instances for Ceo and Janitor.

First, Hand-coded:

```
instance hasAddressCeo :: HasAddress Ceo where
  getAddress (Ceo p) = getAddress p ①

instance hasAddressJanitor :: HasAddress Janitor where
  getAddress (Janitor p) = getAddress p ①
```

① We use Pattern Matching to unwrap Person.

Next, we write it generically using unwrap from Newtype: