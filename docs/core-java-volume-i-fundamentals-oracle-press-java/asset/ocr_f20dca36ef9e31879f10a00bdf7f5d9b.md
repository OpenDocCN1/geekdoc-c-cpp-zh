# java.util.prefs.Preferences 1.4

+   - `Preferences userRoot()`

returns the root preferences node of the user of the calling program.

+   - `Preferences systemRoot()`

returns the systemwide root preferences node.

+   - `Preferences node(String path)`

returns a node that can be reached from the current node by the given path. If path is absolute (that is, starts with a /), then the node is located starting from the root of the tree containing this preference node. If there isn’t a node with the given path, it is created.

+   - `Preferences userNodeForPackage(Class cl)`

+   - `Preferences systemNodeForPackage(Class cl)`

returns a node in the current user’s tree or the system tree whose absolute node path corresponds to the package name of the class cl.

+   - `String[] keys()`

returns all keys belonging to this node.

+   - `String get(String key, String defval)`

+   - `int getInt(String key, int defval)`

+   - `long getLong(String key, long defval)`

+   - `float getFloat(String key, float defval)`

+   - `double getDouble(String key, double defval)`

+   - `boolean getBoolean(String key, boolean defval)`

+   - `byte[] getByteArray(String key, byte[] defval)`

returns the value associated with the given key or the supplied default value if no value is associated with the key, the associated value is not of the correct type, or the preferences store is unavailable.