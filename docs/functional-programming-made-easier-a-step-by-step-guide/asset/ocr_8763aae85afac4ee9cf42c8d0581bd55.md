```
teacher :: Teacher
teacher =
  { grades: [ Preschool, Kindergarten, Grade 1 ]
  , numberOfStudents: 23
  , personal: {
      height: Centimeters 162.56
    , weight: Kilograms 63.5
    , age: Years 31
    }
  , status: NonTenured
  }
```

Notice how personal doesn’t have a Data Constructor. It didn’t used to need one, but we added a Data Constructor to Personal when we made it a real Type. So, we need to add it here too.

Turns out that teacher doesn’t have a Data Constructor either.

Go ahead and fix this before reading on.

Here’s the fix:

```
teacher :: Teacher
teacher = Teacher ①
  { grades: [ Preschool, Kindergarten, Grade 1 ]
  , numberOfStudents: 23
  , personal: Personal { ②
      height: Centimeters 162.56
    , weight: Kilograms 63.5
    , age: Years 31
    }
  , status: NonTenured
  }
```

① Added Teacher Data Constructor.

② Added Personal Data Constructor.

With Type Aliases, we can just use Records, but now, with newtype, we need to pass those Records to the proper Data Constructors.

Next, we’ll code an Argonaut decoder for Grade, i.e. a DecodeJson Instance.

Note the different names in the different libraries. Foreign’s Typeclass is Decode, whereas Argonaut’s is called DecodeJson. Same goes for Encode to EncodeJson.