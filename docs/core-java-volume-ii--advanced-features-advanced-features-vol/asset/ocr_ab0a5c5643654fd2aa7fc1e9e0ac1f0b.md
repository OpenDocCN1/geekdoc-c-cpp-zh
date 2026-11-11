Just to show off the syntax, there is a second mechanism for primitive types:

```
```xml
<value type="int">30</value>
```
```

A configuration is a sequence of entries. Each entry has an ID and an object:

```
```xml
<config>
    <entry id="background">
        <construct class="java.awt.Color">
            <value type="int">55</value>
            <value type="int">200</value>
            <value type="int">100</value>
        </construct>
    </entry>
    ...
</config>
```
```

The parser checks that IDs are unique.

The DTD, shown in Listing 3.4, is straightforward.

Listing 3.5 contains the equivalent schema. In the schema, we can provide additional checking: an int or boolean element can only contain integer or boolean content. Note the use of the xs:group construct to define parts of complex types that are used repeatedly.

The program in Listing 3.2 shows how to parse a configuration file. A sample configuration is defined in Listing 3.3.

The program uses the schema instead of the DTD if you choose a file that contains the string -schema.

This example is a typical use of XML. The XML format is robust enough to express complex relationships. The XML parser adds value by taking over the routine job of validity checking and supplying defaults.

# Listing 3.2  read/XMLReadTest.java

```
```java
package read;

import java.io.*;
import java.lang.reflect.*;
import java.util.*;

import javax.xml.parsers.*;

import org.w3c.dom.*;
import org.xml.sax.*;
```
```