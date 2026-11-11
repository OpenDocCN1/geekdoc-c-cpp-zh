A new configuration is read from the location specified by the `java.util.logging.config.file` system property. Then the mapper is applied to resolve the values for all keys in the old or new configuration. The mapper is a `Function<String,BiFunction<String,String,String>>`. It maps keys in the existing configuration to replacement functions. Each replacement function receives the old and new values associated with the key (or `null` if there is no associated value), and produces a replacement, or `null` if the key should be dropped in the update.

That sounds rather complex, so let’s walk through a couple of examples. A useful mapping scheme would be to merge the old and new configurations, preferring the new value when a key is present in both the old and new configurations. Then the mapper is

```
    key -> ((oldValue, newValue) -> newValue == null ? oldValue :
    newValue)
```

Or perhaps you want to only update the keys that start with `com.mycompany` and leave the others unchanged:

```
    key -> key.startsWith("com.mycompany")
        ? ((oldValue, newValue) -> newValue)
        : ((oldValue, newValue) -> oldValue)
```

It is also possible to change logging levels in a running program by using the `jconsole` program. See [www.oracle.com/technetwork/articles/java/jconsole-1564139.html#LoggingControl](http://www.oracle.com/technetwork/articles/java/jconsole-1564139.html#LoggingControl) for information.

**NOTE:**

The logging properties file is processed by the `java.util.logging.LogManager` class. It is possible to specify a different log manager by setting the `java.util.logging.manager` system property to the name of a subclass. Alternatively, you can keep the standard log manager