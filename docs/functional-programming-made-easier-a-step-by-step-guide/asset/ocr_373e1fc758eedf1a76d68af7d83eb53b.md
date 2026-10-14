```
whitelistExtensions :: Array String
whitelistExtensions = [ "js", "html", "jpg", "png" ]
```

Add this to server’s project in Main now.

We can add to this list if we have a need for a different file type. This is just an added precaution in case we accidentally put a file of a different extension into the client/dist folder. At least our server won’t deliver it.

Next, we’re going to write a Function that takes a File Extension and will return the appropriate MIME Type. The MIME Type will tell us what to put in the Content-Type HTTP Header in the response. This information will tell the Browser how to treat the file.

First, create a Map of File Extensions and their corresponding MIME Types. Use Data.MediaType and Data.MediaType.Common to help you. Call this map mimeTypes. Return here when you’re ready to move on.

First, we need to add media-types to our spago.dhall file so we can use this library:

```
npx spago install media-types
```

Then build:

```
npx spago build
```

And then we can add the following code to Main:

```
import Data.Map (Map) ①
import Data.Map as Map
import Data.MediaType (MediaType)
import Data.MediaType.Common as MIME
import Data.Tuple (Tuple(..))

mimeTypes :: Map String MediaType
mimeTypes = Map.fromFoldable [ ②
    Tuple "js" MIME.applicationJavascript ③
  , Tuple "html" MIME.textHTML
  , Tuple "jpg" MIME.imageJPEG
  , Tuple "png" MIME.imagePNG
]
```

① Added these imports.