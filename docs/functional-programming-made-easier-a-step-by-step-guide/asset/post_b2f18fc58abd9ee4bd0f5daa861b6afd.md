
② When the browser sends OPTIONS, we’re going to respond to allow all Methods and Headers from any origin.

③ Responding with an empty body using emptyResponse since OPTIONS only needs to return headers.

But, we’re not going to do any of this. I’ve only put it here for future reference, i.e. if you find yourself in a situation where you need to support CORS on the server.

## 30.9.2. Static File Server Solution

Instead of dealing with CORS, we’re going to have our server serve our index.html and other files to the Browser instead of relying on Python’s SimpleHTTPServer.

This means that the files and the API calls will be from the exact same server avoiding the CORS issue altogether.

To do this, we’re going to have to support the GET method since that’s what the Browser uses to retrieve files from a web server.

But, we’re going to want to also make sure we don’t serve up just any files. So, we’ll support a Whitelist of acceptable file types, i.e. file extensions, that can be safely served up.

Another thing we’ll do is to sequester the files that can be served up when we build the client. These files will be served up by our server.

First, let’s change our build to copy the appropriate files to a dist, or distribution Folder. To do this, we’ll need to modify our Makefile in our client:

```
build:
    npx spago bundle-app ①
    mkdir -p dist ②
    cp {index.html,index.js} dist ③

.PHONY: build ④
```

① Changed build to bundle-app. bundle-app is the build option in spago to build all of your code into a single index.js file for the Browser.

② The -p option will not error if the directory already exists.

③ Copy both index.html and index.js to dist. Make sure there are NO spaces in the list of files.

④ Removed the run target from the file and from this line.

Make the above change to your client’s Makefile.

Next, add index.js to your .gitignore:

```
/bower_components/
/node_modules/
/.pulp-cache/
/output/
/generated-docs/
/.psc-package/
/.psc*
/.purs*
/.psa*
/.spago
index.js ①
```

① This is the output of the bundle-app command.

Now run to create a distribution, i.e. release:

```
make build
```

You should now see a dist Folder with the appropriate files in it.

Remember that every time we change the client, we’ll have to run make build to BUILD and COPY the files so that our server can serve the updated files to the Browser.

Next, add the following line to the .gitignore file that spago init created:

```
dist
```

This will EXCLUDE this directory from the git repository.

If you’re coding in VSCode, you should notice that index.js and the dist directory are grayed out.

Now, switch to your server project.

We’re going to support serving up files, but before we do let’s make a plan:

- Maintain a Whitelist of file extensions that are allowed to be retrieved
- Return the appropriate MIME Type based on the file extension
- Read files from ../client/dist, which is relative to the server directory

First, we’ll create a Whitelist in Main.purs:

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

② Using fromFoldable from Map to take an Array of Tuples of keys and values to create our Map.

③ Each entry in our Array is a Tuple where the first position has the key and the second has the value.

Now, that I'm looking at this, it seems that we've got 2 sources of truth. The whitelistExtensions and mimeTypes. Imagine adding to mimeTypes but forgetting to add it to whitelistExtensions or vice versa.

Delete whitelistExtensions and we'll use mimeTypes as our Whitelist. When we cannot find a MIME Type then we'll treat that file as being blacklisted.

Next, add a Function called mimeType (no s) that takes a fileName and returns its MIME Type. Use mimeTypes to look up its type. Return here to continue reading when you're done.

First, we start with the Type Signature:

```
mimeType :: String -> Maybe MediaType ①
```

① Returns a Maybe since we could fail to find the MIME Type. In that case, we'll consider this file request as invalid since it's not part of our Whitelist.

Next, we'll do the start of the implementation:

```
mimeType :: String -> Maybe MediaType
mimeType fileName = do ①
  ???
```

① Coding in the Maybe Monad.

Next step is to get the File Extension:

```
import Data.Array (last, tail) ①
import Data.String.Common (split)
import Data.String.Pattern (Pattern(..))

mimeType :: String -> Maybe MediaType
mimeType fileName = do
  ext <- last ==< (tail $ split (Pattern ".") fileName) ② ③
  ???
```

① Added these imports.

② Split the fileName on . and throw away the head, i.e. part before the file extension, then get the last item in the Array.

③ Either extract the Just result or Short-circuit returning Nothing to the caller. We can do this because we're in the Maybe Monad.

And finally, we’ll look up the File Extension in the mimeTypes Map:

```
import Data.String.Common (split, toLower) ①

mimeType :: String -> Maybe MediaType
mimeType fileName = do
  ext <- last ==< (tail $ split (Pattern ".") fileName)
  Map.lookup (toLower ext) mimeTypes ②
```

① Added toLower to input list.

② Map.lookup will return a Maybe.

And since we have a do block with only 2 lines of code, we can rewrite this as:

```
mimeType :: String -> Maybe MediaType
mimeType fileName = (last ==< (tail $ split (Pattern ".") fileName)) >>=
  flip Map.lookup mimeTypes <<< toLower
```

I’m not sure I like this version better. You can choose for yourself. I’m going to keep the do block version.

Now, add the following to your code:

```
staticRoot :: String
staticRoot = "../client/dist"
```

This is the root directory for all static file requests. The files are considered static since they are not dynamically generated files by our server, i.e. it’s not Server Rendered content as one might find in technologies such as JSP, ASP.NET, WebForms, Next.js, etc. or when running React or Angular on the server.

Next, write a Function called staticFiles that will take a Request and return a ResponseM. From that request it’ll use the path, which is an Array, and staticRoot to build a path to the file. If the path is empty then index.html will be the default.

Then that file will be read and its contents returned to the client if and only if it’s in the Whitelist, i.e. we can find a MIME Type for its File Extension.

See how we did readTextFile in the Account Manager in our server as reference, but, in this case, use try from Control.Monad.Error.Class and when you cannot read the file send HTTPure.notFound, i.e. 404.

And finally, you’re going to want to send both Content-Length and Content-Type in the HTTP Headers. This can be accomplished with HTTPure.headers and by using the Primed version of ok, i.e. HTTPure.ok'.
