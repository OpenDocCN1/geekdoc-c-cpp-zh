# Listing 11.19  *(Continued)*

```
```java
95  catch (ClassNotFoundException e)
96  {
97      return new DataFlavor[0];
98  }
99 }

101 public boolean isDataFlavorSupported(DataFlavor flavor)
102 {
103     return DataFlavor.stringFlavor.equals(flavor)
104             || "application".equals(flavor.getPrimaryType())
105             && "x-java-serialized-object".equals(flavor.getSubType())
106             && flavor.getRepresentationClass().isAssignableFrom(obj.getClass());
107 }

109 public Object getTransferData(DataFlavor flavor) throws UnsupportedFlavorException
110 {
111     if (!isDataFlavorSupported(flavor)) throw new UnsupportedFlavorException(flavor);
112
113     if (DataFlavor.stringFlavor.equals(flavor)) return obj.toString();
114
115     return obj;
116 }
117 }
```
```

# 11.13.6 Using a Local Clipboard to Transfer Object References

Occasionally, you might need to copy and paste a data type that isn’t one of the data types supported by the system clipboard and that isn’t serializable. To transfer an arbitrary Java object reference within the same JVM, use the MIME type

```
```text
application/x-java-jvm-local-object;class=className
```
```

You need to define a Transferable wrapper for this type. The process is entirely analogous to the SerialTransferable wrapper of the preceding example.

An object reference is only meaningful within a single virtual machine. For that reason, you cannot copy the shape object to the system clipboard. Instead, use a local clipboard:

```
```java
Clipboard clipboard = new Clipboard("local");
```
```

The construction parameter is the clipboard name.

However, using a local clipboard has one major disadvantage. You need to synchronize the local and the system clipboard, so that users don’t confuse the two. Currently, the Java platform doesn’t do that synchronization for you.