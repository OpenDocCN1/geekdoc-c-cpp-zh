+   - The file `.java.policy` (notice the period at the beginning of the file name) in the user’s home directory

> **NOTE:** You can change the locations of these files in the `java.security` configuration file in the `jdk/conf/security` directory. The defaults are specified as
> 
> ```text
> policy.url.1=file:${java.home}/lib/security/java.policy
> policy.url.2=file:${user.home}/.java.policy
> ```
> 
> A system administrator can modify the `java.security` file and specify policy URLs that reside on another server and cannot be edited by users. There can be any number of policy URLs (with consecutive numbers) in the policy file. The permissions of all files are combined.
> 
> If you want to store policies outside the file system, you can implement a subclass of the `Policy` class that gathers the permissions. Then change the line
> 
> ```text
> policy.provider=sun.security.provider.PolicyFile
> ```
> 
> in the `java.security` configuration file.

During testing, we don’t like to constantly modify the standard policy files. Therefore, we prefer to explicitly name the policy file required for each application. Place the permissions into a separate file—say, `MyApp.policy`. To apply the policy, you have two choices. You can set a system property inside your application’s main method:

```
System.setProperty("java.security.policy", "MyApp.policy");
```

Alternatively, you can start the virtual machine as

```
java -Djava.security.policy=MyApp.policy MyApp
```

In these examples, the `MyApp.policy` file is added to the other policies in effect. If you add a second equal sign, for example:

```
java -Djava.security.policy==MyApp.policy MyApp
```

then your application will use *only* the specified policy file, and the standard policy files will be ignored.

> **CAUTION:** Any easy mistake during testing is to accidentally leave a `.java.policy` file that grants a lot of permissions, perhaps even `AllPermission`, in the home directory. If you find that your application doesn’t seem to pay attention to the restrictions in your policy file, check for a left-behind `.java.policy` file in your home directory. If you use a UNIX system, this is a particularly easy mistake to make because files with names that start with a period are not displayed by default.