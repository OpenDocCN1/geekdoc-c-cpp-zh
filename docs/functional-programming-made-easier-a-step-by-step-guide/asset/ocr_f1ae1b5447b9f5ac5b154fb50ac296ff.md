```
data Action
= Logon
  | Input String ①

-- ABOVE CODE REDACTED
    [ HH.label [
        HC.style do
            width (rem 6.0)
        ] [ HH.text "Username: " ]
    , HH.input [
        HE.onValueInput Input ②
    , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
        ]
    ]
-- CODE REDACTED
    [ HH.label [
        HC.style do
            width (rem 6.0)
        ] [ HH.text "Password: " ]
    , HH.input [
        HP.type_ InputPassword
    , HE.onValueInput Input ②
    , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
        ]
    ]
-- BELOW CODE REDACTED
```

① Added Input Data Constructor. The String Parameter is given to us by onValueInput.

② Added the Event Handler for both fields.

Note that onValueInput takes a Function of Type String -> Maybe a. This allows for us to reject the input in the render logic. We could also reject it handleAction.

Let’s look at our component creation code: