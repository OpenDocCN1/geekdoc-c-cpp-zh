```
```java
public class ProgramResources_en_US extends ListResourceBundle
{
    private static final Object[][] contents =
    {
        { "backgroundColor", Color.blue },
        { "defaultPaperSize", new double[] { 216, 279 } }
    };
    public Object[][] getContents() { return contents; }
}
```
```

> > **NOTE:** The paper sizes are given in millimeters. Everyone on the planet, with the exception of the United States and Canada, uses ISO 216 paper sizes. For more information, see www.cl.cam.ac.uk/~mgk25/iso-paper.html.

Alternatively, your resource bundle classes can extend the ResourceBundle class. Then you need to implement two methods, to enumerate all keys and to look up the value for a given key:

```
```java
Enumeration<String> getKeys()
Object handleGetObject(String key)
```
```

The getObject method of the ResourceBundle class calls the handleGetObject method that you supply.

| java.util.ResourceBundle 1.1 |
|---|
| • `static ResourceBundle getBundle(String baseName, Locale loc)`<br>• `static ResourceBundle getBundle(String baseName)`<br><br>loads the resource bundle class with the given name, for the given locale or the default locale, and its parent classes. If the resource bundle classes are located in a package, the base name must contain the full package name, such as `intl.ProgramResources`. The resource bundle classes must be public so that the getBundle method can access them.<br><br>• `Object getObject(String name)`<br><br>looks up an object from the resource bundle or its parents.<br><br>• `String getString(String name)`<br><br>looks up an object from the resource bundle or its parents and casts it as a string.<br><br>• `String[] getStringArray(String name)`<br><br>looks up an object from the resource bundle or its parents and casts it as a string array. |