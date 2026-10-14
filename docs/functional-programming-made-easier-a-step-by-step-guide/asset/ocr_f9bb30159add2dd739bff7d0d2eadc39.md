③ Changed this to use isSelected.

④ Added this style to change the text color from black to white when selected.

Now, rebuild the Application and retest and see how it looks.

I think our change looks much better.

And the final step for our Users Page is to display the User information to the right. Since this part of the code is pretty much just HTML and CSS, I'm just going to give it to you whole.

Please take the time to try to understand what it's doing:

```
import CSS.Geometry (minWidth, padding, paddingBottom, paddingRight) ①
import CSS.Flexbox (flexDirection, row, column, flexGrow, flexBasis
    , justifyContent, alignItems, flexStart) ②
import CSS.Size (rem, pct) ③

-- ABOVE CODE REDACTED
    [ HH.ul_
        (Map.values users # fromFoldable
            <# \(user@(User { userName })) ->
            let isSelected = Just user == selectedUser in
            HH.li [
                HP.class_ $ ClassName "list-group-item"
            , HC.style do
                backgroundColor
                    if isSelected then selectedColor
                    else paperColor
                color
                    if isSelected then white
                    else black
                cursor pointer
            , HE.onClick $ const $ UserSelected user
            ]
            [ HH.text userName ])
    ]
    , selectedUser # maybe (HH.text "") \(User user) -> ④
        let item h = HH.div [ HC.style $ paddingBottom (rem 0.5) ] [ h ] in ⑤
        HH.div [
            HC.style do
                display flex
                flexDirection row
                flexBasis (pct 100.0)
                backgroundColor paperColor
```