```
**Listing 9.14** jaas/JAASTest.policy

```
1 grant codebase "file:login.jar"
2 {
3    permission java.awt.AWTPermission "showWindowWithoutWarningBanner";
4    permission java.awt.AWTPermission "accessEventQueue";
5    permission javax.security.auth.AuthPermission "createLoginContext.Login1";
6    permission javax.security.auth.AuthPermission "doAsPrivileged";
7    permission javax.security.auth.AuthPermission "modifyPrincipals";
8    permission java.io.FilePermission "jaas/password.txt", "read";
9 };
10
11 grant principal jaas.SimplePrincipal "role=admin"
12 {
13    permission java.util.PropertyPermission "*", "read";
14 };
```
```

```
**Listing 9.15** jaas/jaas.config

```
1 Login1
2 {
3    jaas.SimpleLoginModule required pwfile="jaas/password.txt" debug=true;
4 };
```
```

+   **javax.security.auth.callback.CallbackHandler** 1.4
+   
+   - void handle(Callback[] callbacks)
+     handles the given callbacks, interacting with the user if desired, and stores the
+     security information in the callback objects.

+   **javax.security.auth.callback.NameCallback** 1.4
+   
+   - NameCallback(String prompt)
+   - NameCallback(String prompt, String defaultName)
+     constructs a NameCallback with the given prompt and default name.
+   - String getName()
+   - void setName(String name)
+     gets or sets the name gathered by this callback.
+   - String getPrompt()
+     gets the prompt to use when querying this name.
+   - String getDefaultName()
+     gets the default name to use when querying this name.