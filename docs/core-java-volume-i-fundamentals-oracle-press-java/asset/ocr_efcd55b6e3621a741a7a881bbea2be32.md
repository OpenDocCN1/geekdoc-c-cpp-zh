# **TIP:**

As you can see, the version numbering changed in Java 9. This seemingly small change broke a good number of tools that had relied on the old format. If you parse the version string, be sure to read JEP 322 at [http://openjdk.java.net/jeps/322](http://openjdk.java.net/jeps/322) to see how version strings will be formatted in the future—or at least, until the numbering scheme changes again.

The `Properties` class has two mechanisms for providing defaults. First, whenever you look up the value of a string, you can specify a default that should be used automatically when the key is not present.

```
```java
String filename = settings.getProperty("filename", "");
```
```

If there is a `"filename"` property in the property map, `filename` is set to that string. Otherwise, `filename` is set to the empty string.

If you find it too tedious to specify the default in every call to `getProperty`, you can pack all the defaults into a secondary property map and supply that map in the constructor of your primary property map.

```
```java
var defaultSettings = new Properties();
defaultSettings.setProperty("width", "600");
defaultSettings.setProperty("height", "400");
defaultSettings.setProperty("filename", "");
...
var settings = new Properties(defaultSettings);
```
```

Yes, you can even specify defaults to defaults if you give another property map parameter to the `defaultSettings` constructor, but it is not something one would normally do.