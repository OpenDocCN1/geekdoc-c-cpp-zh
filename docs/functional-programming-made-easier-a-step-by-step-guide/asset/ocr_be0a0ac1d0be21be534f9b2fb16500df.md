```
```haskell
render :: State -> H.ComponentHTML Action Slots m
render { loggedOff, errorMessage } =
  HH.div
    [
      HC.style do
        display flex
        flexDirection row
        alignItems center
        justifyContent center
        paddingTop $ vw 0.65
    ]
    if loggedOff then
      [ HH.text "You have been successfully logged off"
      , HH.button
          [
            HC.style do
              backgroundColor themeColor
              themeFont
              fontWeight $ FontWeight $ value "500"
              fontSize $ vw 1.0
              width (rem 20.0)
              height $ vw 3.0
              color white
              cursor pointer
          , HE.onClick $ const Click
          ]
          [ HH.text "Log Back On" ]
      ]
    else [] <> 
      [ (errorMessage # maybe (HH.text "") \message ->
          HH.slot _modal unit
            (Modal.component ModalCommon.errorConfig Message.component)
            message Modal)
      ]
```
```

+   1. Destructure to get `loggedOff`.
+   2. If `loggedOff` then prepend this `Array` of HTML Elements to the Modal Child Element.
+   3. Otherwise, prepend an empty `Array`.

And finally, we need to call the Logoff API when we land on the Page. That will warrant an `Intialize` Action: