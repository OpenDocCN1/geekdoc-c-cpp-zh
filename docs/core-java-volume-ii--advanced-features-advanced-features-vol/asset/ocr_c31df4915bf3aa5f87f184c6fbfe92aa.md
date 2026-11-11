```
file:C:/dir/filename.ext
file://C:/dir/filename.ext
file:///C:/dir/filename.ext
```

Actually, in our tests, the file:///C:/dir/filename.ext is acceptable as well, and we have no explanation for that.

> **NOTE:** Consider an application that compiles some Java code, which requires a large number of permissions. Prior to JDK 9, you could have granted all permissions to the code in the tools.jar file. This JAR file doesn’t exist anymore. Instead, give permissions to the appropriate module, like this:

```
grant codeBase "jrt:/jdk.compiler"
{
    permission java.security.AllPermission;
};
```

The permissions have the following structure:

```
permission className targetName, actionList;
```

The className is the fully qualified class name of the permission class (such as java.io.FilePermission). The targetName is a permission-specific value—for example, a file or directory name for the file permission, or a host and port for a socket permission. The actionList is also permission-specific. It is a list of actions, such as read or connect, separated by commas. Some permission classes don’t need target names and action lists. Table 10.2 lists the commonly used permission classes and their actions.

**Table 10.2 Permissions and Their Associated Targets and Actions**

| Permission | Target | Action |
|---|---|---|
| `java.io.FilePermission` | File target (see text) | read, write, execute, delete |
| `java.net.SocketPermission` | Socket target (see text) | accept, connect, listen, resolve |
| `java.util.PropertyPermission` | Property target (see text) | read, write |

*(Continues)*