to learn PureScript and, more specifically, when we're learning how do we build a real application in a Purely Functional Programming Language.

So, instead, we're just going to read the data from a file. But, just because we're being expedient doesn't mean we won't try to do some best practices, e.g. we're not going to store passwords in the Accounts File in Plain Text. We'll actually hash them as is the norm in real-world systems.

I'd like to capture this new decision somewhere and I don't like it just buried here in the words of the previous paragraph because requirements like that tend to get lost or forgotten.

I want to note this decision on our diagram, which means I was wrong about the drawing not changing:

![](bbox=[0.144, 0.279, 0.853, 0.628])

The elements of the CSV (Comma Separated Values) file are as follows:

+   - userName - A unique identifier for logging on to the system.
+   - passwordHash - The hash that's calculated from the password.
+   - temporaryPassword - true if the current password MUST be changed upon the next logon.
+   - admin - true if Administrative Account.
+   - firstName - User's first name.
+   - lastName - User's last name.

The next step is to write a formal definition for our API. We'll do that based on the list of functions that our application will perform.

The first API call will be to try to logon a user. Let's define what that JSON looks like, both the Request made by the Browser and all possible responses by the Server.