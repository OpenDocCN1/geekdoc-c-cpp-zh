```
```
});
T result = Subject.doAs(subject, action); // or Subject.doAsPrivileged(subject, action, null)
```
```

If the actions can throw checked exceptions, you need to implement the `PrivilegedExceptionAction` interface instead.

The difference between the doAs and doAsPrivileged methods is subtle. The doAs method starts out with the current access control context, whereas the doAsPrivileged method starts out with a new context. The latter method allows you to separate the permissions for the login code and the “business logic.” In our example application, the login code has permissions

```
```
permission javax.security.auth.AuthPermission "createLoginContext.Login1";
permission javax.security.auth.AuthPermission "doAsPrivileged";
```
```

The authenticated user has a permission

```
```
permission java.util.PropertyPermission "user.*", "read";
```
```

If we had used doAs instead of doAsPrivileged, then the login code would have also needed that permission.

The program in Listings 9.6 and 9.7 demonstrates how to restrict permissions to certain users. The AuthTest program authenticates a user and runs a simple action that retrieves a system property.

To make this example work, package the code for the login and the action into two separate JAR files:

```
```
javac auth/*.java
jar cvf login.jar auth/AuthTest.class
jar cvf action.jar auth/SysPropAction.class
```
```

If you look at the policy file in Listing 9.8, you will see that the UNIX user with the name harry has the permission to read all files. Change harry to your login name. Then run the command

```
```
java -classpath login.jar:action.jar
  -Djava.security.policy=auth/AuthTest.policy
  -Djava.security.auth.login.config=auth/jaas.config
  auth.AuthTest
```
```

Listing 9.9 shows the login configuration.

On Windows, change UnixPrincipal to NTUserPrincipal in AuthTest.policy and UnixLoginModule to NTLoginModule in jaas.config. When running the program, use a semicolon to separate the JAR files:

```
```
java -classpath login.jar;action.jar . . .
```
```