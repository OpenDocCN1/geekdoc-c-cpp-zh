```
import Capability.Navigate (class Navigate, navigate) ①

-- ABOVE CODE REDACTED
    where
    handleQuery
        :: ∀ a
          . Query a
        -> H.HalogenM State Action Slots Output m (Maybe a)
    handleQuery = case _ of
        Navigate route a -> do
            { userRef } <- ask
            ref <- H.liftEffect $ Ref.read userRef
            if isNothing ref then navigate Logon ②
            else H.modify_ _ { route = route } ③
                pure (Just a)
-- BELOW CODE REDACTED
```

① Added navigate to the import list.

② Now we explicitly navigate to Logon. This will change the Hash in the Address Bar of the Browser.

③ Otherwise, we just abide by the requested route.

Now, rebuild the client:

```
make build
```

And refresh the Browser.

When I do this, my Hash is /logon.

Log back on and try out the Users button to see what happens.

It goes to the Users Page when I click it. Now, refresh the page and see if you go back to the Logon Page with the correct Hash.

When I did that, it does. So, it looks like our Hash Routing is working much better now.

# 30.11. Users Page

The Users Page is will contain a list of users to the left and when the user clicks on a User from the list, we will route to the Users Page, but this time with a User selected.

This routing will allow the Browser back buttons to work in a more natural way that users have come to expect.