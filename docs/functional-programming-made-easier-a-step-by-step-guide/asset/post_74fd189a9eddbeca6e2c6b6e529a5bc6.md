
```purescript
red :: Style
red = "red"

bold :: Style
bold = "bold"

test :: Effect Unit
test = log $ chalk [ red, bold ] "Test" <> chalk [ red ] "Test"
```

While this is better, it doesn’t prevent the following:

```purescript
test :: Effect Unit
test = log $ chalk [ red, bold ] "Test"
    <> chalk [ red, "crash" ] "Test"
```

① Added "crash".

We need a Type that is not a String, but can be converted into a String for chalk to use. How might we accomplish this?

If you’re thinking about using newtype, let’s see how that might work:

```purescript
newtype Style = Style String

red :: Style
red = Style "red"

bold :: Style
bold = Style "bold"
```

This certainly protects us from random Strings thanks to the newtype, i.e. Style.

But how do we pass an Array Style to our Javascript Function that’s expecting an Array String?

Way back when we learned about newtype, I mentioned that there were some optimizations that the compiler could make for newtypes. One of those optimizations is that the newtype is represented internally at runtime as the underlying Type.

We can see this by changing our test code to add the following:

```purescript
import Debug (spy)

newtype Style = Style String

red :: Style
red = Style "red"

test :: Effect Unit
test = do
  let x = spy "red" red
  pure unit
```

① Import spy and add debug to spago.dhall.

② Print the internal representation of red.

This outputs:

```text
red: 'red'
```

red is stored as a Javascript String. That means we don’t have to do anything special with Style since it’s just a newtype. This also means that if we pass an Array Style it’s going to pass Array String to our Javascript Function.

I’ve set up a GitHub Gist of a PureScript module that contains all of the valid Styles. You can find it here at this link, ChalkStyles.purs. Click it.

If you don’t have access to GitHub, here’s the code:

```purescript
module ChalkStyles where

newtype Style = Style String

black :: Style
black = Style "black"

red :: Style
red = Style "red"

green :: Style
green = Style "green"

yellow :: Style
yellow = Style "yellow"

blue :: Style
blue = Style "blue"

magenta :: Style
magenta = Style "magenta"

cyan :: Style
cyan = Style "cyan"

white :: Style
white = Style "white"

blackBright :: Style
blackBright = Style "blackBright"

gray :: Style
gray = Style "gray"

grey :: Style
grey = Style "grey"

redBright :: Style
redBright = Style "redBright"

greenBright :: Style
greenBright = Style "greenBright"

yellowBright :: Style
yellowBright = Style "yellowBright"

blueBright :: Style
blueBright = Style "blueBright"

magentaBright :: Style
magentaBright = Style "magentaBright"

cyanBright :: Style
cyanBright = Style "cyanBright"

whiteBright :: Style
whiteBright = Style "whiteBright"

bgBlack :: Style
bgBlack = Style "bgBlack"

bgCyanBright :: Style
bgCyanBright = Style "bgCyanBright"

bgWhiteBright :: Style
bgWhiteBright = Style "bgWhiteBright"

reset :: Style -- Resets the current color chain.
reset = Style "reset"

bold :: Style -- Make text bold.
bold = Style "bold"

dim :: Style -- Emitting only a small amount of light.
dim = Style "dim"

italic :: Style -- Make text italic. (Not widely supported)
italic = Style "italic"

underline :: Style -- Make text underline. (Not widely supported)
underline = Style "underline"

inverse :: Style -- Inverse background and foreground colors.
inverse = Style "inverse"

hidden :: Style -- Prints the text, but makes it invisible.
hidden = Style "hidden"

strikethrough :: Style -- Puts a horizontal line through the center of the text. (Not widely supported)
strikethrough = Style "strikethrough"

visible :: Style -- Prints the text only when Chalk has a color level > 0. Can be useful for things that are purely cosmetic.
visible = Style "visible"
```

Add this file to your project. Make sure to name it `ChalkStyles.purs` and put it under `src`.

Then change your test code to use it before continuing.

First thing to do is remove the following from `Ch27a.purs`:

```purescript
type Style = String
```

Then import ChalkStyles:

```purescript
import ChalkStyles (Style, bold, red)
```

And finally, change our Strings to Styles in our test code:

```purescript
test :: Effect Unit
test = log $ chalk [ red, bold ] "Test" <> chalk [ red ] "Test"
```

