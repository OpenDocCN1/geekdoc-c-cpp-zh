
If the URL ends in a /, it refers to a directory. Otherwise, it is taken to be the name of a JAR file. For example,

```
grant codeBase "www.horstmann.com/classes/" { . . . };
grant codeBase "www.horstmann.com/classes/MyApp.jar" { . . . };
```

The code base is a URL and should always contain forward slashes as file separators, even for file URLs in Windows. For example,

```
grant codeBase "file:C:/myapps/classes/" { . . . };
```

> **NOTE:** Everyone knows that http URLs start with two slashes (http://). But there is enough confusion about file URLs, so the policy file reader accepts two forms of file URLs—namely, file://localFile and file:localFile. Furthermore, a slash before a Windows drive letter is optional. That is, all of the following are acceptable:
>
> ```
> file:C:/dir/filename.ext
> file:/C:/dir/filename.ext
> file:///C:/dir/filename.ext
> file://C:/dir/filename.ext
> ```
>
> Actually, in our tests, the file:///C:/dir/filename.ext is acceptable as well, and we have no explanation for that.

The permissions have the following structure:

```
permission className targetName, actionList;
```

The className is the fully qualified class name of the permission class (such as java.io.FilePermission). The targetName is a permission-specific value—for example, a file or directory name for the file permission, or a host and port for a socket permission. The actionList is also permission-specific. It is a list of actions, such as read or connect, separated by commas. Some permission classes don’t need target names and action lists. Table 9.2 lists the commonly used permission classes and their actions.

**Table 9.2 Permissions and Their Associated Targets and Actions**

| Permission | Target | Action |
|---|---|---|
| `java.io.FilePermission` | File target (see text) | read, write, execute, delete |
| `java.net.SocketPermission` | Socket target (see text) | accept, connect, listen, resolve |
| `java.util.PropertyPermission` | Property target (see text) | read, write |
| `java.lang.RuntimePermission` | `createClassLoader`<br>`getClassLoader`<br>`setContextClassLoader`<br>`enableContextClassLoaderOverride`<br>`createSecurityManager`<br>`setSecurityManager`<br>`exitVM`<br>`getenv.variableName`<br>`shutdownHooks`<br>`setFactory`<br>`setIO`<br>`modifyThread`<br>`stopThread`<br>`modifyThreadGroup`<br>`getProtectionDomain`<br>`readFileDescriptor`<br>`writeFileDescriptor`<br>`loadLibrary.libraryName`<br>`accessClassInPackage.packageName`<br>`defineClassInPackage.packageName`<br>`accessDeclaredMembers.className`<br>`queuePrintJob`<br>`getStackTrace`<br>`setDefaultUncaughtExceptionHandler`<br>`preferences`<br>`usePolicy` | None |
| `java.awt.AWTPermission` | `showWindowWithoutWarningBanner`<br>`accessClipboard`<br>`accessEventQueue`<br>`createRobot`<br>`fullScreenExclusive`<br>`listenToAllAWTEvents`<br>`readDisplayPixels`<br>`replaceKeyboardFocusManager`<br>`watchMousePointer`<br>`setWindowAlwaysOnTop`<br>`setAppletStub` | None |
| `java.net.NetPermission` | `setDefaultAuthenticator`<br>`specifyStreamHandler`<br>`requestPasswordAuthentication`<br>`setProxySelector`<br>`getProxySelector`<br>`setCookieHandler`<br>`getCookieHandler`<br>`setResponseCache`<br>`getResponseCache` | None |
| `java.lang.reflect.ReflectPermission` | `suppressAccessChecks` | None |
| `java.io.SerializablePermission` | `enableSubclassImplementation`<br>`enableSubstitution` | None |
| `java.security.SecurityPermission` | `createAccessControlContext`<br>`getDomainCombiner`<br>`getPolicy`<br>`setPolicy`<br>`getProperty.keyName`<br>`setProperty.keyName`<br>`insertProvider.providerName`<br>`removeProvider.providerName`<br>`setSystemScope`<br>`setIdentity.publicKey`<br>`setIdentity.info`<br>`addIdentity.certificate`<br>`removeIdentity.certificate`<br>`printIdentity`<br>`clearProviderProperties.providerName`<br>`putProviderProperty.providerName`<br>`removeProviderProperty.providerName`<br>`getSignerPrivateKey`<br>`setSignerKeyPair` | None |
| `java.security.AllPermission` | None | None |
| `javax.sound.sampled.AudioPermission` | `play`<br>`record` | None |
| `javax.security.auth.AuthPermission` | `doAs`<br>`doAsPrivileged`<br>`getSubject`<br>`getSubjectFromDomainCombiner`<br>`setReadOnly`<br>`modifyPrincipals`<br>`modifyPublicCredentials`<br>`modifyPrivateCredentials`<br>`refreshCredential`<br>`destroyCredential`<br>`createLoginContext.contextName`<br>`getLoginConfiguration`<br>`setLoginConfiguration`<br>`refreshLoginConfiguration` | None |
| `java.util.logging.LoggingPermission` | `control` | None |
| `java.sql.SQLPermission` | `setLog` | None |

As you can see from Table 9.2, most permissions simply permit a particular operation. You can think of the operation as the target with an implied action "permit". These permission classes all extend the BasicPermission class (see Figure 9.7 on p. 512). However, the targets for the file, socket, and property permissions are more complex, and we need to investigate them in detail.

File permission targets can have the following form:

- `file` — A file
- `directory/` — A directory
- `directory/*` — All files in the directory
- `*` — All files in the current directory
- `directory/-` — All files in the directory or one of its subdirectories
- `-` — All files in the current directory or one of its subdirectories
- `<<ALL FILES>>` — All files in the file system

For example, the following permission entry gives access to all files in the directory `/myapp` and any of its subdirectories:

```
permission java.io.FilePermission "/myapp/-", "read,write,delete";
```

You must use the `\\` escape sequence to denote a backslash in a Windows file name.

```
permission java.io.FilePermission "c:\\myapp\\-", "read,write,delete";
```

Socket permission targets consist of a host and a port range. Host specifications have the following form:

| Host specification | Meaning |
|---|---|
| `hostname` or `IPAddress` | A single host |
| `localhost` or the empty string | The local host |
| `*.domainSuffix` | Any host whose domain ends with the given suffix |
| `*` | All hosts |

Port ranges are optional and have the form:

| Port range | Meaning |
|---|---|
| `:n` | A single port |
| `:n-` | All ports numbered *n* and above |
| `-n` | All ports numbered *n* and below |
| `:n1-n2` | All ports in the given range |

Here is an example:

```
permission java.net.SocketPermission "*.horstmann.com:8000-8999", "connect";
```

Finally, property permission targets can have one of two forms:

| Property target | Meaning |
|---|---|
| `property` | A specific property |
| `propertyPrefix.*` | All properties with the given prefix |

Examples are "java.home" and "java.*".

For example, the following permission entry allows a program to read all properties that start with java.vm:

```
permission java.util.PropertyPermission "java.vm.*", "read";
```

You can use variables in policy files. The token `${property}` is replaced by the property value. For example, `${user.home}` is replaced by the home directory of the user. Here is a typical use of this system property in a permission entry:

```
permission java.io.FilePermission "${user.home}", "read,write";
```

To create platform-independent policy files, it is a good idea to use the file.separator property instead of explicit `/` or `\\`. To make this simpler, the special notation `${/}` is a shortcut for `${file.separator}`. For example,

```
permission java.io.FilePermission "${user.home}${/}-", "read,write";
```

This is a portable entry for granting permission to read and write in the user’s home directory and any of its subdirectories.

> **NOTE:** The JDK comes with a rudimentary tool, called *policytool*, that you can use to edit policy files (see Figure 9.8). Of course, this tool is not suitable for end users who would be completely mystified by most of the settings. We view it as a proof of concept for an administration tool that might be used by system administrators who prefer point-and-click over syntax. Still, what’s missing in it is a sensible set of categories (such as low, medium, or high security) that would be meaningful to nonexperts. As a general observation, we believe that the Java platform certainly contains all the pieces for a fine-grained security model but it could benefit from some polish in delivering these pieces to end users and system administrators.

![](img/7dd923a566750151a3aab0dacd0cdaa5_542_0.png)

Figure 9.8 The policy tool

### 9.2.4 Custom Permissions

In this section, you'll see how you can supply your own permission class that users can refer to in their policy files.

To implement your permission class, extend the Permission class and supply the following methods:
