the same logic we used in Logon since the Component owns the buttons. We have to inform Modal that we want the button enabled.

We’ll have to check on every Input to determine if we should enable or disable the Create Button. Do this in Component.Modal.CreateUser before reading any further.

Here’s that change:

```
import Data.Array (filter, null) ①
import Data.String.Common (trim)

handleAction
  :: Action
  -> H.HalogenM State Action Slots (InnerOutput Output) m Unit
handleAction = case _ of
  Input f -> do
    state <- H.modify $ f ②
    H.raise if canCreate state then EnableAffirmative
      else DisableAffirmative ③
-- CODE REDACTED
  where
  canCreate s = [ s.userName, s.password, s.firstName, s.lastName ] ④
    <#> trim
    # filter (_ == "")
    # null

  errorMsg' msg = _ { errorMessage = Just msg }

  errorMsg = H.modify_ <<< errorMsg'
-- BELOW CODE REDACTED
```

① Added these imports.

② Modify State and return the updated State, which is why we’re using H.modify without the _.

③ If we can create a User, then enable the button, otherwise disable it.

④ Take an Array of the field values that must be non-empty before we can create a User. Then trim them and filter only empty fields and then check to see if the Array is empty, which means none of the fields are blank.

Now, rebuild the Application, refresh the browser and create a new user and see what happens. Then return here.

When I do this, I cannot tell if anything got created. I can certainly see that that the new User isn’t added to the list on the Users Page.