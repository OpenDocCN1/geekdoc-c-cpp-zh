# Listing 8.13 *(Continued)*

```
```java
if (getClass() != otherObject.getClass()) return false;
Item other = (Item) otherObject;
return Objects.equals(description, other.description) && partNumber == other.partNumber;
}

@LogEntry(logger = "com.horstmann")
public int hashCode()
{
    return Objects.hash(description, partNumber);
}
}
```
```

# Listing 8.14  set/Test.java

```
```java
package set;

import java.util.*;
import java.util.logging.*;

/**
 * @version 1.02 2012-01-26
 * @author Cay Horstmann
 */
public class SetTest
{
    public static void main(String[] args)
    {
        Logger.getLogger("com.horstmann").setLevel(Level.FINEST);
        Handler handler = new ConsoleHandler();
        handler.setLevel(Level.FINEST);
        Logger.getLogger("com.horstmann").addHandler(handler);

        Set<Item> parts = new HashSet<>();
        parts.add(new Item("Toaster", 1279));
        parts.add(new Item("Microwave", 4104));
        parts.add(new Item("Toaster", 1279));
        System.out.println(parts);
    }
}
```
```

# 8.7.2  Modifying Bytecodes at Load Time

In the preceding section, you saw a tool that edits class files. However, it can be cumbersome to add yet another tool into the build process. An attractive