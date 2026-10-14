![](bbox=[0.19, 0.06, 0.81, 0.336])

Please run this same test. If you already have a user with that userName, then just use user2. But make sure you have the first and last names EXACTLY how I’ve typed it here.

Once the user is created, go to your `server` project and restart the server. What happens?

Here’s what I get:

```
Cannot load accounts: (ParseError "Character 't' did not satisfy predicate"
(Position { line: 3, column: 146 })
```

This is a problem on line 3, which for me is as follows:

```
user,3b7b539fcfa135efbc1c71d2a4edc996042424638884d8b6d9053cfa71914a7628d8fe3dd
00e131537c9d82799bd58d5da86aff0ae905a26c3054a3decd70405,true,false,test,test
                                                                                         ^
                                                                                         |
This is column 146 -----------------------------------------------+
```

Why do you think this is?

If you remember correctly, our Parser doesn’t allow lowercase letters to start a First Name. It also doesn’t allow uppercase letters except for the first character.

We are doing ZERO validation at the API.

There are many solutions:

+   1. Validate in the UI.
+   2. Allow lowercase characters, i.e. change the parser.