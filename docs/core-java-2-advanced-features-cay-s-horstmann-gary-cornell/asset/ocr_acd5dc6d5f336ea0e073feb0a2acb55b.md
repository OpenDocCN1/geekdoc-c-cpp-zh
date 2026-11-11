# Listing 10.17  *(Continued)*

```
```java
listenerList.remove(TreeModelListener.class, l);
}

protected void fireTreeStructureChanged(Object oldRoot)
{
    TreeModelEvent event = new TreeModelEvent(this, new Object[] { oldRoot });
    for (TreeModelListener l : listenerList.getListeners(TreeModelListener.class))
        l.treeStructureChanged(event);
}
}
```
```

# Listing 10.18  `treeModel/Variable.java`

```
```java
package treeModel;

import java.lang.reflect.*;
import java.util.*;

/**
 * A variable with a type, name, and value.
 */
public class Variable
{
    private Class<?> type;
    private String name;
    private Object value;
    private ArrayList<Field> fields;

    /**
     * Construct a variable.
     * @param aType the type
     * @param aName the name
     * @param aValue the value
     */
    public Variable(Class<?> aType, String aName, Object aValue)
    {
        type = aType;
        name = aName;
        value = aValue;
        fields = new ArrayList<>();

        // find all fields if we have a class type except we don't expand strings and null values

        if (!type.isPrimitive() && !type.isArray() && !type.equals(String.class) && value != null)
        {
            // get fields from the class and all superclasses
```
```