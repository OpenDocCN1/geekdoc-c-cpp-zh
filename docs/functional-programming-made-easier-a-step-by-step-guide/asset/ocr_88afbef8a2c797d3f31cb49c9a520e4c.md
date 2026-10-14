```
test :: Effect Unit
test = launchAff_ do
    results <- parSequence $ (\json -> Ajax.post ResponseFormat.json
        "http://localhost:3000/"
        $ Just $ RequestBody.String json)
    <$> [
        encodeJSON testTeacher
      , encodeJSON testStudent
    ]
    log $ case map (_body) <$> sequence results of
        Left err -> Ajax.printError err
        Right [teacherJson, studentJson] ->
            show (decodeJson teacherJson :: _ Teacher) <> "\n\n"
            <> show (decodeJson studentJson :: _ Student)
        Right _ ->
            "The number of Ajax calls is different than what's being processed."
```

Now go ahead and make this change and then clean up the unused imports.

And finally, run this to see what you get.

And of course, spago is complaining:

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- parallel
```

Add this and run it again. When I do, I got:

```
(Right (Teacher { grades: [Preschool,Kindergarten,(Grade 1)],
numberOfStudents: 23, personal: (Personal { age: (Years 31), height:
(Centimeters 162.56), weight: (Kilograms 63.5) }), status: NonTenured }))

(Right (Student { gpa: (GPA 3.2), grade: (Grade 1), personal: (Personal { age:
(Years 5), height: (Centimeters 107.9), weight: (Kilograms 17.9) }), teacher:
(Teacher { grades: [Preschool,Kindergarten,(Grade 1)], numberOfStudents: 23,
personal: (Personal { age: (Years 31), height: (Centimeters 162.56), weight:
(Kilograms 63.5) }), status: NonTenured }) }))
```

We've decode the reversed-keys version of our Types every way we planned to except for using Javascript.