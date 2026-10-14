You should have:

```
```purescript
module AppTheme where

import Prelude

import CSS (CSS, fontFamily)
import CSS.Color (Color, rgb)
import CSS.Font (sansSerif)
import Data.NonEmpty ((:|))

paperColor :: Color
paperColor = rgb 0xd9 0xd9 0xd9

themeColor :: Color
themeColor = rgb 0x00 0x66 0x75

themeFont :: CSS
themeFont = fontFamily [ "Verdana" ] $ sansSerif :| []
```
```

Now, clean up the redundant imports and add the following import to `Component.Page`:

```
```purescript
import AppTheme (themeColor, paperColor, themeFont)
```
```

Quick side note: In VSCode, once your PureScript file compiles and if you have a bunch of redundant imports, you’ll notice a Light Bulb Icon pop up near your cursor:

![](bbox=[0.323, 0.626, 0.678, 0.693])

You can click the Light Bulb Icon and you’ll get a menu:

![](bbox=[0.367, 0.739, 0.634, 0.821])

Picking the `Apply all import suggestions` will clean up your redundant imports automatically. I haven’t had great luck with the other menu items, but your mileage may vary.

Next, create a Folder under `src` called `CSS`. Then create a File under that called `Missing.purs`.

Put the following into that File: