
```
newtype LogonRequest = LogonRequest ①
  { ??? ②

  }
```

① The Data Constructor will be the tag field in the JSON.

② The Record will be the contents field in the JSON.

We’re NOT using Type Aliases so that we will get tags in the JSON. We want that so we’ll get some Type safety in our JSON structures.

Next, we’ll add the Record fields:

```
newtype LogonRequest = LogonRequest
  { userName :: String
  , password :: String
  }
```

We should stop here and think about the password here.

It’s defined as a String. This is NOT secure, but not because it’s a String. It’s not secure since we’re sending it from the Browser to the server in Plain Text.

That’s because our server is using HTTP, not HTTPS. Since we’re just writing a learning program, this will be fine, but we should always keep this in mind when designing any logon system.

By the way, you may think that encrypting the password on the client would solve this problem. But, it does not. The Browser is inherently insecure. We have debugging tools build right in to every Browser on every desktop. Basically, hacker tools have been built into every web application on the planet.

In fact, encrypting our password on the client and then sending it over an insecure channel is only mildly more secure than sending it in plain text.

In the plain-text scenario, a hacker just has to intercept the transmission and they can read the password.

When the password is encrypted on the client, a hacker has to first intercept the encrypted password. Then they’d have to understand how the code that encrypted the password works. And then they could decrypt it.

This is possible because the encryption code is available to the hacker since it’s encrypted in the Browser and if the hacker can access the logon page, they’ll have access to that code.

That code could then be put into a program to allow the hacker to use a brute-force attack by trying passwords until the stolen encryption code produces the encrypted password that the hacker intercepted.

The second scenario is much more work for the hacker and will keep some hackers out, but it’s far from

secure and both should be considered dangerous.

In other words, all logon systems that use passwords should communicate over HTTPS. If you make a server that communicates over HTTP, then you should put it behind a Load Balancer or Reverse Proxy that does communicate over HTTPS.

Then you put the insecure server behind a firewall, i.e. you make sure that it’s not accessible from the Internet. The only way to communicate with your insecure server is to go through the Reverse Proxy or Load Balancer.

With that out of the way, we’ll model the Logon Response based on the following JSON:

```
{ "tag": "LogonResponse",
  "contents": {
    "tag": "LogonResultsSuccess",
    "contents": {
      "authToken": "e0fc09ad-894a-4399-9940-870895c27394",
      "mustChangePassword": true
    }
  }
}
```

Notice how LogonResultsSuccess is a tag. This is the antithesis of LogonResultsFailure in the failure case:

```
{ "tag": "LogonResponse",
  "contents": {
    "tag": "LogonResultsFailure"
  }
}
```

First thing to do then is to make a type for these tags, which are Data Constructors:

```
import Data.UUID (UUID) -- COMPILER ERROR!!

data LogonResults
  = LogonResultsSuccess ①
    { authToken :: UUID ②
    , mustChangePassword :: Boolean
    }
  | LogonResultsFailure
```

① Data Construtor is tag in the JSON.

② Record is contents in JSON.

Update you code to match this if you haven’t already.

The compiler error is because this package is not part of our spago.dhall, so let’s add it:

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "aff"
  , "arrays"
  , "console"
  , "effect"
  , "httpure"
  , "maybe"
  , "prelude"
  , "psci-support"
  , "uuid" ①
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① Keeping the list in alphabetical order.

Then kill the server (if it’s still running) and run:

```
npx spago build
```

We’ll still ignore the warning regarding aff.

Now if you save Logon.purs, the compiler error should disappear.

But there’s one more thing to do. Go look up UUID on Pursuit and then click on the package name in the Search Results.

Read what it says in the package docs, then return here.

Here’s what I found:

> Wrapper for the uuid npm package. This package is not installed automatically, as it comes from npm. Install it with npm install -S uuid.

To install the npm package and update your package.json, run:

```
npm install --save uuid@8.3.2 ①
```

① In the docs, they say to use -S which is equivalent to --save.

Here are the response JSON structures for reference:

```
{ "tag": "LogonResponse", "contents": { "tag": "LogonResultsSuccess", "contents": { "authToken": "e0fc09ad-894a-4399-9940-870895c27394", "mustChangePassword": true } } }

{ "tag": "LogonResponse", "contents": { "tag": "LogonResultsFailure" } }
```

And finally, we need to define the Type for LogonResponse:

```
newtype LogonResponse = LogonResponse LogonResults
```

Add this Type and then create Encode and Decode Instances for LogonRequest, LogonResults and LogonResponse. Use the code you wrote in other Chapters as reference for how to do this.

Do this before reading on.

First, here are those changes for LogonRequest:

```
import Data.Generic.Rep (class Generic) ①
import Foreign.Generic (genericEncode, genericDecode)
import Foreign.Generic.Class (class Encode, class Decode, defaultOptions)

newtype LogonRequest = LogonRequest ②
  { userName :: String
  , password :: String
  }
derive instance genericLogonRequest :: Generic LogonRequest _

instance encodeLogonRequest :: Encode LogonRequest where
  encode = genericEncode defaultOptions

instance decodeLogonRequest :: Decode LogonRequest where
  decode = genericDecode defaultOptions
```

① Add these imports.

② This definition was already here, we just added the line to derive a Generic Instance.

If you didn’t finish, please stop and see if you can finish the Encode and Decode Instance for LogonResults and LogonResponse, then read on.

Here are the changes for LogonResults:

```
data LogonResults ①
  = LogonResultsSuccess
    { authToken :: UUID
    , mustChangePassword :: Boolean
    }
  | LogonResultsFailure
drive instance genericLogonResults :: Generic LogonResults _

instance encodeLogonResults :: Encode LogonResults where
  encode = genericEncode defaultOptions

instance decodeLogonResults :: Decode LogonResults where
  decode = genericDecode defaultOptions
```

① This definition was already here, we just added the line to derive a Generic Instance.

If you didn’t finish, please stop and see if you can finish the Encode and Decode Instance for LogonResponse, then read on.

Here are the changes for LogonResponse:

```
newtype LogonResponse = LogonResponse LogonResults
derive instance genericLogonResponse :: Generic LogonResponse _

instance encodeLogonResponse :: Encode LogonResponse where
    encode = genericEncode defaultOptions

instance decodeLogonResponse :: Decode LogonResponse where
    decode = genericDecode defaultOptions
```

① This definition was already here, we just added the line to derive a Generic Instance.

Now, before we rush off to model any other JSON Requests and Responses, we should write some test code to make sure we aren’t going down a bad path.

Create a file called Test.purs under src and add the following code:

```
module Test where

import Prelude

import Api.Logon (LogonRequest(..), LogonResponse(..), LogonResults(..))
import Effect (Effect)
import Effect.Class.Console (log)

test :: Effect Unit
test = do
    log "placeholder" ①
```

① We’ll remove this later.

Don’t worry too much about the compiler warnings regarding redundant imports. This is just test code that we’ll discard when we’re done with it.

Next, comment out main in Main.purs and replace it with:

```
import Effect (Effect) ①
import Test (test)

main :: Effect Unit
main = test
```

① Added these imports.

Again, don’t worry about redundant imports just yet.
