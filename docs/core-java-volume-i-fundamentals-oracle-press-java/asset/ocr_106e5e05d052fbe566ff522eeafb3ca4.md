returns a set of all keys, including the keys from the default map.

+   - `void load(Reader in) throws IOException`\n\n  loads a property map from a reader.

+   - `void store(Writer out, String header)`\n\n  saves a property map to a writer. The header is in the first line of the stored file.

# **java.lang.System** 1.0

+   - `Properties getProperties()`\n\n  retrieves all system properties. The application must have permission to retrieve all properties, or a security exception is thrown.

+   - `String getProperty(String key)`\n\n  retrieves the system property with the given key name. The application must have permission to retrieve the property, or a security exception is thrown. The following properties can always be retrieved:

```
java.version
java.vendor
java.vendor.url
java.home
java.class.path
java.library.path
java.class.version
os.name
os.version
os.arch
file.separator
path.separator
line.separator
java.io.tmpdir
user.name
```