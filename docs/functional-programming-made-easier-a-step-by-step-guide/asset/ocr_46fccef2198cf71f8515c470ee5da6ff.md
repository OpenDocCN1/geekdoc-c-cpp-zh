```
cursor pointer
    , HE.onClick $ const Logon
    ]
    [ HH.text "LOGON" ]
    ]
]
```

Most of this code is styling, but there are a few things to take note of, e.g. how we specify that an Input field is a Password:

```
import DOM.HTML.Indexed.InputType (InputType(..)) ①

-- ABOVE CODE REDACTED
    , HH.input [
        HP.type_ InputPassword ②
        , HC.style do
            backgroundColor paperColor
            width (vw 8.3)
            paddingLeft (rem 0.5)
            paddingRight (rem 0.5)
            fontSize (vw 1.0)
-- BELOW CODE REDACTED
```

① We need to import the InputType Type, which has Data Constructors for types of input fields.

② Set the type Property to InputPassword.

Another notable item is the button click handling: