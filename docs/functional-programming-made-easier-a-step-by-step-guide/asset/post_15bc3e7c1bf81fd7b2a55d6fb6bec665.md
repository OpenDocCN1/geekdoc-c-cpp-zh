
glueNames ①
  :: ∀ a b
    . Newtype a String ②
  => Newtype b String ②
  => String
  -> a
  -> b
  -> String
glueNames between n1 n2 = unwrap n1 <> between <> unwrap n2 ③

lastNameFirst :: LastName -> FirstName -> String ④
lastNameFirst = glueNames ", " ⑤

fullName :: FirstName -> LastName -> String ④
fullName = glueNames " " ⑥

① When Type Signatures become long, this is an alternative formatting that is commonly used. It takes a bit of getting used to, but definitely helps readability.

② We are constraining both a and b to be newtypes that have instances of Newtype. They also must both wrap a String Type. Both FirstName and LastName fit this requirement.

③ Our generic function to glue these names together uses Newtype’s unwrap Method completely oblivious to the actual Types.

④ Notice the order of Parameters is flipped between lastNameFirst and fullName. Since glueNames doesn’t care about the exact types, we have this flexibility. The only thing glueNames requires is that it gets two newtypes that both wrap String.

⑤ We call glueNames with a comma as our delimiter. This is written in Point-free notation where last name and first name are not explicitly specified.

⑥ We call glueNames with a space as our delimiter. This too is written in Point-free notation, where first name and last name are not explicitly specified.

## 6.8. Deriving Instances using newtype

Let’s revisit FirstName and derive it’s Eq instance:

```
newtype FirstName = FirstName String
derive instance newTypeFirstName :: Newtype FirstName _
derive instance eqFirstName :: Eq FirstName ①
```

① Deriving Eq.

That was easy since we can always derive Eq. But things become a bit more complicated when our newtype wraps something more complicated than a String or if we want our newtype to be an instance of something not derivable, e.g. HasAddress.

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

```
import Data.Newtype (class Newtype, unwrap) ①

newtype Ceo = Ceo Person
derive instance newtypeCeo :: Newtype Ceo _ ②

newtype Janitor = Janitor Person
derive instance newtypeJanitor :: Newtype Janitor _ ②

genericPersonHasAddress :: ∀ a. Newtype a Person => a -> Address ③
genericPersonHasAddress wrappedPerson =
  getAddress $ unwrap wrappedPerson ④

instance hasAddressCeo :: HasAddress Ceo where
  getAddress = genericPersonHasAddress ⑤

instance hasAddressJanitor :: HasAddress Janitor where
  getAddress = genericPersonHasAddress ⑤
```

① We need to import Newtype Class and unwrap.

② We need to make Ceo and Janitor instances of Newtype Class.

③ a is any type as long as it’s a Newtype that wraps Person, which is what Newtype a Person means.

④ We unwrap Person and then call getAddress with it. Remember that since getAddress’s a is Person, the compiler will call Person’s getAddress Method.

⑤ We can now leverage genericPersonHasAddress for both Ceo and Janitor. This is very similar to how we used genericShow.

While this is more code than hand coding, the real benefit here is that every single Type that wraps Person can now leverage genericPersonHasAddress.

And finally, we can write these instances by using derive newtype:

```
import Data.Newtype (class Newtype) ①

newtype Ceo = Ceo Person
derive instance newtypeCeo :: Newtype Ceo _ ②
derive newtype instance hasAddressCeo :: HasAddress Ceo ③

newtype Janitor = Janitor Person
derive instance newtypeJanitor :: Newtype Janitor _ ②
derive newtype instance hasAddressJanitor :: HasAddress Janitor ③
```

① We need to import Newtype Class.

② We need to make `Ceo` and `Janitor` instances of `Newtype` Class.

③ I cheated and used `derive newtype`.

In the final version, I cheated by using something we haven’t seen yet, `derive newtype`. This tells the compiler that our Type is just a `newtype`, so derive the instance, in this case `HasAddress`, by calling the wrapped Type’s implementation, viz. `Person`’s `HasAddress` instance.

This is very convenient and saves us from having to write boilerplate code. It’s also something the compiler can do for us very easily.

One very important point when using this technique is that the underlying Type MUST implement the instance. If `Person` didn’t have a `HasAddress` instance, then the compiler would have complained.

## 6.9. Overlapping Instances

Take the following instances:

```
data Overlap = Overlap

instance overlapShow1 :: Show Overlap where
  show = "Overlap 1"

instance overlapShow2 :: Show Overlap where -- COMPILER ERROR!
  show = "Overlap 2"
```

The compiler isn’t happy to see two instances for showing `Overlap`. The truncated error message is:

```
Overlapping Typeclass instances found for

    Data.Show.Show Overlap
```

You can understand why this is not allowed since there’d be no way for the compiler to resolve which of these to use.

But there are times we need to deal with such a situation. Let’s look at the following Class to `Combine` values:

```
class Combine a where
  combine :: a -> a -> a ❶
```

❶ Takes an `a` and another `a` and combines them somehow and produces another `a`.

If we want to combine Ints using addition, we’d make the following instance of Combine:

```
instance combineInt :: Combine Int where
    combine = (+)
```

But what if we also want to combine Ints using multiplication, in the same program:

```
instance combineMultInt :: Combine Int where -- OVERLAPPING INSTANCES!!
    combine = (*)
```

The problem is that we have two ways of combining Ints in the same module, package or program. It would be fine if we had one way for Ints and one way for Strings. But, in this case, we have two ways for Ints.

There is a way out of our quagmire by creating newtypes for Int. One Type that combines using addition and another that combines using multiplication:

```
newtype AddInt = AddInt Int ①
newtype MultiInt = MultiInt Int ②

instance combineAddInt :: Combine AddInt where
    combine (AddInt x) (AddInt y) = AddInt (x + y) ③

instance combineMultiInt :: Combine MultiInt where
    combine (MultiInt x) (MultiInt y) = MultiInt (x * y) ④
```

① Our newtype for additive combinations.

② Our newtype for multiplicative combinations.

③ Destructure our Parameters and compute their sum rewrapping them back up into an AddInt.

④ Destructure our Parameters and compute their product rewrapping them back up into an MultiInt.

So instead of using Ints, we use either AddInts or MultiInts and there is no ambiguity and no Overlapping Instances.

But what if our Types aren’t Monomorphic? In the above case, we had the concrete Type, Int.

Here’s a Polymorphic example:

```
class IsRecord a where
  isRecord :: a -> Boolean

instance isRecordRecord :: IsRecord (Record a) where
  isRecord _ = true

instance isRecordOther :: IsRecord a where -- COMPILER ERROR
  isRecord _ = false
```

+   1. Here we have a Class whose `isRecord` Method returns `true` if it’s a `Record`.
+   2. This is `Record`'s instance for `IsRecord`.
+   3. What we’re trying to do here is write an instance for EVERY OTHER Type to have it return `false` since we’ve already handled the `Record` instance.

The compiler isn’t happy with this. Can you see why?

It may be clear to us what we’re trying to do here, and it works fine for every Type except for `Record`.

When the Type is `Record a`, it matches both instances. In the first instance, `Record a` unifies with `Record a`. In the second instance, `Record a` unifies with `a`. (Remember the `a` in `Record a` is different than `a` in `class IsRecord a`.)

What we need is a way to specify the first instance as a specific case and to specify the second as a Catch-All. And we can do exactly that with *Instance Chaining*.

```
class IsRecord a where
  isRecord :: a -> Boolean

instance isRecordRecord :: IsRecord (Record a) where
  isRecord _ = true
else instance isRecordOther :: IsRecord a where
  isRecord _ = false
```

The addition of the keyword `else` "Chains" these two instances together.

When using Instance Chaining, order matters. So if we were to swap the instance order the compiler will NOT complain. It just will NEVER use the second one since `a` will match all Types. This is the same issue we’ve seen with Pattern Matching.

## 6.10. Orphaned Instances

There are some restrictions on where we can define instances of Classes and for good reason, which will become apparent soon enough:
