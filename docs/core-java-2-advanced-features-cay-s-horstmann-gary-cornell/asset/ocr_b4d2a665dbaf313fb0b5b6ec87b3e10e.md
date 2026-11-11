> > **NOTE:** In addition to all the places already mentioned, classes can be loaded from the `jre/lib/endorsed` directory. This mechanism can only be used to replace certain standard Java libraries (such as those for XML and CORBA support) with newer versions. See http://docs.oracle.com/javase/8/docs/technotes/guides/standards for details.

# 9.12 The Class loader Hierarchy

Class loaders have a *parent/child* relationship. Every class loader except for the bootstrap one has a parent class loader. A class loader is supposed to give its parent a chance to load any given class and to only load it if the parent has failed. For example, when the system class loader is asked to load a system class (say, `java.util.ArrayList`), it first asks the extension class loader. That class loader first asks the bootstrap class loader. The bootstrap class loader finds and loads the class in `rt.jar`, so neither of the other class loaders searches any further.

Some programs have a plugin architecture in which certain parts of the code are packaged as optional plugins. If the plugins are packaged as JAR files, you can simply load the plugin classes with an instance of `URLClassLoader`.

```
URL url = new URL("file:///path/to/plugin.jar");
URLClassLoader pluginLoader = new URLClassLoader(new URL[] { url });
Class<?> cl = pluginLoader.loadClass("mypackage.MyClass");
```

Since no parent was specified in the URLClassLoader constructor, the parent of the pluginLoader is the system class loader. Figure 9.1 shows the hierarchy.

Most of the time, you don’t have to worry about the class loader hierarchy. Generally, classes are loaded because they are required by other classes, and that process is transparent to you.

Occasionally, however, you need to intervene and specify a class loader. Consider this example:

+   - Your application code contains a helper method that calls `Class.forName(classNameString)`.
+   - That method is called from a plugin class.
+   - The `classNameString` specifies a class that is contained in the plugin JAR.

The author of the plugin has reasons to expect that the class should be loaded. However, the helper method’s class was loaded by the system class loader, and that is the class loader used by `Class.forName`. The classes in the plugin JAR are not visible. This phenomenon is called *classloader inversion*.