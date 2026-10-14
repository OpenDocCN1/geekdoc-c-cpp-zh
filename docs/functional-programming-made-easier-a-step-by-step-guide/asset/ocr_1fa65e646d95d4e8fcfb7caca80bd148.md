```
-- ABOVE CODE REDACTED
    [ HH.ul_
        (users <# \user@(User { userName }) -> ①
            HH.li [
                HP.class_ $ ClassName "list-group-item"
            , HC.style do
                backgroundColor paperColor
                cursor pointer
            , HE.onClick $ const $ UserSelected user ②
            ]
            [ HH.text userName ])
        ]
    ]
```

① Named the Parameter user using the @ syntax.

② Added HE.onClick. The const is to throw away the MouseEvent and just return an Action.

Now, go back to handleAction and write the code to handle the selection of a User by navigating to Route.User. Don’t forget that Route.User’s first Parameter is a String, i.e. the userName, which uniquely identifies the user that is selected.

Then when you’re done, return here and continue reading.

First, we’ll make the change to handleAction to navigate:

```
import Capability.Navigate (class Navigate, navigate) ①
import Data.Route as Route ②

-- ABOVE CODE REDACTED
    UserSelected (User { userName }) -> ③
        navigate $ Route.Users $ Just userName ④
-- BELOW CODE REDACTED
```

① Added navigate to the import list.

② Added this import.

③ Destructure User to get at userName.

④ Navigate to the Users route with the userName, which will dictate which user in the list of users is highlighted and whose information will be displayed to the right of the list of users.

Next, we have to handle the userName from the Route in the render Function in Component.Router.

Currently, we don’t do anything with it. Here’s the current code for reference: