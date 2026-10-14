![](bbox=[0.14, 0.06, 0.86, 0.41])

Do you see that red box labeled Server? It’s time to drill down and design what’s inside of that box.

List out all of the moving parts to the server that you can think of before reading my list.

Here’s my list:

+   - Account Management
+     - Load ALL accounts
+     - Save an account
+   - SIGINT Handler
+   - API Handler
+     - Authorization
+     - Logon/Logoff
+     - Query Users
+     - Create User
+   - Session Management
+     - Logon
+     - Logoff
+     - Authentication

This is the best I can do at this point. There may be other things that we’ll add later as we discover them, but this is a good starting point.