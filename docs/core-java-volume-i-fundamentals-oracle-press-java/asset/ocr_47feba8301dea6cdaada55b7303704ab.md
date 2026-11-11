```
```java
}

public static void printTypes(Type[] types, String pre,
                              String sep, String suf,
                              boolean isDefinition)
{
    if (pre.equals(" extends ") && Arrays.equals(types, new
Type[] { Object.class }))
        return;
    if (types.length > 0) System.out.print(pre);
    for (int i = 0; i < types.length; i++)
    {
        if (i > 0) System.out.print(sep);
        printType(types[i], isDefinition);
    }
    if (types.length > 0) System.out.print(suf);
}

public static void printType(Type type, boolean
isDefinition)
{
    if (type instanceof Class t)
    {
        System.out.print(t.getName());
    }
    else if (type instanceof TypeVariable t)
    {
        System.out.print(t.getName());
        if (isDefinition)
            printTypes(t.getBounds(), " extends ", " & ", "",
false);
    }
    else if (type instanceof WildcardType t)
    {
        System.out.print("?");
        printTypes(t.getUpperBounds(), " extends ", " & ",
"", false);
        printTypes(t.getLowerBounds(), " super ", " & ", "",
false);
    }
```
```