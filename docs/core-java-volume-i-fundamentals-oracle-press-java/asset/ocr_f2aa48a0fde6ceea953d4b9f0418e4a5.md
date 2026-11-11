The Preferences class has a solution for the second problem. You can export the preferences of a subtree (or, less commonly, a single node) by calling the methods

```
```java
void exportSubtree(OutputStream out)
void exportNode(OutputStream out)
```
```

The data are saved in XML format. You can import them into another repository by calling

```
```java
void importPreferences(InputStream in)
```
```

Here is a sample file:

```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE preferences SYSTEM
"http://java.sun.com/dtd/preferences.dtd">
<preferences EXTERNAL_XML_VERSION="1.0">
    <root type="user">
        <map/>
        <node name="com">
            <map/>
            <node name="horstmann">
                <map/>
                <node name="corejava">
                    <map>
                        <entry key="height" value="200.0"/>
                        <entry key="left" value="1027.0"/>
                        <entry key="filename"
value="/home/cay/books/cj11/code/v1ch11/raven.html"/>
                        <entry key="top" value="380.0"/>
                        <entry key="width" value="300.0"/>
                    </map>
                </node>
            </node>
        </node>
    </root>
</preferences>
```
```