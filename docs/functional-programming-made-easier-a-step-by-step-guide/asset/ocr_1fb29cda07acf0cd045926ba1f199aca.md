```
json: { contents:
    { teacher:
        { contents:
            { status: { tag: 'NonTenured' },
              personal:
                { contents: { weight: 63.5, height: 162.56, age: 31 },
                  tag: 'Personal' },
              numberOfStudents: 23,
              grades:
                [ { tag: 'Preschool' },
                  { tag: 'Kindergarten' },
                  { contents: 1, tag: 'Grade' } ] },
        tag: 'Teacher' },
    personal:
        { contents: { weight: 17.9, height: 107.9, age: 5 },
          tag: 'Personal' },
    grade: { contents: 1, tag: 'Grade' },
    gpa: 3.2 },
  tag: 'Student' }
```

Remember that this is what we’re giving decodeJSON. Ask yourself if this looks like what decodeJSON wants:

```
decodeJSON :: ∀ a. Decode a => String -> F a
```

Can you see it now?

Okay, if you realized that this is NOT a String, then kudos to you. _reverseKeys works with a Javascript Object. If you remember, that’s why we’re calling parseJSON, i.e. to convert the String to a Foreign.

The problem is that we told the compiler that _reverseKeys would return a String:

```
foreign import _reverseKeys :: Foreign -> String
```

But it doesn’t. I lied to the compiler and now I’m paying the price.

So, we need to stringify the Javascript Object before we return it from _reverseKeys. Note that we CANNOT make reverseKeys do this since it’s recursive.

But we can make _reverseKeys do this: