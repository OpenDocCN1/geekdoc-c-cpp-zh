For example, suppose your application needs to find its working directory relative to a given base directory that is read from a configuration file, as in the preceding example.

```
```java
Path workRelative = Paths.get("work");
Path workPath = basePath.resolve(workRelative);
```
```

There is a shortcut for the resolve method that takes a string instead of a path:

```
```java
Path workPath = basePath.resolve("work");
```
```

There is a convenience method resolveSibling that resolves against a path's parent, yielding a sibling path. For example, if workPath is /opt/myapp/work, the call

```
```java
Path tempPath = workPath.resolveSibling("temp");
```
```

creates /opt/myapp/temp.

The opposite of resolve is relativize. The call p.relativize(r) yields the path q which, when resolved with p, yields r. For example, relativizing "/home/harry" against "/home/fred/input.txt" yields "../fred/input.txt". Here, we assume that .. denotes the parent directory in the file system.

The normalize method removes any redundant . and .. components (or whatever the file system may deem redundant). For example, normalizing the path /home/harry/../fred/./input.txt yields /home/fred/input.txt.

The toAbsolutePath method yields the absolute path of a given path, starting at a root component, such as /home/fred/input.txt or c:\users\fred\input.txt.

The Path interface has many useful methods for taking paths apart. This code sample shows some of the most useful ones:

```
```java
Path p = Paths.get("/home", "fred", "myprog.properties");
Path parent = p.getParent(); // the path /home/fred
Path file = p.getFileName(); // the path myprog.properties
Path root = p.getRoot(); // the path /
```
```

As you have already seen in Volume I, you can construct a Scanner from a Path object:

```
```java
Scanner in = new Scanner(Paths.get("/home/fred/input.txt"));
```
```

> > **NOTE:** Occasionally, you may need to interoperate with legacy APIs that use the File class instead of the Path interface. The Path interface has a toFile method, and the File class has a toPath method.