# ### java.security.auth.login.LoginContext 1.4

+   - `LoginContext(String name)`
+     constructs a login context. The name corresponds to the login descriptor in the JAAS configuration file.
+   - `void login()`
+     establishes a login or throws `LoginException` if the login failed. Invokes the `login` method on the managers in the JAAS configuration file.
+   - `void logout()`
+     logs out the subject. Invokes the `logout` method on the managers in the JAAS configuration file.
+   - `Subject getSubject()`
+     returns the authenticated subject.

# ### java.security.auth.Subject 1.4

+   - `Set<Principal> getPrincipals()`
+     gets the principals of this subject.
+   - `static Object doAs(Subject subject, PrivilegedAction action)`
+   - `static Object doAs(Subject subject, PrivilegedExceptionAction action)`
+   - `static Object doAsPrivileged(Subject subject, PrivilegedAction action, AccessControlContext context)`
+   - `static Object doAsPrivileged(Subject subject, PrivilegedExceptionAction action, AccessControlContext context)`
+     executes the privileged action on behalf of the subject. Returns the return value of the `run` method. The `doAsPrivileged` methods execute the action in the given access control context. You can supply a "context snapshot" that you obtained earlier by calling the static method `AccessController.getContext()`, or you can supply `null` to execute the code in a new context.

# ### java.security.PrivilegedAction 1.4

+   - `Object run()`
+     You must define this method to execute the code that you want to have executed on behalf of a subject.