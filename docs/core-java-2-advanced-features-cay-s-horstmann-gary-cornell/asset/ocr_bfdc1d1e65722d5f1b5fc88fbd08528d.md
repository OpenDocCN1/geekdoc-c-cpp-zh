You can install policy files in standard locations. By default, there are two locations:

+   - The file `java.policy` in the Java platform’s home directory
+   - The file `.java.policy` (notice the period at the beginning of the file name) in the user’s home directory

**NOTE:** You can change the locations of these files in the `java.security` configuration file in the `jre/lib/security`. The defaults are specified as

```
    policy.url.1=file:${java.home}/lib/security/java.policy
    policy.url.2=file:${user.home}/.java.policy
```

A system administrator can modify the `java.security` file and specify policy URLs that reside on another server and cannot be edited by users. There can be any number of policy URLs (with consecutive numbers) in the policy file. The permissions of all files are combined.

If you want to store policies outside the file system, you can implement a subclass of the `Policy` class that gathers the permissions. Then change the line

```
    policy.provider=sun.security.provider.PolicyFile
```

in the `java.security` configuration file.

During testing, we don’t like to constantly modify the standard policy files. Therefore, we prefer to explicitly name the policy file required for each application. Place the permissions into a separate file—say, `MyApp.policy`. To apply the policy, you have two choices. You can set a system property inside your applications’ main method:

```
    System.setProperty("java.security.policy", "MyApp.policy");
```

Alternatively, you can start the virtual machine as

```
    java -Djava.security.policy=MyApp.policy MyApp
```

For applets, you should instead use

```
    appletviewer -J-Djava.security.policy=MyApplet.policy MyApplet.html
```

(You can use the -J option of the appletviewer to pass any command-line argument to the virtual machine.)