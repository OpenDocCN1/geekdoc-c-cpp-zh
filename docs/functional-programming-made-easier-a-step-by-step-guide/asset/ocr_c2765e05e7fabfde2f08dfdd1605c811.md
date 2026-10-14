Takes a userName and a password and will produce a Hash as a String of hex characters. Notice that we return a String in the Aff Context. That’s because of our use of hex.

Next, we’ll write the left-hand side:

```
passwordHash :: String -> String -> Aff String
passwordHash userName password =
  ???
```

Next, step is to calculate the Salt using userNameSalt:

```
import Data.String.CodePoints (length) ①

passwordHash :: String -> String -> Aff String
passwordHash userName password =
  let salt = userNameSalt (3 * length userName) userName in ② ③
  ???
```

+   ① Import length.

+   ② Make the Salt 3 times longer than the userName.

+   ③ Note the in keyword. That’s because we’re not in a do block.

Finally, we’ll call hex on the password concatenated with its salt:

```
import Node.Crypto.Hash (Algorithm(..), hex) ①
import Effect.Class (liftEffect)

passwordHash :: String -> String -> Aff String
passwordHash userName password =
  let salt = userNameSalt (3 * length userName) userName in
  liftEffect $ hex SHA512 (password <> salt) ② ③ ④
```

+   ① Add these imports.

+   ② Use the SHA512 hash algorithm.

+   ③ Append salt to password to add some randomness into the password hash.

+   ④ Use liftEffect to convert the Effect of hex to Aff.

Now, we’re getting a shadowed variable warning on passwordHash in accountToCSV. Let’s fix this by renaming our new Function to passwordHashHex: