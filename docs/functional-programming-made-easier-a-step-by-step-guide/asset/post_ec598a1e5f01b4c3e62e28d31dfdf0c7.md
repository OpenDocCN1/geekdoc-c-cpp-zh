
Understanding these Lifecycle issues is very important for creating both a performant Application, as well as a properly functioning one.

To fix the compiler error, the Users Component needs to accept Input from its Parent, the Router Component. Remember this is handled by the receive Function in the EvalSpec.

First, create an Action in Component.Users called SelectedUserName that takes a Maybe String and then stub out the handling of it in handleAction. And second, implement receive in the EvalSpec. Then return here and continue reading.

Here’s the first part:

```
type Input = Maybe String ①

data Action
  = Initialize
  | UserSelected User
  | SelectedUserName (Maybe String) ②

-- ABOVE CODE REDACTED
  handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
  handleAction = case _ of
-- CODE REDACTED
  UserSelected (User { userName }) -> navigate $ Route.Users $ Just userName
  SelectedUserName _ -> pure unit ③
```

① Change from Unit to Maybe String.

② Added Action to handle Input from our Parent.

③ Stubbed out code for handling our new Action.

Here’s the second part:

```
component
  :: ∀ m
    . MonadAff m
  => MonadAsk Env m
  => Navigate m Route
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> ①
      { authorized: false
      , selectedUser: Nothing
      , users: []
      }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction
      , receive = Just <<< SelectedUserName ②
      , initialize = Just Initialize
      }
  }
```

① We’re currently throwing away the Input we get initially since we have no users. We’ll need to fix this.

② Input from our Parent produces the Action, SelectedUserName.

Notice that initialState isn’t using the userName that it gets from its Parent, i.e. the Router Component.

We cannot look up the user here since we don’t have any users yet since we haven’t called the backend yet to get them.

We’ll need to store this Value in the State so when we do get the users from our server API, we can then select the current user, if there is one.

Make that change to the code to simply store the initial username calling our new field initUserName before reading on.

Here’s that change:

```
type State =
  { authorized :: Boolean
  , selectedUser :: Maybe User
  , users :: Array User
  , initUserName :: Maybe String ①
  }

-- ABOVE CODE REDACTED
component = H.mkComponent
  { initialState: \initUserName -> ②
    { authorized: false
    , selectedUser: Nothing
    , users: []
    , initUserName ③
    }
  }
-- BELOW CODE REDACTED
```

① Added initial user name field that might be Nothing depending on the initial URL Hash path.

② We no longer throw away the Input Parameter.

③ We initialize our new field with initUserName that we get from the Router Component, i.e. our Parent.

We now need to change the Initialize case in handleAction to update selectedUser AFTER it successfully gets the users back from the QueryUsersRequest API call.

Let’s start by coding:

```
-- ABOVE CODE REDACTED
    Right (QueryUsersResponse
      (QueryUsersResultsSuccess { users })) ->
      H.modify_
        { authorized = true
        , users = users
        , selectedUser = initUserName <#> \userName -> ??? ①
        }
-- BELOW CODE REDACTED
```

① We need to find the user with the specified userName.

It should be obvious that I made a mistake when I made users an Array:

```
type State =
  { authorized :: Boolean
  , selectedUser :: Maybe User
  , users :: Array User
  , initUserName :: Maybe String
  }
```

It would be so much better if this was a Map whose key was userName.

Comment out this unfinished line of code and fix my mistake by changing users in State to be a Map and then fix the code anywhere that this change breaks by using Map instead Array.

Then return here and continue reading.

First, we’ll change State:

```
import Data.Map (Map) ①

type State =
  { authorized :: Boolean
  , selectedUser :: Maybe User
  , users :: Map String User ②
  , initUserName :: Maybe String
  }
```

① Added this import.

② Changed from Array to Map.

Next, we’ll fix render to work with the Values of the Map of users:

```
import Data.Array (fromFoldable) ①
import Data.Map as Map

    render :: State -> H.ComponentHTML Action Slots m
    render { authorized, users, selectedUser } = ②
    -- CODE REACTED
        (Map.values users # fromFoldable ③
            <# \(user@(User { userName })) ->
                HH.li [
                    HP.class_ $ ClassName "list-group-item"
                , HC.style do
                    backgroundColor paperColor
                    cursor pointer
                , HE.onClick $ const $ UserSelected user
                ]
                [ HH.text userName ])
    -- BELOW CODE REACTED
```

① Added these imports.

② Destructure selectedUser also.

③ Use just the values from the Map. We have to convert the List that we get back from Map.values into Array using fromFoldable.

Next, we’ll fix initialize:

```
-- ABOVE CODE REACTED
component = H.mkComponent
    { initialState: \initUserName ->
        { authorized: false
        , selectedUser: Nothing
        , users: Map.empty ①
        , initUserName
        }
    , render
    , eval: H.mkEval H.defaultEval
        { handleAction = handleAction
        , receive = Just <<< SelectedUserName
        , initialize = Just Initialize
        }
    }
```

① Changed from empty Array to empty Map.

And finally, we’ll convert the Array of users we get back from QueryUsersRequest into a Map:

```
import Data.Foldable (foldl) ①
import Data.Newtype (unwrap)

-- ABOVE CODE REDACTED
    Right (QueryUsersResponse
        (QueryUsersResultsSuccess { users })) ->
    let mkMap f =
        foldl (\m r -> Map.insert (f r) r m) Map.empty in ②
    H.modify_ _
        { authorized = true
        -- COMPILER ERROR!!
        , users = mkMap (_ .userName <<< unwrap) users ③
        -- , selectedUser = initUserName <#> \userName ->
        }
-- BELOW CODE REDACTED
```

① Added these imports.

② mkMap will take an Array of Records and use f to produce a Key from each Record. It will then add that Key and the Record as the Value to the Map.

③ Using unwrap to get contained Record from User.

We’ll get a compiler error since we’ve used unwrap in the above code. This is because User doesn’t have a Newtype Instance.

So, we’ll have to go the the server code where User is defined and make a it has a Newtype Instance:

```
import Prelude ①
import Data.Newtype (class Newtype)

newtype User = User (Record (UserRow ()))
derive instance genericUser :: Generic User _
derive instance newtypeUser :: Newtype User _ ②
```

① Added these imports.

② Derive Newtype.

Now return to the client code and run:

```
make build
```

This will build the code from our newly changed code from the server.

But this will produce an error:

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- arrays
- foldable-traversable
- newtype
- ordered-collections
```

Add these to spago and then re-build:

```
make build
```

Then return to Component.Users and save the file and the compiler error should disappear.

Now that my bad decision to make users an Array is fixed, we can return to that line of code we commented out:

```
-- ABOVE CODE REDACTED
    Right (QueryUsersResponse
        (QueryUsersResultsSuccess { users })) ->
    let mkMap f = foldl (\m r -> Map.insert (f r) r m) Map.empty in
    H.modify_ _
        { authorized = true
        , users = mkMap (_.userName <<< unwrap) users
        -- , selectedUser = initUserName <#> \userName -> ①
        }
-- BELOW CODE REDACTED
```

① This line is unfinished.

Uncomment the unfinished line of code and finish coding it to look up the initUserName in the Map of users. Once you’ve done that, return back here and continue.

Here’s that change:
