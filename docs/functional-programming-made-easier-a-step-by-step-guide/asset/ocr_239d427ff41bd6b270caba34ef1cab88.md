```
{ grades: [ Preschool, Kindergarten,
, numberOfStudents: 23
, personal: {
  height: Centimeters 162.56
, weight: Kilograms 63.5
, age: Years 31
}
, status: NonTenured
}

processAjaxResult :: ∀ a. Show a => Pr
processAjaxResult _ = case _ of
  Left err -> Ajax.printError err
  Right { body } -> case runExcept $ (decodeJSON body :: _ a) of
    Left err -> show err

No type class instance was found for
Foreign.Generic.Class.Decode a1

while applying a function decodeJSON
of type Decode t2 => String -> ExceptT (NonEmpty
to argument body
while checking that expression decodeJSON body
has type t0 a1
in value declaration processAjaxResult
```

Well, I remembered to make a showable, but forgot that it must have a Decode Instance too since we’re calling decodeJSON and it’s expecting it to decode a Value of Type _ a.

Let’s fix that:

```
processAjaxResult
  :: ∀ a
    . Show a
    => Decode a ①
    => Proxy a
    -> Either Ajax.Error (Ajax.Response String)
    -> String
processAjaxResult _ = case _ of
  Left err -> Ajax.printError err
  Right { body } -> case runExcept (decodeJSON body :: _ a) of
    Left err -> show err
    Right reversedTeacher -> show reversedTeacher
```

① Added Decode Constraint.

And now the compiler is happy. But, I’m not. I see one more little thing that we could improve.

Notice the Variable name reversedTeacher. That’s not accurate anymore. It’s not just a reversed version of Teacher anymore. It could be any reversed JSON Object.

Let’s rename it to reversedRecord: