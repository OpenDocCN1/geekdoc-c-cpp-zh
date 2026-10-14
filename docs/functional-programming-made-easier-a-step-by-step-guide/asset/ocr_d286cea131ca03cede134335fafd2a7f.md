Update your code to make this improvement and rebuild and run your server to see the new error message.

When I run this, I get:

```
Cannot load accounts: (ParseError "Failed to parse complete file" (Position {
line: 10, column: 155 }))
```

This message is so much better than the old generic one.

Now, edit your accounts.csv to remove the McCloud account and restart your server. Then return to your client project.

Now that we’ve fixed our parser, there’s one last thing I’d like to do before we leave the Users Page. I’d like the newly added User to be the selectedUser. This way it’s selected in the list and the information will show on the right.

Make that change to Component.Users and then return here.

Here’s that change:

```
-- ABOVE CODE REDACTED
    CreateUserModal output -> case output of
        Modal.Affirmative -> H.modify_ _ { creatingUser = false }
        Modal.Negative -> H.modify_ _ { creatingUser = false }
        Modal.InnerOutput user@(User { userName }) ->
            H.modify_ \s ->
                s { users = Map.insert userName user s.users
                  , selectedUser = Just user } ①
-- BELOW CODE REDACTED
```

① Make the newly created user the selected user.

Now, rebuild, refresh the Browser and create a new user.

Here’s how it should looks right after hitting the Create Button:

![](bbox=[0.146, 0.768, 0.854, 0.942])