Now run it again and it should produce the same output.

Okay, now change your program in the following ways:

```purescript
import ChalkStyles (Style(..), bold, red)

test :: Effect Unit
test = log $ chalk [ red, bold ] "Test"
    <> chalk [ red, Style "crash" ] "Test"
```

① Include Data Constructors for Style.

② Add our own Style that’s unsupported and will crash our program.

Run the test code and see what happens.

It crashes.

The problem is that we have access to the Style Data Constructor and can create any Style we like, even ones that chalk doesn’t support.

So, how do we prevent this?

To fix this, we need to export out the Type and all of the valid styles, but NOT the Style Data Constructor:

```purescript
module ChalkStyles
  ( Style
  , black
  , red
  , green
  , yellow
  , blue
  , magenta
  , cyan
  , white
  , blackBright
  , gray
  , grey
  , redBright
  , greenBright
  , yellowBright
  , blueBright
  , magentaBright
  , cyanBright
  , whiteBright
  , bgBlack
  , bgRed
  , bgGreen
  , bgYellow
  , bgBlue
  , bgMagenta
  , bgCyan
  , bgWhite
  , bgBlackBright
  , bgGray
  , bgGrey
  , bgRedBright
  , bgGreenBright
  , bgYellowBright
  , bgBlueBright
  , bgMagentaBright
  , bgCyanBright
  , bgWhiteBright
  , reset
  , bold
  , dim
  , italic
  , underline
  , inverse
  , hidden
  , strikethrough
  , visible
  )
where
```

① Export the Type but not the Data Constructor. If this line was `Style(..)`, then the Data Constructors would also be exported.

I’ve set up another GitHub Gist for this improvement at this link, ChalkStylesExports.purs.

Click the link and copy and paste the contents of ChalkStylesExports.purs into your ChalkStyles.purs.

If you don’t have access to GitHub, then the above code is all that changed.

We now have a Type-safe way to call chalk. It is IMPOSSIBLE to use chalk in a way that will crash our program.

Make the following changes to your code:

```purescript
import ChalkStyles (Style, bold, red, dim, strikethrough)
import Data.Array ((:))

test :: Effect Unit
test = do
  let colorful styles = chalk $ red : styles
  log $ colorful [ bold, strikethrough ] "Test"
    <> colorful [] "Test" <> colorful [ dim ] "Test"
```

① Removed the (..) from Style since we no longer have access to its Data Constructor.

② Added dim and strikethrough.

③ Import (:).

④ Factored out common styles.

⑤ Added strikethrough to the first "Test". According to the chalk documentation, strikethrough isn’t widely supported. So, depending on what system you’re running on, you might not see this style.

⑥ Added an additional "Test" that’s dim.

Your output should look like:

![](img/8c0e9b687c62642e828ccb5481e11313_1241_0.png)

Don’t worry if the strikethrough doesn’t show up. Not all terminal programs support this. iTerm2 does support this.

## 27.2. Reversing JSON Keys in Javascript

Now that we know how to call Javascript from PureScript, we’re going to return to our Echo Server project. This time we’re going to reverse the keys in the JSON that the Echo Server sends back to us by using Javascript. We’re going to start with what we did last in Chapter 25.

So create a new file called Ch27b.purs and then copy and paste all of the code from Ch25b.purs into it. Then save it.

Now, CLOSE Ch25b.purs and make sure you’re working in Ch27b.purs.

Edit the module name to be Ch27b.

Then delete all of the Argonaut imports:

```purescript
import Data.Argonaut (class DecodeJson, JsonDecodeError(..)
    , decodeJson, (..:))

import Data.Argonaut.Decode.Decoders (decodeJObject)
```

Then import the Decode Typeclass:

```purescript
import Foreign.Generic.Class (class Encode, class Decode)
```

① Added class Decode to the import list.

You should now get errors on all of the DecodeJson Instance derivations, for example:

```purescript
derive newtype instance decodeJsonCentimeters :: DecodeJson Centimeters
```

This can be fixed by simply changing it to be:

```purescript
derive newtype instance decodeCentimeters :: Decode Centimeters
```

① Renamed decodeJsonCentimeters to decodeCentimeters.

② Renamed DecodeJson to Decode.

Now, edit all of the other similar derive declarations.

The next bunch of errors we’ll attack are the handwritten Argonaut Decoders, for example.
