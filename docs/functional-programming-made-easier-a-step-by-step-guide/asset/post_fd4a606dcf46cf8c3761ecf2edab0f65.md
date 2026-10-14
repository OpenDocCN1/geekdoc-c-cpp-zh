
# 7.21. Hint for `ToCSV`

When we think about encoding something, we first have to determine the Type for the encoding.

Our case is simply a CSV, which could easily be encoded with a `String`. But, we don’t want to accidentally mix up any old `String` with our CSV `Strings`.

So first let’s make a `newtype` for our CSV encoded string. Let’s call it `CSV`.

And to help remind you of the syntax of Typeclasses, here’s our `HasAddress` Typeclass from an earlier Chapter:

```
class HasAddress a where
  getAddress :: a -> Address
```

Take a second stab at writing both the `newtype` and the `class` before venturing further.

## 7.22. Code for `ToCSV`

First, let’s create our `newtype`:

```
newtype CSV = CSV String
```

`CSV` is just a wrapper for a `String`, but has the added benefit of being Type Safe, i.e. the compiler will complain if we pass a `String` in its place.

Next, we’ll write the class:

```
class ToCSV a where
  toCSV :: a -> CSV
```

The Method `toCSV` will take our Type, represented here by `a`, and encode it as a `CSV`.

## 7.23. Using `ToCSV`

Take the following Data Types and make an Instance of `ToCSV` for `Person`:

```
newtype FullName = FullName String

newtype Age = Age Int

data Occupation = Doctor | Dentist | Lawyer | Unemployed

data Person = Person
  { name :: FullName
  , age :: Age
  , occupation :: Occupation
  }
```

Give it a try and see how far you can get. If you're struggling, please consult the following Hint section.

## 7.24. Another Hint for ToCSV

First thing to realize is that it's easiest to implement show for FullName, Age and Occupation before attacking Person's ToCSV instance.

Give it another try before reading ahead.

## 7.25. Code for ToCSV

Let's write the FullName instance first:

```
newtype FullName = FullName String

instance showFullName :: Show FullName where
  show (FullName name) = name ①
```

① We destructure FullName exposing name, which is Type String.

Then we can write the same for Age, but this time we're going to do it a little differently:

```
import Data.Newtype (class Newtype) ①

newtype Age = Age Int
derive instance newtypeAge :: Newtype Age _ ②
derive newtype instance showAge :: Show Age ③
```

① We need to import class Newtype to derive Newtype for Age.

② The Newtype Typeclass lets us derive Typeclasses for our wrapper Type by delegating to the wrapped Type’s implementation. This saves us from having to write and debug our implementation.

③ Derive Show for Age (our wrapper Type) by using Show for Int (our wrapped Type).

We could’ve implemented FullName using this exact techique. Deriving is typically preferable to hand-coding.

Next, we’ll write the show instance for Occupation:

```
import Data.Generic.Rep (class Generic) ①
import Data.Show.Generic (genericShow)

data Occupation = Doctor | Dentist | Lawyer | Unemployed
derive instance genericOccupation :: Generic Occupation _ ②

instance showOccupation :: Show Occupation where
  show = genericShow ③
```

① We need to import these to implement show.

② We need to derive Generic to leverage genericShow.

③ We implement Show using genericShow.

Now, we are poised to write the ToCSV instance for Person:

```
data Person = Person
  { name :: FullName
  , age :: Age
  , occupation :: Occupation
  }

instance toCSVPerson :: ToCSV Person where
  toCSV (Person {name, age, occupation}) = ①
    CSV $ show name <> "," <> show age <> "," <> show occupation ②
```

① Destructure Person and then destructure the fields of its underlying Record.

② We show each field in the order we’ve defined them and then delimit them with commas and wrap the result in CSV.

## 7.26. Testing ToCSV

Try to come up with test code for testing toCSV for Person before looking ahead at my suggestion for a test.

Don’t forget to remove our placeholder code from the test function:

```
log "placeholder"
```

Remove this line.

Here’s some test code if you cannot think of what to write:

```
-- COMPILER ERROR!
log $ show $ toCSV
  (Person
    { name: FullName "Sue Smith"
    , age: Age 23
    , occupation: Doctor
    }) == CSV "Sue Smith,23,Doctor"
```

Cannot compare for equality for a CSV.

Notice how `name` isn’t just a hardcoded `String`, but is a `FullName`. Same issue with `age`.

To make the compiler happy, we need to implement `Eq` for `CSV` so that we can check for Equality:

```
newtype CSV = CSV String
derive instance newtypeCSV :: Newtype CSV
derive newtype instance eqCSV :: Eq CSV
```

First derive `Newtype` to make deriving other Typeclasses easy. We’ll need this later.

Leverage the underlying `String`’s `Eq` instance to derive ours. We could also leave off the `newtype` here since we can derive `Eq` for ANY Type.

Now our test code compiles and can be run:

```
log $ show $ toCSV
  (Person
    { name: FullName "Sue Smith"
    , age: Age 23
    , occupation: Doctor
    }) == CSV "Sue Smith,23,Doctor"
```

Prints `true`.

## 7.27. Writing **FromCSV**

Anytime you encode something, you’ll almost always need to decode it. So let’s make another Typeclass called FromCSV with a single Method called fromCSV.

Looking back at what we did with ToCSV should be helpful. Give it a go and then check your work in the next section.

Also, you're going to need a function called split in the Data.String module. Consult Pursuit to learn more about this function.

## 7.28. Code for FromCSV

The class is pretty straightforward:

```
import Data.Maybe (Maybe) ①

class FromCSV a where
  fromCSV :: CSV -> Maybe a ②
```

① Import the Type Maybe. Note that the constructors are NOT imported. We'll need to rectify that soon.

② Since we are taking a CSV, which is essentially just a String, it's possible that we cannot decode it to our Type, e.g. we encode Type A and then try to decode that to Type B. This potential failure is why we are returning a Maybe.

And now, we can write Person's Instance one step at a time. First, the imports:

```
import Data.Maybe (Maybe(..)) ①
-- COMPILER ERROR!!
import Data.String (Pattern(..), split) ②
```

① Add (..) to include Just and Nothing which fromCSV will need.

② Import for splitting a string based on a Pattern into an Array String.

We're going to need to add the package for the module Data.String. Go look up that module on Pursuit and see what package it belongs in. Then return here.

According to Pursuit, it can be found in purescript-strings.

First, comment out the offending import:

```
-- import Data.String (Pattern(..), split)
```

This will allow us to full build the project.

Add strings to your spago.dhall file and then build the project with:

```
npx spago build
```

We get the following output:

```
[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- strings
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- newtype
```

The warning is expected, but the error tells us that we need to add newtype to spago.dhall.

Do so then rerun:

```
npx spago build
```

Don't forget to uncomment out the import Data.String line.

The next step is the instance:

```
instance fromCSVPerson :: FromCSV Person where
  fromCSV (CSV str) = case split (Pattern ",") str of ① ②
    [name, age, occupation] -> Just $ Person ③
      { name: FullName name
      , age Age ??? ④
      , occupation: ??? ④
      }
    _ -> Nothing
```

① We destructure the CSV to expose its underlying String. We could have just as easily called unwrap in our code. But first, we’d have to derive a Newtype instance for CSV.

② We split the String, str, on Commas. This will return an Array of Strings.

③ We Pattern Match on an Array of length 3. Remember, we can only Pattern Match Arrays of an exact size.

④ The ??? are places we need to convert a String to another Type, an Int for age and Occupation for
